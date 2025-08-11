# ⚙️ MikroTik RB5009 VLAN Design & Setup Guide

## 📜 Overview
This document outlines the VLAN design and configuration steps for the MikroTik RB5009 in a **router-on-a-stick** topology, with a Cisco switch providing the Layer 2 VLAN fabric and a TP-Link Wi-Fi 7 AP for wireless coverage.

---

## 🗂 VLAN Plan

| VLAN ID | Name        | Subnet             | MikroTik IP (GW) | DHCP Pool Range                | Use Case                          |
|---------|------------|--------------------|------------------|---------------------------------|------------------------------------|
| 10      | Main LAN   | 192.168.10.0/24     | 192.168.10.1     | 192.168.10.100–192.168.10.199  | PCs, trusted devices              |
| 20      | Guest      | 192.168.20.0/24     | 192.168.20.1     | 192.168.20.100–192.168.20.199  | Guest Wi-Fi                       |
| 30      | IoT        | 192.168.30.0/24     | 192.168.30.1     | 192.168.30.100–192.168.30.199  | Smart/IoT devices                 |
| 40      | Lab        | 192.168.40.0/24     | 192.168.40.1     | 192.168.40.100–192.168.40.199  | Testing / Pentesting              |
| 99      | Management | 192.168.99.0/24     | 192.168.99.1     | 192.168.99.50–192.168.99.99    | Router, switch, AP management     |

> **Note:** The ISP WAN uses VLAN ID `10` on `ether1` for the upstream connection (wan-vlan10). These VLAN IDs are for **LAN** use and can be changed (e.g., 100/200/300/400/999) to avoid overlap with the WAN VLAN.

---

TODO: Add Diagram of the segmentation of Vlans and IP assignment

---

## 🖥 Topology (Ports)

- **RB5009 ether1 → ONT** (WAN: `wan-vlan10`, DHCP client)
- **RB5009 ether2 → Cisco switch uplink** (802.1Q trunk, carrying VLANs 10/20/30/40/99)
- **Cisco switch → Access ports** for wired devices
- **Cisco trunk to TP-Link AP**
  - **Option A:** Trunk, map SSIDs to VLANs
  - **Option B:** Single SSID, access port on chosen VLAN (e.g., Main LAN)

---

## 🛠 MikroTik Configuration (Winbox)

### 1️⃣ Enable Bridge VLAN Filtering
- **Bridge → Bridge** → double-click bridge → **VLAN tab** → `VLAN Filtering = Yes`
- **Bridge → Ports:** Ensure all LAN ports (e.g., ether2 to Cisco) are members of the bridge.

---

### 2️⃣ Create VLAN Interfaces
Repeat for each LAN VLAN:

**Interfaces → VLAN → “+”**
- **Name:** `vlan10-main` (or `vlan100-main` if avoiding WAN overlap)
- **VLAN ID:** `10`
- **Interface:** `bridge`

Repeat for VLANs 20, 30, 40, 99.

---

### 3️⃣ Assign IP Addresses
**IP → Addresses → “+”**

| VLAN Interface | Address         |
|----------------|-----------------|
| vlan10-main    | 192.168.10.1/24 |
| vlan20-guest   | 192.168.20.1/24 |
| vlan30-iot     | 192.168.30.1/24 |
| vlan40-lab     | 192.168.40.1/24 |
| vlan99-mgmt    | 192.168.99.1/24 |

---

### 4️⃣ Configure DHCP Servers
For each VLAN:

- **IP → Pools → “+”**
  - **Name:** `pool-main`
  - **Range:** e.g., `192.168.10.100-192.168.10.199`

- **IP → DHCP Server → “+”**
  - **Name:** `dhcp-main`
  - **Interface:** `vlan10-main`
  - **Address Pool:** `pool-main`

- **IP → DHCP Server → Networks → “+”**
  - **Address:** `192.168.10.0/24`
  - **Gateway:** `192.168.10.1`
  - **DNS:** `192.168.10.1` (and/or `1.1.1.1`)

Repeat for VLANs 20, 30, 40, 99.

---

### 5️⃣ Define VLAN Tagging
**Bridge → VLANs → “+”**
- **VLAN ID:** 10
- **Tagged:** `bridge`, `ether2` (uplink to Cisco)
- **Untagged:** None (untagged done on Cisco access ports)

Repeat for VLANs 20, 30, 40, 99.

---

### 6️⃣ Interface Lists & NAT
- **Interfaces → Interface List → WAN:** Ensure `wan-vlan10` is present.
- **Interfaces → Interface List → LAN:** Ensure `bridge` is present.
- **IP → Firewall → NAT:** One `srcnat` rule, **Out-Interface-List = WAN**, action = `masquerade`.

---

### 7️⃣ Basic Inter-VLAN Firewall Rules
1. **Allow Established/Related**
2. **Drop Invalid**
3. **Block IoT/Guest → Main LAN**
   - `src-address=192.168.30.0/24` → `dst-address=192.168.10.0/24` → drop
   - `src-address=192.168.20.0/24` → `dst-address=192.168.10.0/24` → drop
4. **Allow IoT/Guest → WAN** (default forward + NAT covers this)
5. **Allow Management → All** (or restrict as needed)

---

## 📌 Notes
- VLAN routing and firewalling are handled entirely by the RB5009.
- The Cisco switch remains Layer 2 only.
- If needed, VLAN IDs can be rebased to avoid WAN conflicts.

---

**Next Step:** Configure Cisco switch trunk and access ports to match this VLAN plan.
