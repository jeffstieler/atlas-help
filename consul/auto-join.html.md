---
title: "Consul Auto-Join"
---

# Consul Auto-Join

Consul can be configured to auto-join via Atlas. Atlas will track the most recent
members to join the infrastructure named by the configured`-atlas` flag and automatically
join them on start. For servers, the LAN and WAN pool are both joined.

This enables quick discovery of peers for nodes in a datacenter. Atlas
authenticates and verifies this join.

This can be enabled with the `-atlas-join` flag.

    $ consul agent -atlas acmeinc/infrastructure -atlas-join

Read more in the [Consul documentation](https://consul.io/docs/agent/options.html#_atlas_join).
