---
title: "Terraform Variables and Configuration"
---

## Terraform Variables and Configuration

There are two ways to configure Terraform runs in Atlas – with
Terraform Variables or Environment Variables.

## Terraform Variables

Terraform variables are first-class configuration in Terraform. They
define the parameterization of Terraform configurations and are important
for sharing and removal of sensitive secrets from version control.

Variables are sent to Atlas with `terraform push`. Any variables in
`.tfvars` files will automatically be uploaded.

Once variables are uploaded, they will only be changed by re-uploading. You
can not yet edit Terraform variables via the Atlas UI. As a workaround
for this, `TF_VAR_variable_name` environment variables can be used and
updated via the UI.

Read more about [Terraform variables](https://terraform.io/docs/configuration/variables.html).

## Environment Variables

Environment Variables allow you to set variables that will be injected
into the environment that Terraform runs in during `plan` and `apply`.

You can add, edit or delete environment variables by visiting the
Variables item in the menu of an [environment](/help/glossary#environment).

### Security

Terraform variables and environment variables are encrypted within Atlas
and closely guarded. If you have questions or concerns about the safety
of your configuration, email our security team at [security@hashicorp.com](mailto:security@hashicorp.com).
