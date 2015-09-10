---
title: "Uploading Applications to Atlas"
---

# Uploading Applications to Atlas

There are currently three ways to upload applications to Atlas. We recommend
using the GitHub integration to allow transparency on a per-commit
basis of what was changed, but both Vagrant Push and the `atlas-upload-cli`
will work for storing versions of the application.

## GitHub

After you have [connected your GitHub account to Atlas](/settings/connections),
you can visit the integrations tab of your application and enter the username
and name of the repository. It will be linked to the application, and from
that point forward any commits to the default branch will automatically
be ingressed into Atlas and stored, along with references to the GitHub
commits and authorship information.

After each commit the application version will automatically compile. If
automatic builds are enabled, successful compiles will also trigger
a machine image build and optionally a deploy with Terraform with the
built artifact, i.e AMIs.

## Vagrant Push

Vagrant can be configured to push new versions of the application
when a user runs `vagrant push`. To configure Vagrant push, place the
following configuration in your `Vagrantfile`.

    config.push.define "atlas" do |push|
      push.app = "acmeinc/webapp"
    end

After running the `vagrant push` command, Vagrant will archive upload
the relative directory to the application and queue a compile and
potentially build.

Read more about Vagrant push in the [Vagrant documentation](https://docs.vagrantup.com/v2/push/atlas.html).

## Upload CLI

The `atlas-upload-cli` utility can be used to package a directory
and send it to Atlas. This can be performed in a CI, on a developer machine
or anywhere else the binary can run. It requires passing both the username/name
for the application and the local path to upload.

    atlas-upload acmeinc/webapp my-app/

For more info, see the [GitHub repository](https://github.com/hashicorp/atlas-upload-cli).

