# Evidence index

These are selected outputs from the running lab, captured on 25 October 2026. Device names and UTC capture times accompany the records. Commands that configure the solution and all credentials have been excluded.

| File | What to inspect |
| --- | --- |
| [Routing](01-routing.txt) | EIGRP/BGP/OSPF neighbors, actual BGP exports, and BFD session details |
| [Switching](02-switching.txt) | Final STP roots, HSRP roles, trunks, and LACP members |
| [Services](03-services.txt) | NTP status for all managed devices, DHCP bindings, and restored endpoint addresses |
| [Policy probes](04-policy-tests.txt) | 36 site/VLAN/destination tests with positive or explicit deny responses |
| [Policy results](policy-results.json) | Machine-readable expected/observed policy outcomes |
| [Failure tests](05-failure-tests.txt) | Successful alternate paths, recovery state, and observed failures |
| [DMVPN](06-dmvpn.txt) | Direct remote branch NBMA mappings and NHRP shortcut routes |
| [SSH](07-ssh.txt) | Authenticated privileged access from MGMT and refusal from another network |
| [Open findings](08-open-findings.txt) | Reproductions and diagnostic outputs for unresolved forwarding failures |
| [Configuration summary](configuration-summary.json) | Credential-free baseline, synchronization, persistence, and ISP preservation checks |
| [SHA-256 manifest](SHA256SUMS.txt) | Integrity checks for the published evidence files |

Text records are console exports, not independent attestation. The SHA-256 manifest detects later file changes; it does not establish authorship by itself. The [live EVE-NG screenshot](../assets/eve-topology.jpg) shows the actual workspace viewport. The [architecture overview](../assets/architecture.png) is a separately drawn explanatory diagram.
