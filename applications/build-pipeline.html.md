---
title: "Application Build Pipeline"
---

# Application Build Pipeline

Optionally, you can configure an application to use a build configuration
as a template for the build process. This allows operators to maintain
a single set of configuration for the build step and create similiar images
from a number of different application sources.

When properly configured, creating new applications with the same requirements
from the perspective of a developer will be as easy as selecting this template
from the list.

By default, any build configuration can be selected as a template when
creating a new application. This will automatically run builds with the
same Packer templates and associated files.

Each application has distinct builds when using a build configuration
as a template. Automatically, the latest version of the configuration
will be used, but you can optionally pin to a specific version of
configuration.

## Build Environment

When this build runs, the following variables will be injected into
the environment, along with the standard
[Packer environment variables](/help/packer/builds/build-environment#environment-variables).

- `ATLAS_APPLICATION_NAME` - This is the name of the application connected to
  the Packer build (e.g. `"myapp"`).
- `ATLAS_APPLICATION_SLUG` - This is the full name of the application connected
  to the Packer build (e.g. `"company/myapp"`).
- `ATLAS_APPLICATION_USERNAME` - This is the username associated with the
  application connected to the Packer build (e.g. `"sammy"`)
- `ATLAS_APPLICATION_VERSION` - This is the version of the application connected
  to the Packer build (e.g. `"2"`).
- `ATLAS_APPLICATION_GITHUB_BRANCH` - This is the name of the branch that the
  associated application version was ingressed from (e.g. `master`).
- `ATLAS_APPLICATION_GITHUB_COMMIT_SHA` - This is the full commit hash
  of the commit that the associated application version was ingressed from
  (e.g. `"abcd1234..."`).
- `ATLAS_APPLICATION_GITHUB_TAG` - This is the name of the tag that the
  associated application version was ingressed from (e.g. `"v0.1.0"`).

For any of the `GITHUB_` attributes, the value of the environment variable will
be the empty string (`""`) if the resource is not connected to GitHub or if the
resource was created outside of GitHub (like using `vagrant push`).
