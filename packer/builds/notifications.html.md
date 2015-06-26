---
title: "About Packer Build Notifications"
---

<div class="alert info">
    <span class="alert-text">
        Notifications for Packer builds is an unreleased beta feature. <a href="/help/support">Contact us</a> if you're interested in using them.
    </span>
</div>

# About Packer Build Notifications

Atlas can send build notifications to your organization via Email, Slack, or
Webhooks. The following events are configurable:

- **Starting** - The build has begun.
- **Finished** - All build jobs have finished successfully.
- **Errored** - An error has occurred during one of the build jobs.
- **Canceled** - A user in Atlas has canceled the build.

You can toggle notifications for each of these events on the "Integrations" tab
of a build configuration.
