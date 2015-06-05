---
title: "Continuous Deployment of Immutable Infrastructure"
---

## Continuous Deployment of Immutable Infrastructure

Using Packer to build artifacts linking any number of applications and their
bundled source code, organizations can continually create, store and deploy
immutable services with Atlas.

Below is a small example of this.

1. A __developer__ pushes application code to a `acmeinc/web` GitHub repository linked to Atlas
2. Packer configuration for a `acmeinc/frontend` service then merges this code with
its provisioning scripts (i.e Puppet, Shell, etc.) and automatically
builds an AMI artifact and stores it in Atlas
3. A Terraform `plan` is automatically queued and run, showing a difference
in the AMI for a deployed instance. An __operator__ is notified of a pending
change
4. An __operator__ reviews and confirms this infrastructure change
5. Terraform, running in Atlas, automatically applies these changes
6. Consul, running on the `frontend` service, notifies via Slack or Email
of any service disruptions, as well as providing a UI for the __operator__
