---
title: "SCADA in Atlas"
---
## SCADA in Atlas

[SCADA](https://scada.hashicorp.com) is a service to allow tools to
integrate with Atlas. SCADA stands for Supervisory Control And Data
Acquisition, and as the name implies it allows Atlas to provide control
functions and request data from the tools that integrate. Using SCADA is
completely optional and requires an opt-in with every tool that supports
it.

For example, when SCADA integration is enabled in Consul the Atlas Web
UI can be used to inspect the current cluster state. Providing the
Consul dashboard is done by means of data acquisition from the connected
instances. Optionally, Consul can also perform an auto-join to other
members of it's cluster. This is done by informing the SCADA system that
auto-join should be enabled allowing Atlas to orchestrate the cluster
joins. This is done by means of supervisory control of the connected
instances.

The technical details about how SCADA works are fairly simple. Clients
first open a connection to the SCADA service at scada.hashicorp.com on
port 7223. This connection is secured by TLS, allowing clients to verify
the identity of the servers and to encrypt all communications. Once
connected, a handshake is performed where a client provides it's Atlas
API credentials so that Atlas can verify the client identity. Once
complete, clients keep the connection open in an idle state waiting for
commands to be received. Commands map to APIs exposed by the product,
and are subject to any ACLs, authentication or authorization mechanisms
of the client. More specific details are available in the product
documentation.

