---
title: "Atlas vs. AWS, GCE, Azure and Other Infrastructure Providers"
---

# Atlas vs. AWS, GCE, Azure and Other Infrastructure Providers

AWS, GCE and Azure, among others, often offer infrastructure
management solutions within their own systems. These tools
can be used when all infrastructure exists inside of that specific
provider, but are often designed without portability in mind.

Organizations often have complex requirements or need for infrastructure
provider changes that cause important workflows to be lost while moving.
Atlas provides a consistent workflow that still leverages toolsets inside
of each unique infrastructure provider, but applies a layer of abstraction
to allow for easy lateral movement between providers.

This is seen largely in the [Terraform](/help/terraform/features) tool, which
is primarily designed to launch and manage infrastructure _across_
different providers. Combining the best features from all providers
enables organizations to leverage strengths and adapt to legacy
requirements, without fracturing workflows.
