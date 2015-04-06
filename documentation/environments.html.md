---
title: "What are Environments?"
---
## What are Environments?

Environments show the real-time status of your infrastructure,
any pending changes, and its change history.

Real-time infrastructure status is powered by
[Consul](https://consul.io), a HashiCorp tool for service
discovery, service registry, health checks, and monitoring.
Setting the [`-atlas` flag](https://consul.io/docs/guides/atlas.html)
in your Consul configuration connects your Consul cluster with Atlas. This
enables Atlas to display the health of all the nodes and services
in your infrastructure.

Infrastructure changes are powered by [Terraform](https://terraform.io),
a HashiCorp tool for launching, combining, and versioning infrastructure.
[Terraform remote state](https://terraform.io/docs/commands/remote.html)
enables Terraform to be run remotely by Atlas. All infrastructure changes
are stored and versioned to display an auditable history of your
infrastructure.

Environments can be configured to use any or all of the three components —
real-time status, remote changes, and change history.

To learn about the internals of Consul and Terraform in greater detail,
visit the [Consul Documentation](https://consul.io/docs) and
[Terraform Documentation](https://terraform.io/docs).
