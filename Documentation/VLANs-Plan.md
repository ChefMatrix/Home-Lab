# VLAN Plan

This document outlines the VLAN segmentation plan for the Home Lab network.  
All VLANs are terminated on the MikroTik RB5009, which handles DHCP, routing, and firewall rules.  
The Cisco switch provides VLAN-aware Layer 2 distribution, and the TP-Link Wi-Fi AP maps SSIDs to VLANs via trunking.

---

## VLAN Overview

| VLAN ID | Name       | Subnet          | Gateway IP      | DHCP Pool                 | Purpose                      |
|---------|------------|-----------------|-----------------|---------------------------|------------------------------|
| 10      | Main LAN   | 192.168.10.0/24 | 192.168.10.1    | 192.168.10.100–192.168.10.199 | Trusted PCs, wired LAN      |
| 20      | Guest      | 192.168.20.0/24 | 192.168.20.1    | 192.168.20.100–192.168.20.199 | Guest Wi-Fi                 |
| 30      | IoT        | 192.168.30.0/24 | 192.168.30.1    | 192.168.30.100–192.168.30.199 | Smart home / IoT devices    |
| 40      | Lab        | 192.168.40.0/24 | 192.168.40.1    | 192.168.40.100–192.168.40.199 | Testing / penetration lab   |
| 99      | Management | 192.168.99.0/24 | 192.168.99.1    | 192.168.99.50–192.168.99.99   | Router, Switch, AP mgmt     |

---

## SSID Mapping

| SSID        | VLAN ID | Subnet          | Notes                          |
|-------------|---------|-----------------|--------------------------------|
| HomeWiFi    | 10      | 192.168.10.0/24 | Main trusted wireless          |
| GuestWiFi   | 20      | 192.168.20.0/24 | Internet-only guest network    |
| IoTWiFi     | 30      | 192.168.30.0/24 | IoT devices isolated from LAN  |
| LabWiFi     | 40      | 192.168.40.0/24 | Lab/Testing wireless           |

---

## Cisco Port Mapping

| Cisco Port | Mode   | VLAN(s) | Purpose                   |
|------------|--------|---------|---------------------------|
| Gi1/0/48   | Trunk  | 10,20,30,40,99 | Uplink to MikroTik ether2 |
| Gi1/0/47   | Trunk  | 10,20,30,40    | Trunk to TP-Link AP       |
| Gi1/0/10   | Access | 10      | Wired PC                  |
| Gi1/0/11   | Access | 30      | IoT device (wired)        |
| Gi1/0/12   | Access | 99      | Mgmt (Cisco/AP admin)     |

---

## Notes
- MikroTik RB5009 handles inter-VLAN routing, DHCP, and firewall policies.
- Cisco switch operates at Layer 2, providing VLAN trunks and access ports.
- TP-Link AP operates in AP mode; SSIDs are mapped to VLANs via trunk.
- Firewall rules will enforce segmentation (e.g., IoT/Guest blocked from Main).
