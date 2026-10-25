# Skills and evidence

| Skill | Evidence to inspect |
| --- | --- |
| IPv4/IPv6 routing and named EIGRP | Neighbor tables and routing state in [routing outputs](../evidence/01-routing.txt) |
| BGP policy | Actual exported prefixes, peer state, route preference and [BFD timing](../evidence/09-bfd-timing.json) |
| OSPF | Area adjacencies, summarization and default-route state in [routing outputs](../evidence/01-routing.txt) |
| Switching and gateway design | STP roots, HSRP roles, trunk state and bundled LACP members in [switching outputs](../evidence/02-switching.txt) |
| Segmentation | Expected/observed outcomes for [36 access-policy checks](../evidence/policy-results.json) |
| Resilience testing | Defined faults and sampled endpoint traffic in [resilience records](../evidence/05-resilience-tests.txt) |
| DMVPN | Remote NBMA mappings and NHRP shortcuts in [overlay records](../evidence/06-dmvpn.txt) |
| IP services and operations | DHCP, NTP and saved configuration checks in [service records](../evidence/03-services.txt) |
| Secure management | Authenticated access and source-policy tests in [SSH records](../evidence/07-ssh.txt) |
