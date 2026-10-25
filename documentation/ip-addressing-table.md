# IP Addressing Plan

## Overview

The lab uses two IPv4 subnets to separate HR and Management devices into different VLANs. Router0 provides the default gateways and DHCP services.

| VLAN | Name       | Network      | Subnet Mask   | Default Gateway |
| ---- | ---------- | ------------ | ------------- | --------------- |
| 10   | HR         | 192.168.10.0 | 255.255.255.0 | 192.168.10.1    |
| 20   | Management | 192.168.20.0 | 255.255.255.0 | 192.168.20.1    |

## Router Subinterfaces

| Interface             | VLAN | IP Address      |
| --------------------- | ---- | --------------- |
| GigabitEthernet0/0.10 | 10   | 192.168.10.1/24 |
| GigabitEthernet0/0.20 | 20   | 192.168.20.1/24 |

## DHCP Configuration

Router0 has separate DHCP pools for VLAN 10 and VLAN 20.

The following ranges are excluded from DHCP allocation:

* VLAN 10: 192.168.10.1–192.168.10.10
* VLAN 20: 192.168.20.1–192.168.20.10

Clients obtain their IP configuration dynamically.

## Verification

DHCP assignment was verified on all PCs. Default gateway reachability and communication between VLAN 10 and VLAN 20 were tested successfully.

Individual PC addresses are not listed here because they may be assigned dynamically by DHCP.
