---
title: "Atlas vs. Cloudformation, Heat, and Other Infrastructure Management"
---
## Atlas vs. Cloudformation, Heat, and Other Infrastructure Management

Tools like CloudFormation, Heat, etc. allow the details of an infrastructure
to be codified into a configuration file. The configuration files allow
the infrastructure to be elastically created, modified and destroyed.

Atlas provides similar functionality by using Terraform to change
and manage infrastructure. However, Terrraform
differs in this regard in that it goes further by being both cloud-agnostic and enabling multiple
providers and services to be combined and composed. For example, Terraform
can be used to orchestrate an AWS and OpenStack cluster simultaneously,
while enabling 3rd-party providers like CloudFlare and DNSimple to be
integrated to provide CDN and DNS services. This enables Terraform to
represent and manage the entire infrastructure with its supporting services,
instead of only the subset that exists within a single provider. It provides
a single unified syntax, instead of requiring operators to use independent
and non-interoperable tools for each platform and service.

Additionally, using Terraform inside of Atlas provides a place for collaboration
on plain text configuration, with powerful planning, auditing, and
version control integrations.

Using infrastructure management tools without an interface like Atlas
requires workflows that are typically created on a per organization
basis and often have steep learning curves. Atlas provides a consistent
and polished platform, backed by a large open source tool and community,
to begin managing infrastructure in a codified manner.

