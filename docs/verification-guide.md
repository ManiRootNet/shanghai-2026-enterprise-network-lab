# Verification method

The evidence was collected from the running EVE-NG lab. Each console block identifies its device, command, capture time and test phase.

## Control-plane checks

Inspect neighbor establishment, then review actual routes and advertised prefixes:

```text
show ip eigrp neighbors
show ipv6 eigrp neighbors
show ip ospf neighbor
show ip bgp summary
show bfd neighbors details
```

## Switching and gateways

Compare STP roots, HSRP roles, trunk state and LACP membership with the architecture:

```text
show spanning-tree root
show standby brief
show interfaces trunk
show etherchannel summary
```

## Endpoint tests

Generate traffic from the required client role. Check the response together with the destination, active route, NAT translation or NHRP shortcut entry. The selected policy batch covers four roles at three sites against three destinations.

## Recovery and persistence

Restore temporary test interfaces, access VLANs and endpoint roles. Verify service state, save configurations and compare running/startup content. The published summary reports these checks without exposing credentials or complete configurations.

The architecture image is an original overview. The workspace screenshot is a live EVE-NG view; console evidence is exported text. SHA-256 hashes identify the corresponding published evidence files.
