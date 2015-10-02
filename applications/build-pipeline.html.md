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

When this build runs, the following variables will be injecting into
the environment, along with the standard
[Packer environment variables](/help/packer/builds/build-environment#environment-variables).

- `ATLAS_APPLICATION_VERSION`: The version of the application uploaded to Atlas, i.e `5`
- `ATLAS_APPLICATION_USERNAME`: The username of the application owner
- `ATLAS_APPLICATION_NAME`: The name of the application
- `ATLAS_APPLICATION_SLUG`: Both the username and the name separated by a forward slash, i.e `acmeinc/webapp`
