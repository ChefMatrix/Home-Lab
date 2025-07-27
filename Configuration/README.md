# ⚙️ Configuration Files

This directory documents the **device-specific configurations** within my HomeLab infrastructure. It is structured by vendor to reflect the real-world layout of my network and offers version-controlled insights into the configuration of each component.

Each subdirectory contains configurations, commands, and notes tailored to that specific device type.

---

## 🗂️ Folder Structure

| Vendor     | Description                                                 |
|------------|-------------------------------------------------------------|
| [`Cisco/`](./Cisco)       | Configuration files and CLI logs for Cisco Layer 2 switches (e.g., VLANs, port security, trunking) |
| [`MikroTik/`](./MikroTik) | Core router configuration (planned). Will include routing, NAT, inter-VLAN routing, firewall rules |
| [`TPLink/`](./TPLink)     | Current gateway/router configuration. Includes basic network setup and wireless profiles |

---

## 🧭 Purpose

Maintaining clear and modular documentation for configurations ensures:

- 🔄 **Reproducibility** — Reconfigure or restore devices quickly
- 📚 **Learning** — Understand the impact of each setting as part of my CCNA/CCNP studies
- 📜 **Change Tracking** — Easily track version changes and rollback if needed
- 🔐 **Security Hardening** — Document security baselines and audits

---

> 📌 Each folder includes its own `README.md` summarizing the device, role, and relevant command sets.
