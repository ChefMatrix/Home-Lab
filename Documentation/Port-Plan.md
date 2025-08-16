# Port Mapping

Single source of truth for physical port roles. Will try and keep this updated whenever I move cables or change VLANs.

---

## Device Roles (at a glance)

- **RB5009**: Layer-3 gateway (DHCP, inter-VLAN routing, firewall, NAT)
- **Cisco switch**: Layer-2 VLAN fabric (trunks + access)
- **TP-Link AP**: Access Point only (SSIDs mapped to VLANs; DHCP off)

**LAN VLANs** (example plan)
- VLAN 10 — Main LAN — 192.168.10.0/24 — GW 192.168.10.1
- VLAN 20 — Guest — 192.168.20.0/24 — GW 192.168.20.1
- VLAN 30 — IoT — 192.168.30.0/24 — GW 192.168.30.1
- VLAN 40 — Lab — 192.168.40.0/24 — GW 192.168.40.1
- VLAN 99 — Management — 192.168.99.0/24 — GW 192.168.99.1

> WAN is 2degrees Fibre on **ether1** with **ISP VLAN 10 (WAN)**. Don’t confuse with **LAN VLAN 10** above.

---

## MikroTik RB5009 — Port Map

| Port    | Type     | VLANs / Purpose                                               | Notes                              |
|---------|----------|----------------------------------------------------------------|------------------------------------|
| ether1  | WAN      | ISP **VLAN 10 (WAN)** → DHCP client (`wan-vlan10`)            | To ONT                             |
| ether2  | Trunk    | **VLANs 10,20,30,40,99** (to Cisco)                            | Primary LAN uplink                 |
| ether3  | Access   | (optional) Access **VLAN 10**                                  | For a quick wired client           |
| ether4  | Access   | (optional) Access **VLAN 30**                                  | IoT/wired                          |
| ether5  | Access   | (optional) Access **VLAN 99**                                  | Mgmt jump-host                     |
| ether6  | Spare    | —                                                              |                                    |
| ether7  | Spare    | —                                                              |                                    |
| ether8  | Spare    | —                                                              |                                    |
| ether9  | Spare    | —                                                              |                                    |
| SFP+    | (unused) | —                                                              | 10G uplink option in future        |

**RB5009 notes**
- `bridge` has VLAN filtering enabled; VLAN interfaces on `bridge` provide gateways/DHCP.
- NAT rule uses **Out-Interface-List = WAN** (make sure `wan-vlan10` is in WAN list).

---

## Cisco Switch — Port Map

> Adjust interface numbers to your actual switch. Examples assume **Gi1/0/x**.

### Trunks

| Port      | Mode  | Allowed VLANs           | Connected To          | Description                  |
|-----------|-------|-------------------------|-----------------------|------------------------------|
| Gi1/0/48  | Trunk | 10,20,30,40,99          | RB5009 **ether2**     | Core trunk uplink            |
| Gi1/0/47  | Trunk | 10,20,30,40,99          | TP-Link **AP**        | Multi-SSID VLAN trunk        |

### Access Ports (examples)

| Port      | Mode   | Access VLAN | Connected Device     | Description               |
|-----------|--------|-------------|----------------------|---------------------------|
| Gi1/0/10  | Access | 10          | PC / NAS             | Main LAN                  |
| Gi1/0/11  | Access | 30          | IoT hub / camera     | IoT isolated              |
| Gi1/0/12  | Access | 99          | Admin laptop         | Management only           |
| Gi1/0/13  | Access | 20          | Guest wired drop     | Guest internet only       |

**Cisco notes**
- All trunks use `switchport mode trunk` + `switchport trunk allowed vlan 10,20,30,40,99`.
- Access ports use `switchport mode access` + `switchport access vlan <id>`.
- Enable `spanning-tree portfast` on access ports; `portfast trunk` on known trunks.

---

## TP-Link AP — SSID to VLAN Map

| SSID       | VLAN ID | Notes                                 |
|------------|---------|---------------------------------------|
| HomeWiFi   | 10      | Main LAN                              |
| GuestWiFi  | 20      | Internet-only                         |
| IoTWiFi    | 30      | IoT devices; AP Isolation as needed   |
| LabWiFi    | 40      | Lab/testing                           |

**AP notes**
- AP mode, **DHCP disabled**, static mgmt IP (e.g., 192.168.99.x if you move it to Mgmt).
- **Share Network enabled**, **AP Isolation disabled** unless intentionally isolating.
- Uplink to Cisco is a **trunk** carrying the SSID VLANs above.

---
