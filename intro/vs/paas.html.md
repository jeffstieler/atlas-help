---
title: "Atlas vs. Heroku and other PaaS"
---

## Atlas vs. Heroku and other PaaS

PaaS, like Heroku, typically manage the entire application and
service stack within their own infrastructure. This means
creating services on a PaaS is very low effort.

However, as infrastructure grows in complexity, a PaaS may
become too opinionated to handle new business requirements. At this
stage, you must either bend your application to fit with a PaaS or
move off of it.

Atlas attempts to bridge this gap and is focused on the workflow of
deployment and infrastructure management, rather than where applications
run. For example, Terraform can manage Heroku resources and combine them
with AWS compute.

Depending on the legacy requirements, cost structures, and service availability,
a PaaS may be too simple for some applications. In this case, Atlas
can bring a similar developer experience to lower-level service
and infrastructure providers.

Atlas is built on the open source HashiCorp toolset, so configurations
can be taken out of Atlas and still function in different environments. In
this way, Atlas avoids lock-in, typically a problem with PaaS providers.
