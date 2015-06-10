---
title: "Linked Applications"
---

## Linked Applications

You can link applications to a build to automatically
include the source of the application in the environment that Packer runs.

This can be used to create an image with application code embedded upon
changes to the application. Some use this as part of a
[continuous deployment](/help/intro/use-cases/continuous-deployment-of-immutable-infrastructure)
workflow.

You can link any number of applications to builds in
order to make those files available in the build environment.

### Linking an Application

To link an application, visit the build and click the "Links" item
in the sidebar.

This requires the following information:

- __Application Username__: The username of the application you are linking. Your
account must have access to this application to link it
- __Application Name__: The name of the application you are linking
- __Path__: The path to inject the application. When a new build is run,
the application files are placed at this path in the environment Packer
is run

Once an application is linked, you may need to [start a build](/help/packer/builds/starting).

### Moving Files to a Target Image

Linked applications are copied into the Packer build environment
at the path specified while linking. This may end up looking something
like this:

    .packer-template
    LICENSE
    http/
    http/preseed.cfg
    scripts/
    scripts/base.sh
    scripts/cleanup.sh
    scripts/dep.sh
    scripts/vagrant.sh
    scripts/virtualbox.sh
    scripts/vmware.sh
    scripts/zerodisk.sh
    template.json
    webapp/config.ru
    webapp/routes/index.rb
    webapp/views/index.html.erb

In this example, the application is linked to the `webapp` path. Packer
provisioners can now access these files at that path.

A typical workflow includes reading the file from these
locations from the Packer environment and copying them to the target image
using Packer provisioners.

In the above example, you may just want to copy the Ruby application
directly onto the target:

    "provisioners": [
        {
            "type": "file",
            "source": "webapp",
            "destination": "/srv/web"
        }
    ]

Read the [Packer file provisioner documentation](https://packer.io/docs/provisioners/file.html)
for more on using the file provisioner, and caveats for directory provisioning.

Additionally, you can read more about the [Packer build environment](/help/packer/builds/build-environment).
