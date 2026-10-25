# Shanghai 2026 Enterprise Network Lab

**Mani Nazari · Network engineering portfolio**

A working EVE-NG implementation of the networking module from the WorldSkills Shanghai 2026 IT Network Systems Administration practice material. This project connects a headquarters, a data centre, and two branches across a simulated ISP.

![Architecture overview](assets/architecture.png)

## What this project demonstrates

| Area | Implementation and evidence |
| --- | --- |
| Enterprise routing | Named EIGRP for IPv4/IPv6, OSPF areas 0 and 10, authenticated eBGP and iBGP |
| Route control | Dynamic aggregation, exact outbound prefix filters, MED preference, conditional default redistribution |
| Campus redundancy | Rapid PVST+, VLAN-based root placement, LACP, IPv4/IPv6 HSRP, STP protection |
| Branch connectivity | Two DMVPN hubs, NHRP registration, dynamically installed spoke-to-spoke shortcuts |
| Segmentation | Separate management, CCTV, wireless, and corporate VLANs; tested allow and deny decisions |
| IP services | DHCP and a client reservation, NTP hierarchy, exit-specific PAT, destination-specific static NAT |
| Operations | Baseline capture, fault injection, recovery checks, and a traceable record of remaining limitations |

The lab contains **15 managed Cisco devices, one simulated ISP router, and six VPCS endpoints**. The endpoints represent four clients and two server roles. They do not run Windows or application server workloads.

## Results worth inspecting

- With the direct HQ-to-DC link disabled, PC1 and PC4 still reached SVR1 through the ISP path.
- With the primary Internet exit disabled, permitted clients used the secondary exit. The captured translations changed to the secondary NAT pool.
- PC4-to-SVR1 traffic used the required exit-specific translation. Its traffic to SVR2 remained outside that special translation.
- CCTV clients at all three user sites reached SVR2 and were denied access to SVR1 and the simulated Internet. Management Internet access was also denied.
- A branch-to-branch ping was checked against the NHRP table. The final evidence shows the remote branch NBMA address and an installed dynamic shortcut, rather than treating a successful ping as proof of a direct tunnel.

Start with the [validation report](docs/validation-report.md), then inspect the [58-aspect requirements map](docs/requirements-map.md) and [selected console evidence](evidence/README.md).

## Read this alongside the results

This is an engineering case study with recorded failures as well as successful tests. It is **not a claim of a perfect marking score**. The current IOS images lack the requested SSH limit per user, and the inherited branch underlay includes additional host routes outside the test project's strict static-route allowance. Partial distribution failures and a one-sided LACP member failure also exposed forwarding problems. Their observations and retests are retained in [known findings](docs/known-findings.md).

The validation distinguishes a configured timer from a measured recovery time. In particular, a BFD configuration with a nominal 900 ms detection budget is not presented as a measured end-to-end sub-second failover result.

## Project record

| Item | Detail |
| --- | --- |
| Initial implementation | Mani Nazari |
| Audit and remediation | Assisted validation pass, 25 October 2026 |
| Environment | EVE-NG on VMware; Cisco IOS 15.4 routers and IOS 15.2 switch images |
| Reference | Locally supplied WSC2026 TP39 Module C, version 1.0, dated 4 August 2026 |
| Marking reference | Locally supplied marking workbook; 58 Module C aspects, 25 available marks |

The [change record](docs/change-record.md) explains what was found and corrected. The [verification guide](docs/verification-guide.md) describes how the evidence was obtained.

Full configurations, credentials, IOS images, lab exports, official question PDFs, and complete solution scripts are intentionally absent. This repository presents implementation outcomes and selected operational evidence.

## About the lab

This is independent personal practice based on the referenced material. It does not imply competition participation, an award, certification, or affiliation with WorldSkills or Cisco. The diagram is an original overview of this implementation; it is not a reproduction of the official topology artwork.

[GitHub profile](https://github.com/ManiRootNet) · [LinkedIn](https://www.linkedin.com/in/mani-nazari-683877381/)
