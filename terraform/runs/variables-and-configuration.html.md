---
title: "Terraform Variables and Configuration"
---

# Terraform Variables and Configuration

There are two ways to configure Terraform runs in Atlas – with
Terraform variables or environment variables.

## Terraform Variables

Terraform variables are first-class configuration in Terraform. They
define the parameterization of Terraform configurations and are important
for sharing and removal of sensitive secrets from version control.

Variables are sent to Atlas with `terraform push`. Any variables in your local
`.tfvars` files are securely uploaded to Atlas. Once variables are uploaded to
Atlas, Terraform will prefer the Atlas-stored variables over any changes you
make locally. Please refer to the
[Terraform push documentation](https://www.terraform.io/docs/commands/push.html)
for more information.

You can also add, edit, and delete Terraform variables via Atlas. To update
Terraform variables in Atlas, visit the "variables" page on your
[environment](/help/glossary#environment).

For detailed information about Terraform variables, please read the
[Terraform variables](https://terraform.io/docs/configuration/variables.html)
section of the Terraform documentation.

## Environment Variables

Environment variables are injected into the virtual environment that Terraform
executes in during the `plan` and `apply` phases.

You can add, edit, and delete environment variables from the "variables" page
on your [environment](/help/glossary#environment).

Additionally, the following environment variables are automatically injected by
Atlas. All Atlas-injected environment variables will be prefixed with `ATLAS_`

- `ATLAS_TOKEN` - This is a unique, per-run token that expires at the end of
  run execution (e.g. `"abcd.atlasv1.ghjkl..."`).
- `ATLAS_RUN_ID` - This is a unique identifier for this run (e.g. `"33"`).
- `ATLAS_CONFIGURATION_NAME` - This is the name of the configuration used in
  this run. Unless you have configured it differently, this will also be the
  name of the environment (e.g `"production"`).
- `ATLAS_CONFIGURATION_SLUG` - This is the full slug of the configuration used
  in this run. Unless you have configured it differently, this will also be the
  name of the environment (e.g. `"company/production"`).
- `ATLAS_CONFIGURATION_VERSION` - This is the unique, auto-incrementing version
  for the Terraform configuration (e.g. `"34"`).
- `ATLAS_CONFIGURATION_VERSION_GITHUB_BRANCH` - This is the name of the branch
  that the associated Terraform configuration version was ingressed from
  (e.g. `master`).
- `ATLAS_CONFIGURATION_VERSION_GITHUB_COMMIT_SHA` - This is the full commit hash
  of the commit that the associated Terraform configuration version was
  ingressed from (e.g. `"abcd1234..."`).
- `ATLAS_CONFIGURATION_VERSION_GITHUB_TAG` - This is the name of the tag
  that the associated Terraform configuration version was ingressed from
  (e.g. `"v0.1.0"`).

For any of the `GITHUB_` attributes, the value of the environment variable will
be the empty string (`""`) if the resource is not connected to GitHub or if the
resource was created outside of GitHub (like using `terraform push`).

- - -

## Notes on Security

Terraform variables and environment variables in Atlas are encrypted using
[Vault](https://vaultproject.io) and closely guarded and audited. If you have
questions or concerns about the safety of your configuration, please contact
our security team at [security@hashicorp.com](mailto:security@hashicorp.com).
