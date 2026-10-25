# Findings and remediation

Audit date: 25 October 2026. Initial implementation by Mani Nazari; the subsequent audit included assisted testing and remediation.

| Finding | Change | Verification |
| --- | --- | --- |
| Thirteen managed devices used UTC+2 instead of the required UTC+8 | Corrected the local time zone | Final configuration and clock review across all 15 managed devices |
| The required privileged local admin account existed only on the two edge routers | Added the specified local account using Type 8 secrets on the other 13 devices | Structural checks for privilege 15 and Type 8; secrets are excluded from public evidence |
| Some router consoles lacked the required non-expiring console setting, and name lookup was not consistently disabled | Restored the required baseline settings | Final configuration review |
| IR2 IPv4 EIGRP did not use passive interfaces by default | Set the default passive state and explicitly enabled only the required neighbors | Operational neighbor tables and final AF-interface review |
| The CCTV ACL was absent from DS2 | Applied the policy to the second HQ gateway | Positive SVR2 and negative SVR1/Internet tests from a HQ CCTV endpoint; gateway role checks |
| Access switches had routing enabled, so the configured default gateway did not provide off-subnet management reachability | Returned AS1-AS4 to Layer 2 operation | Successful off-subnet management pings and NTP synchronization on all four access switches |
| NTP server/calendar settings were missing on some access switches | Completed the hierarchy and calendar synchronization settings | Final NTP status on every managed device |
| Client addresses had not been acquired after boot, and the SVR1 endpoint had no IPv4 address | Renewed client leases, initialized the SVR1 role, and saved endpoint state | DHCP DORA output, the PC1 reservation, endpoint address records, and traffic tests |
| The DMVPN setup could reach remote networks through a hub without proving a direct branch tunnel | Enabled Phase 3 redirect/shortcut behavior and verified the resulting forwarding entries | Both branch NBMA addresses appear dynamically; NHRP routes and branch pings are captured |
| Several router-to-switch links reported duplex mismatches | Matched full-duplex settings on the affected managed router interfaces | Final interface review; ISP1 configuration remained unchanged |

## Investigation changes that were not retained

A shorter IPv6 router-advertisement interval was tested while investigating partial distribution isolation. It did not resolve that failure case, so the experiment was reverted. Unsupported per-user SSH and fast LACP commands were rejected by the images and were not substituted with misleading equivalents.

## Recovery discipline

Running and startup configurations were captured before remediation. Fault tests used restoration steps, and the final collection checks that every interface deliberately disabled for testing has been re-enabled. Temporary access VLANs and client addresses used for policy tests were returned to their original roles before the final save.

Private baseline configurations and test scripts remain outside this public repository.
