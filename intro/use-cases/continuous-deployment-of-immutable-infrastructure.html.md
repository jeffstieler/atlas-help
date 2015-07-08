---
title: "Continuous Deployment of Immutable Infrastructure"
---

## Continuous Deployment of Immutable Infrastructure

Organizations can use the complete HashiCorp toolset to continuously deploy
immutable infrastructure. Build deployable artifacts with Packer, provision
instances with Terraform using those artifacts, and monitor and maintain the
infrastructure with Consul.

Below is a small example of this workflow.

1. A __developer__ works on changes to a `web` service locally in a Vagrant
environment. When the changes look good, the developer pushes the updated
application code to a source control system such as GitHub. From here, Atlas
turns this application code into a running, deployed application.
2. Packer ingests the application code and merges it with 
its required dependencies using a provisioning script
(Puppet, Ansible, Shell, etc) to create a deployable artifact for the `web` service.
This artifact could be an Amazon Machine Image, OpenStack image, Docker container, etc. 
3. The Packer-built artifact is stored in Atlas's artifact registry
under a namespace defining the artifact, such as `acmeinc/web`. 
4. Terraform then references this artifact from the registry and deploys an instance
using the artifact. For example, on Amazon Web Services, an instance would
be provisioned using a fully baked AMI. 
5. When an update is made to an artifact, a Terraform `plan` is automatically run, which
shows the difference in the artifact version for a deployed instance. 
An __operator__ is notified of a pending change.
5. An __operator__ reviews and confirms this infrastructure change which triggers
Terraform, running in Atlas, to apply the change.
6. It's important to note that a Consul agent is configured in the Packer build stage,
so when Terraform deploys a new instance of this `web` service, the Consul agent
identifies the instance as a `web`, it gets added to the Consul service registry,
and other services in the infrastructure can automatically discover it.
7. If the Consul health status of this `web` node changes, it triggers an alert
in Atlas and sends a notification via Slack or Email to the operations team.
8. If the alert identifies an issue which requires an application code change,
start at step 1!
