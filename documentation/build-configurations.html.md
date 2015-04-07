---
title: "What are Build Configurations?"
---
## What are Build Configurations?

Build Configurations define the process to build artifacts (AMIs, OpenStack
images, Vagrant boxes, etc) using [Packer](https://packer.io). Packer is
built by HashiCorp and is a tool for creating identical machine
images for multiple platforms from a single source configuration.

Build Configurations are sent to Atlas with
[`packer push`](https://www.packer.io/docs/templates/push.html), which
sends the Packer template as well as any configuration scripts (Puppet, Chef,
shell, etc) used in the Packer build process.

Common use cases for build configurations include:

- A Packer template and associated scripts to configure and build a
Vagrant box for development.
- A Packer template and associated Puppet module to bake AMIs for
production deployments.
- A Packer template with VirtualBox and DigitalOcean builders to
produce a Vagrant box and DigitalOcean droplet in parallel. This
maintains parity between development and production.

Build Configurations and `packer push` replace running Packer locally with
running Packer in Atlas. This frees up developer machines, simplifies automated
deploy pipelines, and adds build versioning across an organization. Build
statuses and outputs are displayed in the Atlas dashboard.

To learn about the internals of Packer in greater detail,
visit the [Packer Documentation](https://packer.io/docs).
