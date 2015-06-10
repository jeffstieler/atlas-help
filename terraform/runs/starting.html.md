---
title: "Starting Terraform Runs in Atlas"
---

## Starting Terraform Runs in Atlas

You can start a Terraform run (plan and subsequent apply) in two ways: `terraform push`
to upload the configuration and directory or via a GitHub connection that retrieves
the contents of a repository after changes to the default branch (usually
master).

### Terraform Push

Terraform `push` is a [Terraform command](https://terraform.io/docs/commands/push.html)
that packages and uploads a set of Terraform configuration and directory to Atlas. This then creates a run
in Atlas, which performs `terraform plan` and `terraform apply` against the uploaded
configuration.

The directory is included in order to run any associated provisioners,
that might use local files. For example, a remote-exec provsioner
that executes a shell script.

By default, everything in your directory is uploaded as part of the push.

However, it's not always the case that the entire directory should be uploaded. Often,
temporary or cache directories and files like `.git`, `.tmp` will be included by default. This
can cause Atlas to fail at certain sizes and should be avoided. You can
specify [exclusions](https://terraform.io/docs/commands/push.html) to avoid this situation.

Terraform also allows for a [VCS option](https://terraform.io/docs/commands/push.html#_vcs_true)
that will detect your VCS (if there is one) and only upload the files that are tracked by the VCS. This is
useful for automatically excluding ignored files. In a VCS like git, this
basically does a `git ls-files`.


### GitHub Import

Optionally, GitHub can be used to import Terraform configuration,
automatically queuing runs when changes are merged into the default branch
or plans when a PR is made.

When used within an organization, this can be extremely valuable for keeping
differences in environments and last mile changes from occuring before an
upload to Atlas.

This works by first connecting your [Environment]() to the target
GitHub repository and then pushing changes. Currently, an environment
must already exist to be connected to Github. You can create the environment
with `terraform push`, detailed above, and then link it to GitHub.

