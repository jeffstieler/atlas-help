---
title: "Packer Build Environment"
---

## Packer Build Environment

This page outlines the environment that Packer runs in within Atlas.

### Environment Variables

You can set any number of environment variables that will be injected
into your build environment at runtime. These variables can be
used to configure your build with secrets or other key value configuration.

Variables are encrypted and stored securely.

### Supported Builders

Atlas currently supports running the following Packer builders:

- amazon-chroot
- amazon-ebs
- amazon-instance
- digitalocean
- docker
- googlecompute
- null
- openstack
- qemu
- virtualbox-iso
- vmware-iso

### Files

All files in the uploading package (via [Packer push or GitHub](/help/packer/builds/starting)),
and any [linked applications](/help/packer/builds/linked-applications) are available on the filesystem
of the build environment.

You can use the file icon on the running build to show a list of
available files.

Files can be copied to the destination image Packer is provisioning
with [Packer Provisioners](https://packer.io/docs/templates/provisioners.html).

An example of this with the Shell provisioner is below.

    "provisioners": [
        {
            "type": "shell",
            "scripts": [
                "scripts/vagrant.sh",
                "scripts/dependencies.sh",
                "scripts/cleanup.sh"
            ]
        }
    ]

We encourage use of relative paths over absolute paths to maintain portability
between Atlas and local builds.

### Hardware Limitations

Currently, each builder defined in the Packer template receives
the following hardware resources. This is subject to change.

- 1 GB of memory
- 20 GBs of disk space

If this doesn't suit your needs, please [contact us](mailto:support@hashicorp.com).

### Environment Variables

During each Packer build, the following environment variables are available as
part of the build:

- `ATLAS_TOKEN` - a unique token that can communicate with Atlas for the
duration of this build. This token will expire upon completion of the build.
This token is used as part of any Atlas-specific providers or post processors.
- `ATLAS_JOB_NUMBER` - a unique identifier for the complete Packer run including
all builds. Given a Packer template with multiple builders, all builders will be
grouped under a single "job number".
- `ATLAS_BUILD_ID` - a unique identifier for this particular builder within a
job. This is an internal number that uniquely refers to the particular builder
in a job.
- `ATLAS_BUILD_CONFIGURATION_VERSION` - the version of the
[build configuration](/help/glossary) version used during this build.
