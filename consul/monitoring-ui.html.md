---
title: "Consul Monitoring UI"
---

# Consul Monitoring UI

The Consul monitoring UI in Atlas provides an interface to view
nodes, services, and health across datacenters. Organizations in Atlas
can tightly control access to this interface.

This can be enabled with the `-atlas` flag.

    $ consul agent -atlas acmeinc/infrastructure

Read more in the [Consul documentation](https://consul.io/docs/agent/options.html#_atlas).
