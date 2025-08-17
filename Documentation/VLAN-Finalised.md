# 🌐 Network Configuration Documentation

This document details the current network configuration of the **HomeLab** environment, including the MikroTik RB5009UG+S+ router, Cisco Catalyst switch, and TP-Link Wi-Fi 7 access point.

---

## 🔹 Topology Overview

- **Router (MikroTik RB5009UG+S+)**  
  Handles routing, VLAN interfaces, DHCP, NAT, and firewall.

- **Cisco Catalyst Switch**  
  Provides VLAN access and trunk ports, forwards VLAN-tagged traffic.

- **Wireless Access Point (TP-Link Wi-Fi 7)**  
  Connected via switch, currently providing Wi-Fi (no VLAN-to-SSID mapping).

- **PCs & Wired Devices**  
  Connected to switch access ports; receive IPs from MikroTik DHCP pools.

---

## 🔹 MikroTik RB5009 Configuration

### 1️⃣ VLAN Interfaces

Created VLAN interfaces on the main bridge (WAN uplink remains on `ether1`).

| VLAN ID | Name         | Subnet            | Gateway IP      | Notes                    |
|---------|--------------|-------------------|-----------------|--------------------------|
| 10      | VLAN10-Main  | 192.168.10.0/24   | 192.168.10.1    | Trusted LAN (PCs)        |
| 20      | VLAN20-Guest | 192.168.20.0/24   | 192.168.20.1    | Guest network            |
| 30      | VLAN30-IoT   | 192.168.30.0/24   | 192.168.30.1    | Smart/IoT devices        |
| 40      | VLAN40-Lab   | 192.168.40.0/24   | 192.168.40.1    | Pentesting/Lab network   |
| 99      | VLAN99-Mgmt  | 192.168.99.0/24   | 192.168.99.1    | Switch/AP/Router Mgmt    |

- **WAN uplink:** `ether1` → DHCP client → NAT masquerade

---

### 2️⃣ Bridge VLAN Table

Configured VLAN tagging/untagging:

- **Trunk Port**  
  `ether2` (to Cisco switch) → Tagged VLANs: 10,20,30,40,99

- **Access Ports**  
  - `ether3` → PVID 10 (Main LAN untagged)  
  - `ether4` → PVID 40 (Lab untagged)  
  - `ether5` → PVID 30 (IoT untagged)  
  - `ether8` → PVID 99 (Management untagged)

---

### 3️⃣ DHCP Servers

Each VLAN has its own DHCP pool managed by MikroTik.

| VLAN   | Pool Range             | Gateway       | Notes          |
|--------|------------------------|---------------|----------------|
| VLAN10 | 192.168.10.100–200     | 192.168.10.1  | PCs, trusted   |
| VLAN20 | 192.168.20.100–200     | 192.168.20.1  | Guest devices  |
| VLAN30 | 192.168.30.100–200     | 192.168.30.1  | IoT devices    |
| VLAN40 | 192.168.40.100–200     | 192.168.40.1  | Lab devices    |
| VLAN99 | 192.168.99.100–200     | 192.168.99.1  | Mgmt devices   |

---

### 4️⃣ Firewall & NAT

- **NAT Masquerade:** All outgoing traffic → WAN  
- **Inter-VLAN Traffic:** Currently allowed by default  
  > *Planned: Implement filtering rules for isolation (e.g., Guest/IoT restrictions)*

---

## 🔹 Cisco Catalyst Switch Configuration

### 1️⃣ Trunk Port (Uplink to MikroTik)

```plaintext
interface Gi1/0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,99
 switchport trunk native vlan 1
```
### 2️⃣ Access Ports (End Devices)
```plaintext
interface Gi1/0/2
 switchport mode access
 switchport access vlan 10   ! PCs

interface Gi1/0/3
 switchport mode access
 switchport access vlan 30   ! IoT

interface Gi1/0/4
 switchport mode access
 switchport access vlan 40   ! Lab
```
### 3️⃣ Verification Commands
```plaintest
show vlan brief         ! Verify VLANs
show interfaces trunk   ! Confirm trunk VLANs
show mac address-table  ! MAC learning per VLAN
show interfaces status  ! Port-to-VLAN mapping
```
---

## 🔹 Troubleshooting Notes
- Issue: PC on VLAN10 did not get internet initially (manual IP configured).
Fix: Switched to DHCP → received correct lease from MikroTik → internet OK.

- Wireless: AP currently runs without VLAN correlation.
Planned: SSID-to-VLAN mapping once AP firmware supports it.

---

## ✅ Current Status
- VLAN segmentation confirmed working
- DHCP functional across all VLANs
- Trunking consistent across MikroTik ↔ Cisco
- Wired clients operational
- Wireless AP functional (flat network, no VLAN mapping yet)

---

## 🔮 Future Work
- Implement inter-VLAN firewall rules for Guest and IoT isolation
- Configure VLAN-to-SSID mapping on TP-Link AP
- Add monitoring/logging for VLAN usage
