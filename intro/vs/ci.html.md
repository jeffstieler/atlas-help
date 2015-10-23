---
title: "Atlas vs. CI"
---

# Atlas vs. CI

Continuous integration is the process of testing and building code on a regular
basis to make sure problems are detected before they make it to production.

Atlas can run tests and builds with Packer, however Atlas also works with
existing CI workflows. After tests pass successfully, the tested code can be
uploaded to Atlas with the [Atlas upload CLI](https://github.com/hashicorp/atlas-upload-cli).
Or Atlas can be [setup to ingest code](https://atlas.hashicorp.com/help/applications/uploading)
only once it has been merged into the master branch on GitHub. Many teams will test pull
requests in a CI tool before merging them into the master branch.
