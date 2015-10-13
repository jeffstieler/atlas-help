---
title: "Alert Notification Methods"
---

# Alert Notification Methods

Atlas currently supports many different types of notification methods, outlined
below.

Notification methods can be managed by visiting the **Configuration** page for
your user or organization. Notification methods can also be overridden for a
specific build configuration, environment, or infrastructure.

## Email

An email can be set and receive alerts trigged by Atlas. Email
alerts include check status, output, as well as the
affected service or node.

To configure Email notifications:

1. Enter the email into the "Integrations" tab of the environment in Atlas
1. Optionally, test the alert

## HipChat

Notifications can be sent to a [HipChat](https://hipchat.com) room. There are
two ways to configure HipChat notifications:

### User Account

This API token can post to any room that the user account has access to, but
will be displayed as that user's name. You may want to create an "Atlas" user.

1. In your **Account Settings**, click [API
   Access](https://hipchat.com/account/api).
1. Enter a label for the new token, such as "Atlas".
1. Ensure the **Send Notification** scope is selected.
1. Click **Create**, and then copy the token from the confirmation page into
   your Atlas notification methods.

### Group Integration

The API token generated here will only have access to the room you chose during
creation, but you can customize the display name. You may want to create a
Group Integration for each room you intend to post to.

1. Create a [new integration](https://hipchat.com/admin/byo) for your HipChat
   group.
1. Select the room that this integration should post messages to.
1. Choose a name for the integration, such as "Atlas". This will be the
   username that messages are posted as.
1. Click **Create**, and then copy the token from the examples on the next page
   into your Atlas notification methods.

## Slack

Alert messages can be sent to a [Slack](https://slack.com) channel. Alert
types are color coded and show a brief snippet of relevant information.

To configure Slack:

1. Log into your Slack account and [create an incoming webhook](https://my.slack.com/services/new/incoming-webhook/)
1. Enter the webhook URL into the field provided in the "Integrations" tab of the environment
1. Optionally, test the alert

## PagerDuty

[PagerDuty](https://www.pagerduty.com) incidents can be automatically created
based on Consul Alerts triggered by Atlas. When the alert recovers, the
PagerDuty incident is resolved by Atlas.

> Only Consul Alerts are sent to PagerDuty

To configure PagerDuty:

1. Log in to your PagerDuty account
1. Visit **Configuration > Services** to choose an existing service API key, or
   to create a new one
1. Enter the service API key into the "Integrations" tab of the environment tab
   of the environment in Atlas
1. Optionally, test the alert.
