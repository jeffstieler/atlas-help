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

You can also read on to learn more about how Packer uploads and versions
the boxes with post-processors.

## Post-Processors

Packer uses [post-processors]() to define how to process
images and artifacts after provisioning. Both the `vagrant` and `atlas` post-processors must be used in order
to upload Vagrant Boxes to Atlas via Packer.

It's important that they are [sequenced]() in the Packer template so
they run in order. This is done by nesting arrays:

    "post-processors": [
        [
            {
                "type": "vagrant"
                ...
            },
            {
                "type": "atlas"
                ...
            }
        ]
    ]

Sequencing automatically passes the resulting artifact from one
post-processor to the next – in this case, the `.box` file.

### Vagrant Post-Processor

The [Vagrant post-processor]() is required to package the image
from the build (an `.ovf` file, for example) into a `.box` file before
passing it to the `atlas` post-processor.

    {
        "type": "vagrant",
        "keep_input_artifact": false
    }

The input artifact (i.e and `.ovf` file) does not need to be kept when building Vagrant Boxes,
as the resulting `.box` will contain it.

### Atlas Post-Processor

The [Atlas post-processor]() takes the resulting `.box` file and uploads
it to Atlas, adding metadata about the box version.

    {
        "type": "atlas",
        "artifact": "acmeinc/dev-environment",
        "artifact_type": "vagrant.box",
        "metadata": {
            "provider": "vmware_desktop",
            "version": "0.0.1"
        }
    }

#### Attributes Required

These are all of the attributes for that Atlas post-processor
required for uploading Vagrant Boxes. A complete example is shown below.

- `artifact`: The username and box name (`username/name`) you're creating the version
of the box under. If the box doesn't exist, it will be automatically
created
- `artifact_type`: This must be `vagrant.box`. Atlas uses this to determine
how to treat this artifact.

For `vagrant.box` type artifacts, Atlas also requires two keys:

- `provider`: The Vagrant provider for the box. Common providers are
`virtualbox`, `vmware`, `aws` and so on
- `metadata`: This is the Vagrant box [version]() and is constrained to the
same formatting as in the web UI: `[0-9].[0-9].[0-9]`

## Example

An example post-processor block for Atlas and Vagrant is below. In this example,
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
