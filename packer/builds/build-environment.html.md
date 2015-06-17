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
