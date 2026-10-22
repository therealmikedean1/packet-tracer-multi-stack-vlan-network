# Project Audit

## Confirmed strengths

The saved `.pkt` file is a substantial multi-branch networking exercise rather than a basic home-network lab. It contains:

- 20 devices and 19 links
- Four Cisco 1841 routers
- Six Cisco 2960 switches
- Headquarters and three branch locations
- OSPFv2 and OSPFv3
- A three-router IPv6 WAN triangle
- An IPv4 HQ-to-branch WAN link
- Three VLANs with router-on-a-stick routing
- 802.1Q access/trunk configuration
- IPv4 VLSM and structured IPv6 prefix allocation
- Server, PC and wireless-router endpoints

## Accuracy of the “dual-stack” description

The project contains both IPv4 and IPv6, but the configured endpoints and most interfaces are not simultaneously assigned both protocols. Branch C is predominantly IPv4; HQ, Branch A and Branch B are predominantly IPv6. Therefore, “mixed IPv4/IPv6 topology” or “IPv4/IPv6 transition network” is currently more accurate than “dual-stack network.”

## Items requiring correction or validation

### 1. Translation configuration is incomplete or internally inconsistent

Router0 contains:

```text
ip nat inside source list 1 pool NAT64_POOL overload
ipv6 nat prefix 64:FF9B::/96
```

However, the saved running configuration contains no definition for `ip nat pool NAT64_POOL`. It also contains no conventional `ip nat inside` statement on an IPv4 inside interface. Several IPv6-facing interfaces use `ipv6 nat`, while the IPv4-facing serial interface uses `ip nat outside`.

This may represent an unfinished NAT-PT/NAT64 attempt. It should not be described as working until corrected and demonstrated with an actual IPv4-to-IPv6 connectivity test.

### 2. ACL 1 probably does not match the intended source network

The configuration contains:

```text
access-list 1 permit 0.0.0.0 255.255.0.0
```

That is not equivalent to `permit any`, and it does not express the Branch C `150.50.0.0/16` range in the usual form. If the intended source is `150.50.0.0/16`, the conventional wildcard expression would be:

```text
access-list 1 permit 150.50.0.0 0.0.255.255
```

The correct ACL depends on the intended translation direction and design.

### 3. Generic IOS hostnames

Every IOS router is saved as `Router`, and every switch as `Switch`. For a portfolio version, use descriptive names such as:

- `HQ-R1`
- `BRANCH-A-R1`
- `BRANCH-B-R1`
- `BRANCH-C-R1`
- `HQ-SW1`
- `BRANCH-C-DIST-SW1`

### 4. End-to-end results are not captured

The file stores topology and configuration, but the repository still needs fresh evidence of:

- OSPFv2 neighbours
- OSPFv3 neighbours
- learned routes
- trunk operation
- inter-VLAN connectivity
- IPv6 inter-branch connectivity
- translation behaviour, if retained

## Safe portfolio wording now

> Designed a 20-device multi-branch IPv4/IPv6 topology in Cisco Packet Tracer with VLAN segmentation, 802.1Q trunks, router-on-a-stick inter-VLAN routing, IPv4 VLSM, IPv6 `/64` addressing, OSPFv2 and OSPFv3 dynamic routing.

## Wording to avoid until validated

Do not yet claim:

- fully operational NAT64
- complete end-to-end IPv4/IPv6 translation
- a fully dual-stack network
- verified failover or redundancy
- production deployment
