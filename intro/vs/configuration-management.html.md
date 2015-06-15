---
title: "Atlas vs. Chef, Puppet, Ansible and Other Configuration Management"
---

## Atlas vs. Chef, Puppet, Ansible and Other Configuration Management

Configuration management tools install and manage software on a
machine that already exists. Depending on how you use Atlas,
configuration management is still required.

Sometimes, configuration management systems launch and manage infrastructure.
In this case, Atlas replaces that functionality by launching
images with Terraform. This immutable approach can speed up deploy times, increase visiblity
into what is deployed and help guarantee safety in deployments. "Immutable
infrastructure", as it is sometimes called, has numerous other benefits
that are written about broadly.

The Atlas workflow focuses on immutability in deployment. Infrastructure
should be launched in a configured state, rather then being configured
after being launched.

When using Atlas to deploy images as covered
in the [continuous deployment use case](/help/intro/use-cases/continuous-deployment-of-immutable-infrastructure), Atlas
expects configuration to be applied at build-time, during Packer builds.
Packer can leverage many different configuration management tools to configure the
image. It's often the case that Puppet, Ansible or Chef are used to
configure the image, but once configured the image is deployed
and managed by Terraform.

Because of this, Atlas can use existing configuration management systems.
Moving to image deploys is then just a matter of configuring
Packer and Terraform.

