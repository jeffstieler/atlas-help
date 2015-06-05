---
title: "Creating Vagrant Boxes with Packer"
---
# Creating Vagrant Boxes with Packer

We recommend using Packer to create boxes, as is it is fully repeatable and keeps a strong
history of changes within Atlas.

## Getting Started

Atlas has an [interactive tutorial for using Packer and Vagrant](/tutorial/packer-vagrant),
so it's best to follow that in place of a written guide.

At the end of this tutorial, you can use the example scripts and
templates to create your own Vagrant Box, or build on it
with help from the [Packer documentation](https://packer.io).

Using Packer requires more up front effort, but the repeatable and
automated builds will end any manual management of boxes. Additionally,
all boxes will be stored and served from Atlas, keeping a history along
 the way.

Some useful Vagrant Boxes documentation will help you learn
about managing Vagrant boxes in Atlas.

- [Vagrant Box Lifecycle](/help/vagrant/boxes/lifecycle)
- [Distributing Vagrant Boxes with Atlas](/help/vagrant/boxes/distributing)

## Atlas Post-Processor

Packer uses [post-processors]() to define how to process
artifacts after provisioning.

An example post-processor for Atlas and Vagrant is below. In this example,
the build runs on both VMware and Virtualbox and creatings two
different providers for the same box version (`0.0.1`).

    "post-processors": [
        [{
            "type": "vagrant",
            "keep_input_artifact": false
        },
        {
            "type": "atlas",
            "only": ["vmware-iso"],
            "artifact": "acmeinc/dev-environment",
            "artifact_type": "vagrant.box",
            "metadata": {
                "provider": "vmware_desktop",
                "version": "0.0.1"
            }
        },
        {
            "type": "atlas",
            "only": ["virtualbox-iso"],
            "artifact": "acmeinc/dev-environment",
            "artifact_type": "vagrant.box",
            "metadata": {
                "provider": "virtualbox",
                "version": "0.0.1"
            }
        }]
    ]

