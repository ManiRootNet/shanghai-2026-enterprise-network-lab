# Known findings and scope limits

These findings are part of the deliverable. Successful baseline traffic does not close a failure case that still drops traffic.

## F01: SSH sessions per user

**Status: platform limitation.** The requested per-user session-limit command is rejected by both edge router images. SSHv2 and the management-source ACL work, and the existing configuration exposes three SSH-capable VTY lines. That is a global limit, not independent enforcement per username.

Retest the requirement on a supported IOS XE image. The command appears in [Cisco's IOS XE command reference](https://www.cisco.com/c/en/us/td/docs/routers/sd-routing/command/reference/sd-routing-cr-book/m-sd-routing-secure-wan-edge-yang-commands.html). `ip ssh maxstartups` governs concurrent connection establishment and was not substituted for a limit on authenticated sessions.

## F02: Branch underlay differs from the strict static-route allowance

**Status: documented deviation.** The initial branch configuration contains one additional peer-NBMA host route at each branch, beyond the two routes explicitly allowed by the supplied task. The direct Phase 3 shortcut is functional with that underlay, but this is not a strict pass against the stated route restriction.

The branch-to-branch underlay design and the supplied route allowance need to be reconciled before claiming full compliance. ISP1 was not reconfigured during this audit. No static routes to Null0 were added to force BGP announcements.

## F03: IPv6 traffic during HQ distribution failover

**Status: unresolved forwarding failure.** Baseline PC1-to-IR2 IPv6 pings pass. HSRP group 1103 changes to Active on DS2 when DS1 is isolated, but the tested VPCS endpoint does not retain IPv6 reachability in that failure state. IPv4 traffic continues in the complete DS1 isolation test.

Both partial Layer 2 isolation and isolation of all six connected DS1 links were tested. A shorter RA interval was tested and reverted because it did not resolve the issue. The role transition alone is therefore not accepted as a successful IPv6 failover result.

A temporary Cisco IPv6 host on AS1 also lost reachability in the isolated state, while a ping originated by DS2 from its real SVI address succeeded. This prevents attributing the failure only to VPCS. The temporary host interface was removed. Further work must examine neighbor discovery and the emulated HSRP forwarding path, ideally with packet capture and another switch image. The OOD flag shown for an active virtual link-local address is [normal documented HSRP behavior](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst9500/software/release/26-x/command_reference/b_26x_9500_cr/ip_addressing__services_commands.html); it is not itself proof of a fault.

## F04: One-sided LACP member shutdown

**Status: reproducible failure in this lab.** A one-sided member shutdown leaves the remote member in independent mode while the other link remains bundled. PC1-to-SVR1 probes fail throughout the recorded test window of more than two minutes. A both-ends member shutdown passes with the surviving member carrying traffic.

This difference is preserved in the evidence. It may involve the interaction between the required standalone fallback and the image's link-state behavior; the root cause has not been proven. The fast LACP command was also rejected by the current switch images. No recovery-time claim is made for the one-sided case.

## F05: Partial DC SVI failure

**Status: reproducible failure outside the main WAN failover test.** Shutting only DS3's server SVI moves the HSRP role to DS4, but SVR1-to-PC1 traffic fails. In contrast, isolating DS3's upstream and inter-switch links lets the surviving SVR2 endpoint reach PC1 through DS4.

The combination of partial prefix loss, summarization, and forwarding needs further investigation. A summary discard path is a candidate explanation, not a confirmed diagnosis. Also, the two VPCS server roles are each attached to a single distribution switch; gateway redundancy alone cannot provide server availability after loss of that server's only physical attachment.

## F06: BFD timing is not a measured application recovery time

**Status: configuration and session verified; sub-second timing unmeasured.** Both ends show a BFD session registered to BGP, configured for a 300 ms interval and multiplier 3. The nominal detection budget is 900 ms. Console polling and a software shutdown do not establish a measured sub-second end-to-end traffic recovery time.

Use timestamped packet capture or a suitable traffic generator for a timing claim.

## Reference inconsistencies and adaptations

- Interface names are mapped from the reference's GigabitEthernet ports to the Ethernet ports available in the images.
- The reference repeats the same IPv6 /64 on the IR2-CR1 and CR2-DS1 point-to-point links. The inherited lab uses a distinct prefix for IR2-CR1. This is an explicit addressing adaptation, not a claim of exact table compliance.
- The DC addressing table places the second server's address in the management subnet, while a VLAN is separately named for SVR2. The implementation follows the supplied server address and matching gateway; it does not silently move that server to a different subnet.
- The DC gateway wording refers to a .1 address in a /24, while the supplied server subnets are /27. The implementation uses the first usable address of each actual /27.
- Some marking notes name HQ VLANs in the DC OSPF section and label a DHCP device differently from the task. The networking task and observed topology are used for interpretation; these discrepancies are retained rather than treated as configuration errors.
- Current DC HSRP groups are configured. Unknown future VLANs require their own gateway addressing and HSRP configuration; STP priorities can cover future VLANs, but that does not automatically create future HSRP groups.

## What is not assessed here

Windows services, Linux services, real Internet access, encryption of the mGRE overlay, production security, physical-hardware behavior, and the other WorldSkills modules are outside this Cisco lab audit. GRE/NHRP is not described as an encrypted VPN in this portfolio.
