# Evidence index

Selected live console records, captured on 25 October 2026. Device names, UTC times and test conditions accompany the outputs.

| File | Contents |
| --- | --- |
| [Routing](01-routing.txt) | Neighbors, actual BGP exports and BFD session details |
| [Switching](02-switching.txt) | STP roots, HSRP roles, trunks and LACP members |
| [Services](03-services.txt) | Clock status, DHCP bindings and endpoint addresses |
| [Policy probes](04-policy-tests.txt) | The 36 site/role/destination observations |
| [Policy results](policy-results.json) | Expected and observed outcomes in JSON |
| [Resilience](05-resilience-tests.txt) | Selected alternate-path and gateway tests |
| [DMVPN](06-dmvpn.txt) | Dynamic branch NBMA mappings and NHRP shortcuts |
| [SSH](07-ssh.txt) | Management-source authentication and access policy |
| [BFD timing](09-bfd-timing.json) | Same-router timestamp comparison |
| [Saved-state summary](configuration-summary.json) | Credential-free service and persistence checks |
| [SHA-256 manifest](SHA256SUMS.txt) | Hashes of the corresponding evidence files |

[Architecture overview](../assets/architecture.png) · [EVE-NG workspace](../assets/eve-topology.jpg)
