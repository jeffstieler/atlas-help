---
title: "Box Versioning and Lifecycle"
---
# Box Versioning and Lifecycle

Boxes support versioning so that members of your team using Vagrant can
update the underlying box easily, and the people who create boxes can
push fixes and communicate these fixes efficiently.

There are multiple components of a box:

- The box itself, comprised of the box name and description.
- One or more box versions.
- One or more providers for each box version.

## Box Version Release States

Atlas lets you create new versions of boxes without
releasing them or without Vagrant seeing the update. This lets you prepare
a box for release slowly. Box versions have three states:

- `unreleased`: Vagrant cannot see this version yet, so it needs
to be released.  Versions can be released by editing them and clicking
the release button at the top of the page
- `active`: Vagrant is able to add and use this box version
- `revoked`: Vagrant cannot see this version, and it cannot be re-released.
You must create the version again

### Release Requirements

A box can only be released if it has at least one of each component: a
box, a version, and a provider.
