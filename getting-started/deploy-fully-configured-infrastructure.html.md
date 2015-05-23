---
title: "Deploy fully configured infrastructure"
previous: "getting-started/package-services-with-artifacts"
next: "getting-started/run-your-application"
---
## Recap
Before we deploy fully configured infrastructure, let's review what has already been done in the [getting started guide](/help/getting-started/getting-started-overview). First, we learned how to layout and deploy basic infrastructure with Terraform. Then we learned how to build configured machine images with Packer. Now we want to combine the two — layout and deploy fully configured infrastructure!

## Terraform configuration
Now that we have an artifact stored in Atlas, we can reference it in the Terraform configuration:

    provider "atlas" {
        token = "ATLAS_TOKEN_HERE"
    }

    provider "aws" {
        access_key = "ACCESS_KEY_HERE"
        secret_key = "SECRET_KEY_HERE"
        region = "us-east-1"
    }

    resource "atlas_artifact" "web" {
        name = "ATLAS_USERNAME_HERE/example-artifact"
        type = "aws.ami"
    }

Now, let's combine the artifact with the [Terraform configuration written in the first step](/help/getting-started/layout-infrastructure) by referencing the Atlas artifact as the AMI for our "aws_instance.web" resource. The complete Terraform configuration should now look as below.

    provider "atlas" {
        token = "ATLAS_TOKEN_HERE"
    }

    provider "aws" {
        access_key = "ACCESS_KEY_HERE"
        secret_key = "SECRET_KEY_HERE"
        region = "us-east-1"
    }

    resource "atlas_artifact" "web" {
        name = "ATLAS_USERNAME_HERE/example-artifact"
        type = "aws.ami"
    }

    resource "aws_security_group" "allow_all" {
        name = "allow_all"
        description = "Allow all inbound traffic"

        tags {
            Name = "allow_all"
        }

        ingress {
            from_port = 0
            to_port = 0
            protocol = "-1"
            cidr_blocks = ["0.0.0.0/0"]
        }
    }

    resource "aws_instance" "web" {
        instance_type = "t1.micro"
        ami = "${atlas_artifact.web.metadata_full.region-us-east-1}"
        security_groups = ["${aws_security_group.allow_all.name}"]

        tags {
            Name = "web_${count.index+1}"
        }

        # This will create 2 instances
        count = 2
    }

    resource "aws_elb" "web" {
        name = "terraform-example-elb"

        # The same availability zone as our instances
        availability_zones = ["${aws_instance.web.*.availability_zone}"]

        listener {
            instance_port = 80
            instance_protocol = "http"
            lb_port = 80
            lb_protocol = "http"
        }

        health_check {
            healthy_threshold = 2
            unhealthy_threshold = 2
            timeout = 5
            target = "TCP:80"
            interval = 10
        }

        security_groups = ["${aws_security_group.allow_all.id}"]

        # The instances are registered automatically
        instances = ["${aws_instance.web.*.id}"]
    }

Now, when you run the below `terraform push` command, it will reference the proper AMI stored in Atlas that is configured with Apache. Be sure to wait for your Packer build to finish!

    $ terraform push -name="ATLAS_USERNAME_HERE/example-environment"
    Configuration "hashicorp/example-environment" uploaded! (v2)

![Terraform Apply](/help-images/example-terraform-apply.png)

That's it! You now have a fully functional 2-tier infrastructure running on AWS. Up next we'll learn how to get application code on all of your servers.
