# DC1

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)
- [Connected Endpoints](#connected-endpoints)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| DC1 | l2leaf | leaf_1a | 172.100.100.13/24 | cEOSLab | Provisioned | - |
| DC1 | l2leaf | leaf_1b | 172.100.100.14/24 | cEOSLab | Provisioned | - |
| DC1 | l2leaf | leaf_2a | 172.100.100.15/24 | cEOSLab | Provisioned | - |
| DC1 | l2leaf | leaf_2b | 172.100.100.16/24 | cEOSLab | Provisioned | - |
| DC1 | l2spine | spine_1 | 172.100.100.11/24 | cEOSLab | Provisioned | - |
| DC1 | l2spine | spine_2 | 172.100.100.12/24 | cEOSLab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l2leaf | leaf_1a | Ethernet1 | mlag_peer | leaf_1b | Ethernet1 |
| l2leaf | leaf_1a | Ethernet2 | mlag_peer | leaf_1b | Ethernet2 |
| l2leaf | leaf_1a | Ethernet3 | l2spine | spine_1 | Ethernet3 |
| l2leaf | leaf_1a | Ethernet4 | l2spine | spine_2 | Ethernet3 |
| l2leaf | leaf_1b | Ethernet3 | l2spine | spine_1 | Ethernet4 |
| l2leaf | leaf_1b | Ethernet4 | l2spine | spine_2 | Ethernet4 |
| l2leaf | leaf_2a | Ethernet1 | mlag_peer | leaf_2b | Ethernet1 |
| l2leaf | leaf_2a | Ethernet2 | mlag_peer | leaf_2b | Ethernet2 |
| l2leaf | leaf_2a | Ethernet3 | l2spine | spine_1 | Ethernet5 |
| l2leaf | leaf_2a | Ethernet4 | l2spine | spine_2 | Ethernet5 |
| l2leaf | leaf_2b | Ethernet3 | l2spine | spine_1 | Ethernet6 |
| l2leaf | leaf_2b | Ethernet4 | l2spine | spine_2 | Ethernet6 |
| l2spine | spine_1 | Ethernet1 | mlag_peer | spine_2 | Ethernet1 |
| l2spine | spine_1 | Ethernet2 | mlag_peer | spine_2 | Ethernet2 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |

## Connected Endpoints

No connected endpoint configured!
