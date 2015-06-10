---
title: "Packer Build Environment"
---

## Packer Build Environment

This page outlines the environment that Packer runs in within Atlas.

### Files

All files in the uploading package (via [Packer push or GitHub]()),
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

### Hardware Limitations

Currently, each builder defined in the Packer template recieves
the following hardware resources. This is subject to change.

- 1 GB of memory
- 20 GBs of disk space

If this doesn't suit your needs, please [contact us](mailto:support@hashicorp.com).
