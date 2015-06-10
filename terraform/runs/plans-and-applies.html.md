---
title: "Plans and Applies"
---
# Plans and Applies

When a new run is created, Atlas automatically starts a plan. A plan does
not actively change infrastructure and can be run many times without
issue. Applies are the only part of the run that actively changes
infrastructure, and requires operator confirmation.

## Plan

Terraform `plan` is a command is used to create an execution plan.
Terraform performs a refresh and then determines what actions are necessary to
achieve the desired state specified in the configuration files. This generates
a plan file that is persisted and used in the subsequent apply.

## Apply

Terraform `apply` is a command in Terraform that is used to
apply the changes required to reach the desired state of the
configuration. This can result in infrastructure being changed on the
remote provider.


