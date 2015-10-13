---
title: "Debugging Noisy Alerts"
---

# Debugging Noisy Alerts

If alerts are too frequent, or "noisy", there are several strategies
for quieting them. Depending on the health check design, size
of your infrastructure, and application requirements, alerts may be expected or be a
sign of an immediate problem.

When alerts are loud, it's always worth diagnosing why prior to
turning them off – it may be a sign of issues in the underlying system.

## Lenient Health Checks

One way to lower the frequency of alerts is to make health checks
more lenient to partial or minor failures. As an example, if your
health check takes the load average of a system, it's better
to take the past five of fifteen minute load, rather than one minute.

Spikes in usage causing alerts may be a sign of important
scaling requirements of your system not being met, so leniency should only be
built into checks with this in mind.

## Health Check Retries

Occasionally a health check talks to a system that may have occasional
failures. In this case, it may be wise to implement retry logic
into the check system to immediately verify if the system is still
in a problematic state.

It's important, however, to build this same retry into your application
itself. Flapping health checks may be a sign of reliability or quality of service
issues that need to be handled at the application level.
