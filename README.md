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
- Runs on ports `9080` (HTTP) and `9443` (HTTPS)
- Environment variables configured for JWT and SSL
- Integrated with Nextcloud

