---
title: "About Applications in Atlas"
---

# About Applications in Atlas

<div class="alert-infos">
    <div class="row alert-info">
        Application deployment with Atlas is a beta feature. <a href="/help/support">Contact us</a> to use it.
    </div>
</div>

Atlas can be used to deploy applications by storing,
compiling and injecting application slugs (i.e binaries or archives)
into Packer builds in order to build any number of machine images
(i.e AMIs, containers, or Vagrant boxes) for deployment with Terraform in Atlas.

Applications can be uploaded to Atlas with a CLI tool, Vagrant Push, or
automatically import code from GitHub after every commit. Learn more about
[uploading applications](/help/applications/uploading).

## Compiling Applications

Atlas will optionally compile your application prior to queuing
a build for deployment. Depending on your application, this is necessary
to separate from the build step to isolate development and compilation
dependencies from production machine images.

Additionally, it aligns compilation with a set of changes to the application,
ensuring responsibility for a failed compile is tied to a developer
or team making changes.

Learn more about [using application compilation](/help/applications/compilation).

## Triggering Builds

Following a successful compile or upload of application source, either
from GitHub or Vagrant Push, a build can automatically be triggered
to create a machine image containing the application source, along with
any other configuration set by Packer and any provisioners used.

After a successful build and artifact upload, artifacts referenced with
Terraform can be automatically triggered for deploy. Learn more
about [continuous deployment with Atlas](/help/intro/use-cases/continuous-deployment-of-immutable-infrastructure).

