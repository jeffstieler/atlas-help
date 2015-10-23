---
title: "Atlas vs. HashiCorp Tools"
---

# Atlas vs. HashiCorp Tools

HashiCorp tools are the functional foundation for Atlas. Packer is used
to build images, Terraform is used to provision infrastructure, and Consul
is used to monitor and maintain services and nodes.

Atlas unites the open source tools to provide an
automated solution for application delivery. When an application connected
to Atlas pushes a new version, it automatically triggers a Packer build which produces
a deployable artifact. The artifact is stored in Atlas's artifact registry.
When the artifact is successfully stored in Atlas, it automatically triggers a Terraform run, which
creates a new host with the Packer-built artifact. Consul is configured in the
build stage with Packer, so when the new host is provisioned, it automatically
joins the cluster. Each step in this workflow is versioned, auditable, and repeatable.
Atlas can be thought of as the management hub which enables teams to
collaborate across all HashiCorp tooling and automate the workflow from
development to production.
