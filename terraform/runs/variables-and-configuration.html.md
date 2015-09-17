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

## Managing Secret Multi-Line Files

Atlas has the ability store multi-line files as variables. The recommended way to manage your secret/sensitive multi-line files (SSL keys, certificates, etc.) is to add them as [Terraform Variables](#terraform-variables) in Atlas.

Just like secret strings, it is recommended that you never check-in these multi-line secret files to version control. Best practice is setting a blank [variable in Terraform](https://www.terraform.io/docs/configuration/variables.html) that resources utilizing the file will reference, `terraform push` to Atlas, navigate to the "Variables" section of your Atlas Environment, paste the contents of that file into the variable and save.

Now, any resource that consumes that variable will have access to the file without having to check it in to version control. If you want to run Terraform locally, that file will still need to be passed in as a variable. View the [Terraform Variable Documentation](https://www.terraform.io/docs/configuration/variables.html) for different ways to accomplish this.

A few things to note...

- [Environment Variables](#environment-variables) do not support multi-line files
- The `.tfvars` file does not support multi-line files
- You can still use `.tfvars` to define your blank variable, however, you will not be able to actually set the variable in `.tfvars` with the multi-line file contents like you would a variable in a `.tf` file

- - -

## Notes on Security

Terraform variables and environment variables in Atlas are encrypted using
[Vault](https://vaultproject.io) and closely guarded and audited. If you have
questions or concerns about the safety of your configuration, please contact
our security team at [security@hashicorp.com](mailto:security@hashicorp.com).
