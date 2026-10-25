# Requirements map

All 58 Module C aspects from the supplied marking workbook are mapped below. The weights sum to 25 available marks. These are maximum reference weights, **not awarded marks**. The source contains both measurement and graded aspects; no official score is calculated from these statuses.

**VERIFIED** means the described behavior or state was observed. **CONFIG REVIEWED** means the setting was inspected without exhaustive feature-specific fault injection. **PARTIAL / OPEN**, **PLATFORM LIMIT**, and **FUNCTIONAL WITH DEVIATION** do not represent a full pass. Read the [known findings](known-findings.md) alongside the rows. Private credential checks are summarized as booleans; configurations and hashes are not published.

The row number identifies the original workbook aspect, including repeated aspect identifiers. Source-document inconsistencies are interpreted explicitly in the findings.

| Source row | Aspect | Maximum marks | Audit status | Scope and evidence |
| --- | --- | ---: | --- | --- |
| 193 | 3.1.1: IPv4 Addressing  Issue#1- IR1 | 0.2 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 194 | 3.1.1: IPv4 Addressing  Issue#2- CR1 | 0.2 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 195 | 3.1.1: IPv4 Addressing  Issue#3- DS1 | 0.2 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 196 | 3.1.1: IPv4 Addressing - AS3 | 0.1 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 197 | 3.1.1: IPv4 Addressing - AS4 | 0.1 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 198 | 3.1.1: IPv4 Addressing - BR1 | 0.1 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 199 | 3.1.1: IPv4 Addressing - BR2 | 0.1 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 200 | 3.1.2: IPv6 Addressing - DS1 | 0.25 | CONFIG REVIEWED | Matches the supplied DS1 table; see addressing adaptation note for the separate IR2-CR1 link. [Evidence](../evidence/configuration-summary.json) |
| 201 | 3.1.2: IPv6 Addressing - DS2 | 0.25 | CONFIG REVIEWED | Matches the supplied DS2 table. [Evidence](../evidence/configuration-summary.json) |
| 202 | 3.1.3: TimeZone | 0.25 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 203 | 3.1.4: DomainName | 0.25 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 204 | 3.1.5: Privileged mode password | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/configuration-summary.json) |
| 206 | 3.2.1: VTP - Configuration | 0.25 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/02-switching.txt) |
| 207 | 3.2.2: Vlan Configuration | 0.25 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/02-switching.txt) |
| 208 | 3.2.7: HSRP-IPv6 | 0.5 | PARTIAL / OPEN | Baseline and role transition observed; end-to-end IPv6 failover fails (F03). [Evidence](../evidence/02-switching.txt) |
| 209 | 3.2.8: STP Protection | 0.5 | VERIFIED | Root Guard and Loop Guard configured; blocking events observed during fault tests. BPDU suppression is configured on the designated lab port. [Evidence](../evidence/02-switching.txt) |
| 210 | 3.2.9: Access Port Configuration | 0.25 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/02-switching.txt) |
| 211 | 3.2.3: STP | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/02-switching.txt) |
| 216 | 3.2.4: 802.1Q Trunk | 0.5 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/02-switching.txt) |
| 221 | 3.2.5: EtherChannel - LACP | 0.5 | PARTIAL / OPEN | Bundle and bilateral member-outage traffic verified; unilateral shutdown remains a failure (F04). [Evidence](../evidence/02-switching.txt) |
| 226 | 3.2.6: HSRP-IPv4 | 0.5 | PARTIAL / OPEN | Current groups and takeover verified; partial DC SVI failure remains open (F05). Future unknown groups are not auto-created. [Evidence](../evidence/02-switching.txt) |
| 232 | 3.3.2: EIGRP - Router ID | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 233 | 3.3.3: EIGRP - Route Advertisement | 0.5 | CONFIG REVIEWED | Routes and network statements reviewed. The inherited IPv6 link-prefix adaptation is documented separately. [Evidence](../evidence/01-routing.txt) |
| 234 | 3.3.4: EIGRP - Hello Message should be suppressed | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 235 | 3.3.5: EIGRP - Bandwith Control | 0.5 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 236 | 3.3.6: EIGRP - Metric Weights | 0.5 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 237 | 3.3.7: EIGRP-Route Summary | 0.25 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 238 | 3.3.8: EIGRP Authentication | 0.5 | VERIFIED | Named EIGRP HMAC-SHA-256 is configured on the IPv4 IR1-IR2 adjacency; no authentication-failure injection was performed. [Evidence](../evidence/01-routing.txt) |
| 239 | 3.3.9: EIGRP Default Redistribution | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 240 | 3.3.10: EIGRP Route Summarization | 0.25 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 241 | 3.3.11: EIGRP - IPv6 | 0.5 | PARTIAL / OPEN | Baseline PC1-to-IR2 IPv6 traffic verified; distribution failover remains open under F03. [Evidence](../evidence/01-routing.txt) |
| 242 | 3.3.1: EIGRP Named Configuration | 0.5 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 248 | 3.4.1: OSPF- Basic Config | 0.25 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 249 | 3.4.2: OSPF - Route Advertisement | 0.5 | CONFIG REVIEWED | DC VLANs follow the task, rather than the inconsistent VLAN labels in the marking note. [Evidence](../evidence/01-routing.txt) |
| 250 | 3.4.3: OSPF-Hello Messages | 0.25 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 251 | 3.4.4: OSPF-No DR/BDR election | 0.5 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 252 | 3.4.5: OSPF-Default Route | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 253 | 3.4.6: OSPF-Summary Routes | 0.5 | CONFIG REVIEWED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 255 | 3.5.1: eBGP-Basic Config with ISP | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 256 | 3.5.2: eBGP-Basic Config with IR3 | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 257 | 3.5.3: BGP - BFD (sub-second failover) | 0.5 | CONFIG + SESSION; TIMING UNMEASURED | Session UP and BGP registration verified; nominal 900 ms budget. Actual sub-second recovery is unmeasured (F06). [Evidence](../evidence/01-routing.txt) |
| 258 | 3.5.4: BGP - Route Advertisement | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 259 | 3.5.5: BGP - Prefix Filter | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 260 | 3.5.6: iBGP peering | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 261 | 3.5.7: BGP Route-map | 0.75 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 262 | 3.5.8: BGP Path Attribute (MED) | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/01-routing.txt) |
| 263 | 3.5.9: BGP Failover | 0.75 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/05-failure-tests.txt) |
| 265 | 3.6.1: Dynamic NAT - IR1 & IR2 | 0.5 | VERIFIED | All 36 site/VLAN/destination policy probes matched the expected result; both exit pools were observed. [Evidence](../evidence/04-policy-tests.txt) |
| 266 | 3.6.4: IP DHCP- DS1 and DS3 | 0.25 | VERIFIED | HQ leases and PC1 reservation verified. Device naming in the marking title differs from the task. [Evidence](../evidence/03-services.txt) |
| 267 | 3.6.5: IP DHCP- BR1 and BR2 | 0.25 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/03-services.txt) |
| 268 | 3.6.2: Conditional Static NAT | 0.75 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/05-failure-tests.txt) |
| 273 | 3.6.3: NTP | 0.75 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/03-services.txt) |
| 279 | 3.7.1: DMVPN Hub - IR1/IR2 | 0.75 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/06-dmvpn.txt) |
| 280 | 3.7.2: DMVPN Spoke - BR1/BR2 | 0.75 | FUNCTIONAL WITH DEVIATION | Dynamic direct branch shortcuts work with the inherited extra underlay host routes; strict route allowance is not satisfied (F02). [Evidence](../evidence/06-dmvpn.txt) |
| 281 | 3.7.3: EIGRP Summary route - BR1/BR2 | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/06-dmvpn.txt) |
| 282 | 3.7.5: SSH - VTY ACL | 0.5 | VERIFIED | Reviewed against the final private configuration and selected operational records. [Evidence](../evidence/07-ssh.txt) |
| 283 | 3.7.4: SSH -IR1/IR2 | 0.5 | PLATFORM LIMIT | SSHv2 works. The requested per-user limit is unsupported; a global VTY limit is not counted as equivalent (F01). [Evidence](../evidence/06-dmvpn.txt) |
| 288 | 3.7.6: Extended ACL | 0.75 | VERIFIED | CCTV allow/deny probes passed at all three sites. DHCP and HSRP exceptions were reviewed; DNS application service was not present on VPCS. [Evidence](../evidence/04-policy-tests.txt) |
