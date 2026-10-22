# Validation Plan

Run these checks in Packet Tracer and save concise screenshots or text output under a future `evidence/` folder.

## Branch C switching

On Switch2:

```text
show vlan brief
show interfaces trunk
show running-config
```

Expected:

- Fa0/1 in VLAN 10
- Fa0/2 and Fa0/3 operating as trunks
- Gi0/1 operating as the trunk to Router1

On Switch3 and Switch4, confirm the endpoint access ports and VLAN databases.

## IPv4 routing

On Router0 and Router1:

```text
show ip ospf neighbor
show ip route
show ip interface brief
```

Expected:

- OSPFv2 adjacency across `150.50.67.0/30`
- Router0 learns Branch C's VLAN networks
- Router1 learns any intended remote IPv4 routes

## IPv6 routing

On Router0, Router2 and Router3:

```text
show ipv6 ospf neighbor
show ipv6 route
show ipv6 interface brief
```

Expected:

- OSPFv3 adjacencies across the three routed serial links
- Each router learns the other IPv6 LAN prefixes

## Endpoint tests

Record results for at least:

1. PC0 to Server0 over IPv6
2. PC3 to Server3 over IPv6
3. PC2 to Server2 over IPv6
4. PC3 to PC2 over IPv6 across the WAN
5. Server1 to PC1 over IPv4 through inter-VLAN routing
6. PC1 to the Wireless Router0 WAN interface over IPv4
7. An IPv4-to-IPv6 test only after the translation configuration is corrected

Use a table:

| Test | Source | Destination | Protocol | Expected | Actual |
|---|---|---|---|---|---|
| 1 | PC0 | Server0 | IPv6 ICMP | Pass | To be tested |

## Translation/NAT checks

```text
show running-config | include nat
show ip nat statistics
show ip nat translations
```

Do not describe NAT64 as operational until the configuration is corrected and a cross-protocol test succeeds.
