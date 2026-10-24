# Enterprise VLAN Segmentation and Inter-VLAN Routing Lab

## Overview

This project demonstrates the design, configuration, and verification of a segmented enterprise LAN using Cisco Packet Tracer.

The network uses VLANs to separate HR and Management devices into distinct broadcast domains. A Cisco 2901 router provides DHCP services and enables communication between the VLANs through router-on-a-stick inter-VLAN routing.

Two Cisco 3560 multilayer switches connect the end devices and carry VLAN traffic over IEEE 802.1Q trunk links.

The implementation was tested successfully: PCs received IP addresses and default gateways through DHCP, reached their respective gateways, and communicated with devices in the other VLAN.

## Objectives

* Implement VLAN-based network segmentation.
* Configure access ports for end devices.
* Configure IEEE 802.1Q trunk links.
* Implement router-on-a-stick inter-VLAN routing.
* Configure DHCP pools for multiple subnets.
* Verify connectivity using ICMP ping tests.
* Inspect VLANs, trunks, interfaces, and neighboring devices using Cisco IOS commands.

## Network Topology

The lab contains:

* One Cisco 2901 router.
* Two Cisco 3560 multilayer switches.
* Multiple end devices distributed across VLANs 10 and 20.

The router connects to Switch0 through GigabitEthernet0/0 on the router and GigabitEthernet0/1 on Switch0.

Switch0 connects to Switch1 through GigabitEthernet0/2 on both switches.

## VLAN and IP Addressing

| VLAN ID | VLAN Name  | Network         | Default Gateway |
| ------- | ---------- | --------------- | --------------- |
| 10      | HR         | 192.168.10.0/24 | 192.168.10.1    |
| 20      | Management | 192.168.20.0/24 | 192.168.20.1    |

Both VLANs use separate IPv4 subnets.

## Technologies and Protocols

* Cisco Packet Tracer
* Cisco IOS CLI
* VLANs
* IEEE 802.1Q trunking
* Router-on-a-stick
* Dynamic Host Configuration Protocol (DHCP)
* IPv4 addressing and subnetting
* Internet Control Message Protocol (ICMP)
* Cisco Discovery Protocol (CDP)
* Per-VLAN Spanning Tree (PVST)

## Implementation

### 1. VLAN Configuration

VLAN 10 and VLAN 20 were created on both switches.

* VLAN 10 represents the HR network.
* VLAN 20 represents the Management network.

Access ports were assigned to the appropriate VLAN based on the intended end-device connections.

### 2. Trunk Configuration

IEEE 802.1Q trunking was configured on the router-facing and inter-switch links.

The inter-switch trunk was configured to allow VLANs 10 and 20.

Trunk operation was inspected using `show interfaces trunk`.

### 3. Inter-VLAN Routing

Router0 uses two subinterfaces on GigabitEthernet0/0:

| Interface             | VLAN | IP Address      |
| --------------------- | ---- | --------------- |
| GigabitEthernet0/0.10 | 10   | 192.168.10.1/24 |
| GigabitEthernet0/0.20 | 20   | 192.168.20.1/24 |

IEEE 802.1Q encapsulation associates each subinterface with its corresponding VLAN.

The router routes traffic between the two IP subnets.

### 4. DHCP Configuration

Separate DHCP pools were configured for VLAN 10 and VLAN 20.

The router excludes the following address ranges from dynamic assignment:

* 192.168.10.1–192.168.10.10
* 192.168.20.1–192.168.20.10

The DHCP pools provide subnet information, default gateways, DNS server information, and a domain name to clients.

### 5. Network Verification

The following Cisco IOS commands were used to inspect the configuration and operational state.

| Command                   | Purpose                                          |
| ------------------------- | ------------------------------------------------ |
| `show running-config`     | Inspect device configuration                     |
| `show vlan brief`         | Verify VLANs and access-port assignments         |
| `show interfaces trunk`   | Verify operational trunk links and allowed VLANs |
| `show ip interface brief` | Inspect interface status and IP addressing       |
| `show ip route`           | Inspect the routing table                        |
| `show cdp neighbors`      | Identify directly connected Cisco devices        |

## Testing and Results

| Test                             | Result                |
| -------------------------------- | --------------------- |
| DHCP address assignment          | Successful on all PCs |
| Default gateway assignment       | Successful            |
| Ping from VLAN 10 to its gateway | Successful            |
| Ping from VLAN 20 to its gateway | Successful            |
| Ping between VLAN 10 and VLAN 20 | Successful            |

These results confirm that DHCP address assignment, gateway reachability, and inter-VLAN communication are working in the simulated environment.

## Key Learning Outcomes

Through this project, I practised:

* Segmenting a LAN using VLANs.
* Assigning access ports to the correct VLANs.
* Configuring and verifying 802.1Q trunks.
* Implementing router-on-a-stick inter-VLAN routing.
* Providing IPv4 configuration through DHCP.
* Verifying connectivity with ICMP.
* Inspecting network devices using Cisco IOS operational commands.
* Using CDP to identify neighboring devices and connected interfaces.

## Future Improvements

Potential extensions to this lab include:

* Configure SSH for secure device administration.
* Apply port security to access ports.
* Implement DHCP snooping and Dynamic ARP Inspection where supported.
* Restrict trunk allowed-VLAN lists to the minimum required.
* Configure and verify appropriate spanning-tree root bridge placement.
* Add network monitoring using SNMP and a monitoring platform.
* Introduce documented fault scenarios and troubleshooting procedures.

These are proposed improvements, not features claimed to be implemented in the current lab.

## Repository Contents

* `topology/` — Packet Tracer project and topology image.
* `configurations/` — Router and switch configuration exports.
* `documentation/` — Addressing and VLAN documentation.
* `screenshots/` — Configuration and connectivity verification evidence.

## Author

Networking lab project developed using Cisco Packet Tracer for hands-on practice in enterprise LAN configuration and verification.
