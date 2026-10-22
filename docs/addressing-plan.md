# Addressing Plan

This table is reconstructed from the saved Packet Tracer configuration.

## IPv4 domain

| Site/link | Network | Gateway/router interface | Endpoint |
|---|---|---|---|
| Branch C — VLAN 10 | `150.50.40.0/25` | Router1 Fa0/0.1 — `150.50.40.1` | Server1 — `150.50.40.2` |
| Branch C — VLAN 20 | `150.50.40.128/25` | Router1 Fa0/0.2 — `150.50.40.130` | PC1 — `150.50.40.131` |
| Branch C — VLAN 30 | `150.50.41.0/28` | Router1 Fa0/0.3 — `150.50.41.1` | Wireless Router0 WAN — `150.50.41.3` |
| HQ–Branch C WAN | `150.50.67.0/30` | Router0 Se0/1/1 — `150.50.67.1` | Router1 Se0/1/1 — `150.50.67.2` |
| Wireless Router0 LAN | `192.168.0.0/24` | Wireless Router0 — `192.168.0.1` | Wireless clients as configured |

## IPv6 domain

| Site/link | Prefix | Assigned router/endpoints |
|---|---|---|
| Headquarters LAN | `AB12:1640:0:2::/64` | Router0 `::2`, PC0 `::10`, Server0 `::11` |
| HQ–Branch A WAN | `AB12:1640:0:3::/64` | Router0 `::2`, Router2 `::3` |
| Branch A LAN | `AB12:1640:0:4::/64` | Router2 `::3`, Server3 `::4`, PC3 `::5` |
| Branch A–Branch B WAN | `AB12:1640:0:5::/64` | Router2 `::3`, Router3 `::4` |
| Branch B LAN | `AB12:1640:0:6::/64` | Router3 `::4`, Server2 `::5`, PC2 `::6` |
| Branch B–HQ WAN | `AB12:1640:0:7::/64` | Router0 `::2`, Router3 `::4` |
| Translation prefix | `64:FF9B::/96` | Present in Router0 configuration; operation not yet validated |

## VLAN Plan

| VLAN | Saved name | Subnet | Access endpoint | Routing interface |
|---|---|---|---|---|
| 10 | `VLAN_A` | `150.50.40.0/25` | Server1 | Router1 Fa0/0.1 |
| 20 | `VLAN_B` | `150.50.40.128/25` | PC1 | Router1 Fa0/0.2 |
| 30 | `VLAN_C` | `150.50.41.0/28` | Wireless Router0 WAN | Router1 Fa0/0.3 |
