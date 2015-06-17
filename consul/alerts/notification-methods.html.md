---
title: "Alert Notification Methods"
---
# Alert Notification Methods

Atlas currently supports three different types of notification methods.
All three are outlined below. Alert methods can be configured in the
"Integrations" tab of an environment.

## Email

An email can be set and receive alerts trigged by Atlas. Email
alerts include check status, output, as well as the
affected service or node.

To configure Email:

1. Enter the email into the "Integrations" tab of the environment in Atlas
1. Optionally, test the alert

## Slack

Alert messages can be sent to a [Slack](https://slack.com) channel. Alert
types are color coded and show a brief snippet of relevant information.

To configure Slack:

1. Log into your Slack account and [create an incoming webhook](https://my.slack.com/services/new/incoming-webhook/)
1. Enter the webhook URL into the field provided in the "Integrations" tab of the environment
1. Optionally, test the alert

## Pagerduty

[Pagerduty](https://www.pagerduty.com) incidents can be automatically created based on alerts
triggered by Atlas. When the alert recovers, the Pagerduty incident
is resolved by Atlas.

To configure Pagerduty:

1. Log in to your PagerDuty account
1. Visit Configuration > Services to choose an existing service API key, or to create a new one
1. Enter the service API key into the "Integrations" tab of the environment
tab of the environment in Atlas
1. Optionally, test the alert
