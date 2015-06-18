---
title: "About Terraform Run Notifications"
---

<div class="alert info">
    <span class="alert-text">
        Notifications for Terraform runs is an unreleased beta feature. <a href="/help/support">Contact us</a> if you're interested in using them.
    </span>
</div>

# About Terraform Run Notifications

Atlas can send run notifications to your organization via Email, Slack, or
Webhooks. The following events are configurable:

- **Needs Confirmation** - The plan phase has succeeded, and there are changes
  that need to be confirmed before applying.
- **Confirmed** - A plan has been confirmed, and it will begin applying
  shortly.
- **Discarded** - A user in Atlas has discarded the plan.
- **Applying** - The plan has begun to apply and make changes to your
  infrastructure.
- **Applied** - The plan was applied successfully.
- **Errored** - An error has occurred during the plan or apply phase.

You can toggle notifications for each of these events on the "Integrations" tab
of an environment.
