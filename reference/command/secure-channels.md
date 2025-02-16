---
description: >-
  Ockam Secure Channels are mutually authenticated and end-to-end encrypted
  messaging channels that guarantee data authenticity, integrity, and
  confidentiality.
---

# Secure Channels

Now that we understand the basics of Nodes, Workers, and Routing ... let's create our first encrypted secure channel.

Establishing a secure channel requires establishing a shared secret key between the two entities that wish to communicate securely. This is usually achieved using a cryptographic key agreement protocol to safely derive a shared secret without transporting it over the network. In Ockam, we currently have support for two different key agreement protocols - one based on the Noise Protocol Framework and another based on Signal's X3DH design.

```shell-session
ockam identity create blue
ockam node create blue --identity blue

ockam identity create green
ockam node create green --identity green

ockam secure-channel-listener create l --at blue --identity blue --authorized-identifiers $(ockam identity show green)
ockam secure-channel create --from green --to /node/blue/service/l --identity green --authorized $(ockam identity show blue) \
  | ockam message send hello --from /node/green --to -/service/uppercase
```
