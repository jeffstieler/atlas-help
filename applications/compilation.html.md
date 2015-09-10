---
title: "Application Compilation in Atlas"
---

# Application Compilation in Atlas

Atlas can compile an uploaded version of an application for deployment
by injecting the compiled artifact into the environment of a Packer
build, allowing provisioners to move the application artifact
onto the filesystem of the target machine image.

This is a separate step from the build step handled by Packer primarily
in order to avoid compilation and development dependencies being installed
on a production image, as well as placing the compilation responsibility
on the application developer and those responsible or the changes
to the application.

In order to compile an application, compilation must be enabled in the
applications settings and a compile template must be included alongside
the application source.

## Compile Templates

Compile templates are simply Packer templates with a specific set
of post-processors, with no restrictions to what builders
or provisioners are used. Currently, compile templates must contain
a single builder.

Because compilations are performed by Packer templates, the environment
and tools used to perform the compilation is extremely flexible, allowing
any platforms, OSes, dependencies that [Packer and Atlas support](/help/packer/builds/build-environment#supported-builders)
to be used.

### Choosing a Build Environment

Depending on what type of application is being compiled, you can select
the Packer build to use by specifying it in the `builders` stanza. The
example below uses Docker with an Ubuntu image, allowing us to compile
in the Ubuntu operating system without waiting for the slow startup
of a virtual machine.

### Variables

There a several variables available in the compile environment
that can be used to reference artifacts, configure compilation or
name the resulting archives created. This can help ease sharing
of compile templates and remove special casing from each template.

- `ATLAS_APPLICATION_VERSION`: The version of the application uploaded to Atlas, i.e `5`
- `ATLAS_APPLICATION_USERNAME`: The username of the application owner
- `ATLAS_APPLICATION_NAME`: The name of the application
- `ATLAS_APPLICATION_SLUG`: Both the username and the name separated by a forward slash, i.e `acmeinc/webapp`

### Post-Processors

There are two required post-processors for compile templates. The first,
the `artifice` post-processor, selects a file and passes it to the
`atlas` post-processor which uploads the compiled archive to Atlas,
allowing it to be downloaded later during a build.

This archive needs to be downloaded from the builder environment where
the compile occured to the local environment where Packer is running. This
is demonstrated below.

    {
      "type": "file",
      "source": "/tmp/compiled-app.tar.gz",
      "destination": "compiled-app.tar.gz",
      "direction": "download"
    }

The artifact can be stored as any type or under any artifact in Atlas,
as long as it is accessible later by the same user triggering builds
that use the artifact.

### Complete Example

This template is a working example for a project that installs and
compiles the application using a `Makefile` and outputs
a `.tar.gz` archive of the compiled application. It then uploads
the archive to the artifact in Atlas matching the name of the application,
as it uses the `ATLAS_APPLICATION_SLUG` environment variable, i.e `acmeinc/webapp`.

    {
      "variables": {
        "app_slug": "{{ env `ATLAS_APPLICATION_SLUG` }}"
      },
      "builders": [
        {
          "type": "docker",
          "image": "ubuntu:14.04",
          "commit": true
        }
      ],
      "provisioners": [
        {
          "type": "shell",
          "inline": [
            "apt-get -y update"
          ]
        },
        {
          "type": "file",
          "source": ".",
          "destination": "/tmp/app"
        },
        {
          "type": "shell",
          "inline": [
            "cd /tmp/app",
            "make"
          ]
        },
        {
          "type": "file",
          "source": "/tmp/compiled-app.tar.gz",
          "destination": "compiled-app.tar.gz",
          "direction": "download"
        }
      ],
      "post-processors": [
        [
          {
            "type": "artifice",
            "files": ["compiled-app.tar.gz"]
          },
          {
            "type": "atlas",
            "artifact": "{{user `app_slug` }}",
            "artifact_type": "archive"
          }
        ]
      ]
    }
