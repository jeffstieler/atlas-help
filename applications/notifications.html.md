---
title: "Application Notifications"
---

# Application Notifications

Atlas can send application notifications to your organization via one of our
[supported notification methods](/help/consul/alerts/notification-methods). The
following events are configurable:

- **Compile Started** - The application compilation started.
- **Compile Finished** - The application compilation completed successfully.
- **Compile Errored** - An error occured during application compilation.
- **Build Started** - The application build started.
- **Build Finished** - The application build completed successfully.
- **Build Errored** - An error occured during the application build.
- **Build Canceled** - The build was canceled by an Atlas user.

> Emails will include logs for the **Compile Finished**, **Compile Errored**,
> **Build Finished**, and **Build Errored** events.

You can toggle notifications for each of these events on the "Integrations" tab
of an application.
