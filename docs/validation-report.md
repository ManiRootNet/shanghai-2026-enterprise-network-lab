# Selected validation report

Recorded on 25 October 2026 through live EVE-NG node consoles. The results below identify the tested traffic, condition and observed outcome.

## Access policy: 36/36 checks

Four client roles were exercised at HQ, Branch 1 and Branch 2, against SVR1, SVR2 and the simulated Internet. Temporary endpoint roles were restored after collection.

| Role | SVR1 | SVR2 | Simulated Internet |
| --- | --- | --- | --- |
| Management | Allow | Allow | Deny |
| CCTV | Deny | Allow | Deny |
| WLAN | Allow | Allow | Allow |
| Corporate | Allow | Allow | Allow |

All 36 observations matched the expected policy. Deny decisions returned administrative-prohibition responses. [Console records](../evidence/04-policy-tests.txt) · [Machine-readable results](../evidence/policy-results.json)

## Routing and alternate paths

| Controlled test | Observed evidence |
| --- | --- |
| Direct HQ–DC link disabled | PC1 and PC4 each received 5/5 replies from SVR1 |
| Primary Internet exit disabled | WLAN received 5/5 replies through the secondary exit, with matching PAT translations |
| Exit restored | Primary route and corresponding translations returned |
| One LACP member unavailable | UDLD isolated the affected member; the surviving member carried 5/5 PC1-to-SVR1 replies |
| DC Vlan201 gateway SVI unavailable | Alternate-gateway server/client probes returned 3/3 replies |

See the [selected resilience records](../evidence/05-resilience-tests.txt). Each record includes the test condition, device and capture time.

## DMVPN and services

Direct branch traffic was checked against dynamic remote-branch NBMA mappings and installed NHRP shortcut routes. The branch WAN underlay uses dynamic reachability through the practice ISP. [DMVPN evidence](../evidence/06-dmvpn.txt)

DHCP bindings include PC1's corporate reservation and client leases. NTP is synchronized on all 15 managed devices. The saved-state summary compares running/startup configurations on all 16 routers/switches. [Services](../evidence/03-services.txt) · [Saved-state summary](../evidence/configuration-summary.json)

Management-source SSH authentication succeeded with privilege 15; a source outside the management networks was refused. [SSH evidence](../evidence/07-ssh.txt)

## BFD timing method

An incoming test filter interrupted BFD control packets on the direct HQ/DC link. A router-clock sample immediately before filter application and the BFD-triggered BGP-down event use the same IOS clock, with CST/UTC display accounted for. The conservative elapsed upper bound was 408 ms. The filter was removed and the BFD session returned Up.

This is a control-plane detection measurement. [Timestamp record](../evidence/09-bfd-timing.json)
