# VLAN and Port Mapping

## VLAN Definitions

| VLAN ID | VLAN Name  | Purpose               | IPv4 Subnet     |
| ------- | ---------- | --------------------- | --------------- |
| 10      | HR         | HR department network | 192.168.10.0/24 |
| 20      | Management | Management network    | 192.168.20.0/24 |

## Switch0

| Interface           | Configuration         |
| ------------------- | --------------------- |
| FastEthernet0/1–0/3 | Access ports, VLAN 10 |
| FastEthernet0/4–0/6 | Access ports, VLAN 20 |
| GigabitEthernet0/1  | Trunk toward Router0  |
| GigabitEthernet0/2  | Trunk toward Switch1  |

## Switch1

| Interface            | Configuration         |
| -------------------- | --------------------- |
| FastEthernet0/1–0/7  | Access ports, VLAN 10 |
| FastEthernet0/8–0/12 | Access ports, VLAN 20 |
| GigabitEthernet0/2   | Trunk toward Switch0  |

## Trunking

The router-facing and inter-switch links use IEEE 802.1Q trunking. VLANs 10 and 20 are required for end-to-end connectivity.

## Verification Commands

```cisco
show vlan brief
show interfaces trunk
show cdp neighbors
```

These commands were used to inspect VLAN membership, trunk status, and neighboring Cisco devices.
