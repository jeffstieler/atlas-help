---
title: "Creating AMI Artifacts with Atlas"
---
# Creating AMI Artifacts with Atlas

In an [immutable infrastructure]() workflow, it's important to version
and store full images (artifacts) to be deployed. This section covers
storing [AWS AMI]() images in Atlas to be queried and used later.

Note the actual AMI does _not get stored in Atlas_. Atlas
simply keeps the AMI ID as a reference to the target image. Tools
like Terraform can then use this in a deploy.

### Steps

If you run Packer in Atlas, the following will happen after a [push]():

1. Atlas will run `packer build` against your template in our infrastructure.
This spins up an AWS instance in your account and provisions it with
 any specified provisioners
1. Packer stops the instance and stores the result as an AMI in AWS
under your account. This then returns an ID (the artifact) that it passes to the Atlas post-processor
1. The Atlas post-processor creates and uploads the new artifact version with the
ID in Atlas of the type `amazon.ami` for use later

### Example

Below is a complete example Packer template that starts an AWS instance.

    {
      "push": {
        "name": "acmeinc/frontend"
      },
      "provisioners": [],
      "builders": [
        {
          "type": "amazon-ebs",
          "access_key": "",
          "secret_key": "",
          "region": "us-east-1",
          "source_ami": "ami-2ccc7a44",
          "instance_type": "c3.large",
          "ssh_username": "ubuntu",
          "ami_name": "Atlas Example {{ timestamp }}"
        }
      ],
      "post-processors": [
        {
          "type": "atlas",
          "artifact": "acmeinc/web-server",
          "artifact_type": "amazon.ami"
        }
      ]
    }

