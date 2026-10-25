# Validation report

**Audit date:** 25 October 2026. **Method:** live console inspection, configuration review, endpoint traffic, and controlled failure tests. **Scope:** 15 managed Cisco devices, a read-only ISP baseline, and six VPCS endpoint roles.

The supplied workbook contains 58 Module C aspects with 25 available marks. Every aspect is mapped in the [requirements map](requirements-map.md). This is a self-audit against that material, not an official assessor result. Configuration evidence, data-plane verification, unresolved failures, and unsupported features are distinguished explicitly.

## Policy matrix

The outcomes below were observed at HQ, Branch 1, and Branch 2. Existing endpoints were temporarily assigned to additional VLAN roles for the tests, then returned to their intended access ports and addresses.

| Client role | SVR1 | SVR2 | Simulated Internet |
| --- | --- | --- | --- |
| Management | Allowed | Allowed | Denied |
| CCTV | Denied | Allowed | Denied |
| WLAN | Allowed | Allowed | Allowed |
| Corporate | Allowed | Allowed | Allowed |

The negative CCTV and management tests returned administrative-prohibition responses. DHCP leases were acquired separately; a client without an address was not counted as a policy pass.

## Services and routing

| Test | Observation |
| --- | --- |
| PC1 reservation | The client obtained its reserved corporate address through DHCP |
| PC2 DHCP | The WLAN client obtained an address in the configured range |
| Branch CCTV DHCP | Both branch scopes issued leases during the test sequence |
| NTP | All 15 managed devices synchronized; the edge routers selected the preferred ISP time source |
| EIGRP | IPv4 and IPv6 neighbors formed; route and interface settings were reviewed |
| OSPF | Point-to-point adjacencies and summary advertisements were reviewed; the default disappeared from DS3 after the ISP default was withdrawn |
| BGP exports | Actual advertisements were collected and compared with the permitted prefix sets |
| Inbound preference | With the direct HQ-DC path down, the ISP best path and server traceroute selected IR1 |
| Exit PAT | Permitted clients produced translations from the pool associated with the active exit |
| Conditional PC4 NAT | SVR1 traffic produced the required mapping at each exit; SVR2 traffic did not produce that destination-specific translation |
| SSH | Branch management login succeeded with privilege 15; a non-management source was refused |
| Direct branch tunnel | Both remote branch NBMA addresses appeared dynamically, with installed NHRP shortcut routes |

## Failure and recovery matrix

| Fault injected | Outcome | Interpretation |
| --- | --- | --- |
| Direct IR2-IR3 link disabled | PC1 and PC4 reached SVR1, 5/5 replies each | Verified alternate-path connectivity |
| IR1 WAN disabled while direct DC link remained down | WLAN had 5/5 replies; corporate had 4/5 in the captured post-failure probe; secondary translations were recorded | Failover verified with one recorded lost corporate probe; no lossless claim |
| IR1 WAN restored | Primary path and translations returned | Recovery observed |
| IR3 ISP link disabled | The OSPF default was withdrawn from DS3 | Conditional origination verified |
| All connected DS1 interfaces isolated | DS2 assumed gateway/root roles; IPv4 to SVR1 passed 5/5 | IPv4 distribution resilience verified |
| Same DS1 isolation, IPv6 from PC1 | IPv6 probes failed despite HSRP role transition | Open finding F03 |
| DS3 upstream/inter-switch links isolated | DS4 assumed DC gateway roles; surviving SVR2 endpoint reached PC1, 5/5 | Verified for the surviving endpoint; not a claim of dual-homed servers |
| Only DS3 server SVI disabled | HSRP moved; SVR1-to-PC1 probes failed | Open finding F05 |
| LACP member disabled at both ends | Surviving member carried PC1-to-SVR1 traffic, 5/5 | Verified bilateral member outage |
| LACP member disabled at one end | Independent remote member remained; traffic probes failed for more than two minutes | Open finding F04 |

All deliberately disabled interfaces were restored. Temporary access VLANs and endpoint roles were restored before the final save. Final state evidence is linked from the [evidence index](../evidence/README.md).

## Evidence limits

Five ICMP replies demonstrate sampled connectivity, not a long-duration availability SLA. A configured BFD interval does not prove an end-to-end recovery bound. DHCP and ACL review do not prove DNS application service, because the server roles are VPCS endpoints. Functional branch shortcuts currently depend on the underlay deviation described in F02.

The [known findings](known-findings.md) remain part of the result. No percentage or perfect-score badge is derived from partially tested or unsupported requirements.
