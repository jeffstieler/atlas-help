---
title: "What are Build Configurations?"
---
# What are Build Configurations?

Build Configurations represent configurations to run builds with
[Packer](https://packer.io).

These configurations generally contain a Packer template, any
configuration scripts (bash, Puppet, Chef et al) and dependencies.

Common use cases for these build configurations include:

- A Packer template and associated scripts to provision your organizations
Vagrant box for development
- A Packer template and associated Puppet module you use to bake AMIs for
your production deployments
- Packer builders for both Virtualbox and DigitalOcean images, for
maintaining a golden image used for both development and production

These are just some of the use cases of Build Configurations. Put simply,
`packer push` replaces the need to locally build and run Packer. Following
the push, builds are run in parallel in the Atlas infrastructure, showing
a UI and status page for output and information.
