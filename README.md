# Home-Lab
This repository serves as a central hub for documenting my home lab setup and ongoing projects.

# 🏠 HomeLab: My Home Network & Server Infrastructure

Welcome to my homelab documentation. This project showcases how I built, configured, and continuously improved my personal home server setup using Proxmox, Nextcloud, Docker, and more. It's designed for learning, experimentation, and practical self-hosting.

---

## 🧰 Hardware

- **Old Desktop PC**
  - CPU: Intel i7
  - GPU: NVIDIA GTX 1070
  - RAM: 16GB DDR4
  - Storage:
    - 1TB SSD (OS/VMs)
    - 12TB HDD + 6TB HDD (bulk storage)

---
## 🗺️ Network Map
Here is a rough network diagram which I have created. This is still a WIP, as I am still continuing my learning into CCNA and soon CCNP. The network diagram version will change through out my learning. 

Here is the current version:

![Network Map V2](Images/Home%20Network%20Map%20V2.drawio%20(2).png)

---

## ⚙️ Virtualization Platform

### 🔧 Proxmox VE
- Installed via bootable USB
- Installed on 1TB SSD
- Configured with static IP
- Web UI access for VM/container management

---

## 📦 Services Deployed

### 📁 Nextcloud (VM)
- Ubuntu Server 20.04 LTS
- Apache, PHP, MariaDB stack
- Installed Nextcloud manually
- SSL enabled with Let's Encrypt

### 📄 ONLYOFFICE Document Server (Docker)
- Deployed via Docker
- Environment variables configured for JWT and SSL.
- Integrated with Nextcloud

