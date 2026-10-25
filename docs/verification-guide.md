# Verification method

Tests were executed through the EVE-NG node consoles against the running lab. Selected outputs are preserved as plain text with the device, test phase, and capture time. These are exported console records, not screenshots of a terminal and not an external certification of authorship.

## 1. Establish the baseline

Capture the running/startup configurations privately before any change. Check current addresses and routing state on the relevant router or distribution switch:

```text
show ip interface brief
show ipv6 interface brief
show ip route
show ipv6 route
```

Compare these outputs with the reference tables after mapping the physical GigabitEthernet names to the lab image's Ethernet names. Check the stated source-document inconsistencies before making an address change.

## 2. Verify the control plane

On HQ EIGRP devices:

```text
show ip eigrp neighbors
show ipv6 eigrp neighbors
show ip protocols
show ip eigrp interfaces detail
```

On the edge routers and the DC OSPF devices, use the commands relevant to their configured protocols:

```text
show ip bgp summary
show ip bgp
show bfd neighbors details
show ip ospf neighbor
```

An established neighbor alone does not verify filtering. Inspect each edge's actual advertised routes and compare the complete advertised set with the permitted summaries.

## 3. Verify gateways and switching

On distribution switches:

```text
show standby brief
show spanning-tree root
show spanning-tree inconsistentports
show interfaces trunk
show etherchannel summary
```

Record baseline roles, inject one defined fault, capture the changed roles and endpoint traffic, then restore and check the original roles. A unilateral software shutdown in IOL is recorded separately from disabling both ends of a simulated physical link.

## 4. Exercise data-plane policies

Use an endpoint in each tested site/VLAN role. Test the allowed server, the disallowed server where applicable, and the simulated Internet address. A deny result must be attributable to the policy, such as an administrative-prohibition response; an unaddressed client or an unrelated timeout does not prove a working ACL.

For NAT, generate the traffic before collecting translations:

```text
show ip nat translations
show ip nat statistics
```

Check the inside local address, translated address, and destination together. Repeat with the alternate exit active. Do not use a static mapping's mere presence as proof that a packet matched its condition.

## 5. Verify services and branch shortcuts

```text
show ip dhcp binding
show ip dhcp conflict
show ntp status
show ntp associations
show dmvpn
show ip nhrp
```

Generate branch-to-branch traffic before checking NHRP. Confirm that the dynamic peer points to the remote branch NBMA address and that a shortcut route is installed.

## 6. Restore and save

Re-enable every interface disabled during testing. Restore temporary access VLANs and endpoint addresses, verify the intended roles and connectivity, and save the managed device configurations:

```text
write memory
```

Save endpoint state separately. Keep secrets and full configuration backups private. Record unresolved outcomes explicitly rather than assigning a full pass from configuration syntax alone.
