---
title: "Packer Build Environment"
---

# Packer Build Environment

This page outlines the environment that Packer runs in within Atlas.

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
and the application from the [build pipeline](/help/applications/build-pipeline) are available on the filesystem
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

The total size of all files in the package being uploaded via
[Packer push or GitHub](/help/packer/builds/starting) must be 5 GB or less.

If you need to upload objects that are larger, such as dmgs, see the
[`packer push` "Limits" documentation](https://packer.io/docs/command-line/push.html)
for ways around this limitation.

### Hardware Limitations

Currently, each builder defined in the Packer template receives
the following hardware resources. This is subject to change.

- 1 GB of memory
- 20 GBs of disk space

If this doesn't suit your needs, please [contact us](mailto:support@hashicorp.com).

### Environment Variables

You can set any number of environment variables that will be injected
into your build environment at runtime. These variables can be
used to configure your build with secrets or other key value configuration.

Variables are encrypted and stored securely.

During each Packer build, the following environment variables are available as
part of the build:

- `ATLAS_BUILD_CONFIGURATION_VERSION` - the version of the
[build configuration](/help/glossary) version used during this build.
- `ATLAS_BUILD_ID` - a unique identifier for the Packer build.
- `ATLAS_BUILD_NUMBER` - the version number of the build. A build is the
connection between the application and build configuration.
- `ATLAS_TOKEN` - a unique token that can communicate with Atlas for the
duration of this build. This token will expire upon completion of the build.
This token is used as part of any Atlas-specific providers or post processors.

If the build was triggered by a new application verison, the following environment
variables are also available:

- `ATLAS_APPLICATION_NAME` - the name of the application connected to the Packer build.
For example, `logstream`
- `ATLAS_APPLICATION_SLUG` - the full name of the application connected to the Packer
build. For example, `hashicorp/logstream`.
- `ATLAS_APPLICATION_USERNAME` - the username associated with the application
connected to the Packer build. For example, `hashicorp`.
- `ATLAS_APPLICATION_VERSION` - the version of the application connected to the
Packer build. For example, `2`.


### Base Artifact Variable Injection

<div class="alert-infos">
  <div class="alert-info">
    This is an unreleased beta feature. Please <a href="/help/support">contact support</a>
    if you are interested in helping us test this feature.
  </div>
</div>

A base artifact can be selected on the "Settings" page for a build configuration.
During each build, the latest artifact version will have it's external
ID (such as an AMI for AWS) injected as an environment variable for the
environment.

The keys for the following artifact types will be injected:

- `aws.ami`: `ATLAS_BASE_ARTIFACT_AWS_AMI_ID`
- `amazon.ami`: `ATLAS_BASE_ARTIFACT_AMAZON_AMI_ID`
- `amazon.image`: `ATLAS_BASE_ARTIFACT_AMAZON_IMAGE_ID`

You can then reference this artifact in your Packer template, like this
AWS example:

    {
      "variables": {
          "base_ami": "{{env `ATLAS_BASE_ARTIFACT_AWS_AMI_ID`}}"
      },
      "builders": [
        {
          "type": "amazon-ebs",
          "access_key": "",
          "secret_key": "",
          "region": "us-east-1",
          "source_ami": "{{user `base_ami`}}"
        }
      ]
    }

- - -

## Notes on Security

Packer environment variables in Atlas are encrypted using [Vault](https://vaultproject.io)
and closely guarded and audited. If you have questions or concerns
about the safety of your configuration, please contact our security team
at [security@hashicorp.com](mailto:security@hashicorp.com).
