---
title: "What are Environments?"
---
# What are Environments?

Environments are a view of your infrastructure, containing:

- The [Terraform remote state](https://terraform.io/docs/commands/remote.html),
used to track what Terraform knows about your configured infrastructure (like
unique IDs and dependencies)
- The Terraform configuration files (`.tf`), used to manage and declare
the infrastructure
- The connection to the Consul cluster(s) representing the real time
status of the infrastructure

Environments can be configured to use any or all of these 3 components.

When configured, environments generate a view of changes made against
your infrastructure, as well as a real-time picture of the health
and status of various nodes in your infrastructure.
