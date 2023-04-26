# DC1_FABRIC

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
  - [Connected Endpoint Keys](#connected-endpoint-keys)
  - [Firewalls](#firewalls)
  - [Servers](#servers)
  - [Port Profiles](#port-profiles)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| DC1_FABRIC | leaf | LEAF1 | 192.168.0.42/24 | vEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF2 | 192.168.0.43/24 | vEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF3 | 192.168.0.44/24 | vEOS-lab | Provisioned | - |
| DC1_FABRIC | leaf | LEAF4 | 192.168.0.45/24 | vEOS-lab | Provisioned | - |
| DC1_FABRIC | spine | SPINE1 | 192.168.0.40/24 | vEOS-lab | Provisioned | - |
| DC1_FABRIC | spine | SPINE2 | 192.168.0.41/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| leaf | LEAF1 | Ethernet1 | spine | SPINE1 | Ethernet1 |
| leaf | LEAF1 | Ethernet2 | spine | SPINE2 | Ethernet1 |
| leaf | LEAF1 | Ethernet11 | mlag_peer | LEAF2 | Ethernet11 |
| leaf | LEAF1 | Ethernet12 | mlag_peer | LEAF2 | Ethernet12 |
| leaf | LEAF2 | Ethernet1 | spine | SPINE1 | Ethernet2 |
| leaf | LEAF2 | Ethernet2 | spine | SPINE2 | Ethernet2 |
| leaf | LEAF3 | Ethernet1 | spine | SPINE1 | Ethernet3 |
| leaf | LEAF3 | Ethernet2 | spine | SPINE2 | Ethernet3 |
| leaf | LEAF3 | Ethernet11 | mlag_peer | LEAF4 | Ethernet11 |
| leaf | LEAF3 | Ethernet12 | mlag_peer | LEAF4 | Ethernet12 |
| leaf | LEAF4 | Ethernet1 | spine | SPINE1 | Ethernet4 |
| leaf | LEAF4 | Ethernet2 | spine | SPINE2 | Ethernet4 |
| spine | SPINE1 | Ethernet11 | mlag_peer | SPINE2 | Ethernet11 |
| spine | SPINE1 | Ethernet12 | mlag_peer | SPINE2 | Ethernet12 |

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
| --------------------- | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |

## Connected Endpoints

### Connected Endpoint Keys

| Key | Type | Description |
| --- | ---- | ----------- |
| firewalls | firewall | - |
| routers | router | - |
| servers | server | - |

### Firewalls

| Name | Port | Fabric Device | Fabric Port | Description | Shutdown | Type | Mode | VLANs | Profile |
| ---- | ---- | ------------- | ------------| ----------- | -------- | ---- | ---- | ----- | ------- |
| FIREWALL | Eth1 | SPINE1 | Ethernet5 | FIREWALL_Eth1 | False | switched | trunk | 10,20,30 | PP-FIREWALL |
| FIREWALL | Eth2 | SPINE2 | Ethernet5 | FIREWALL_Eth2 | False | switched | trunk | 10,20,30 | PP-FIREWALL |

### Servers

| Name | Port | Fabric Device | Fabric Port | Description | Shutdown | Type | Mode | VLANs | Profile |
| ---- | ---- | ------------- | ------------| ----------- | -------- | ---- | ---- | ----- | ------- |
| Host2 | Eth1 | LEAF4 | Ethernet3 | Host2_Eth1 | False | switched | access | 30 | PP-ORANGE |
| HostA | Eth1 | LEAF1 | Ethernet3 | HostA_Eth1 | False | switched | access | 10 | PP-BLUE |
| HostB | Eth1 | LEAF2 | Ethernet3 | HostB_Eth1 | False | switched | access | 20 | PP-GREEN |
| HostC | Eth1 | LEAF3 | Ethernet3 | HostC_Eth1 | False | switched | access | 10 | PP-BLUE |

### Port Profiles

| Profile Name | Parent Profile |
| ------------ | -------------- |
| PP-DEFAULTS | - |
| PP-BLUE | - |
| PP-GREEN | - |
| PP-ORANGE | - |
| PP-FIREWALL | - |
