# 🏠 Self-Hosted Services for HomeLab

This document outlines recommended self-hosted services to run on the HomeLab cluster. These services provide functionality across **network control, storage, monitoring, security, and convenience**.

---

## 1️⃣ Pi-hole / AdGuard Home
- **What it is:** DNS-based ad blocker and filtering service.
- **Why run it:**  
  - Blocks ads, trackers, and malicious domains across the whole network.  
  - Provides visibility into DNS queries.  
  - Lightweight, easy to run in a container or VM.  

---

## 2️⃣ Reverse Proxy (NGINX Proxy Manager / Traefik / Caddy)
- **What it is:** A gateway for managing all self-hosted services.
- **Why run it:**  
  - Central entry point for multiple services on one public IP.  
  - Easy SSL certificate management (Let’s Encrypt).  
  - User-friendly dashboards for service routing.  

---

## 3️⃣ Nextcloud
- **What it is:** Self-hosted cloud storage and collaboration platform.
- **Why run it:**  
  - Alternative to Google Drive/Dropbox.  
  - Sync and share files, calendars, and contacts.  
  - Integrates with other apps (notes, tasks, password manager).  

---

## 4️⃣ Media Server (Plex / Jellyfin)
- **What it is:** Centralized movie, TV, and music streaming service.
- **Why run it:**  
  - Store and stream media anywhere in the network.  
  - Supports multiple clients (PC, TV, phone).  
  - Plex offers more features, Jellyfin is 100% open source.  

---

## 5️⃣ Password Manager (Vaultwarden)
- **What it is:** Lightweight self-hosted Bitwarden server.
- **Why run it:**  
  - Securely store and manage credentials.  
  - Share access between devices without relying on cloud providers.  
  - Minimal resource usage compared to full Bitwarden server.  

---

## 6️⃣ Monitoring & Metrics (Prometheus + Grafana / Netdata)
- **What it is:** Tools for system metrics collection and visualization.
- **Why run it:**  
  - Monitor resource usage (CPU, RAM, disk, network).  
  - Build dashboards for servers, containers, and network devices.  
  - Early warning on performance issues or failures.  

---

## 7️⃣ Logging (ELK Stack or Loki + Grafana)
- **What it is:** Centralized log collection and analysis.
- **Why run it:**  
  - Aggregate logs from servers, network gear, and services.  
  - Simplifies troubleshooting.  
  - Forms a foundation for future SIEM integration.  

---

## 8️⃣ Threat Intelligence / Security Platform (MISP or OpenCTI)
- **What it is:** Open-source threat intelligence platforms.
- **Why run it:**  
  - Collect, analyze, and share indicators of compromise (IOCs).  
  - Test and integrate with SIEM in a controlled environment.  
  - Great for practicing Blue Team and SOC workflows.  

---

## 9️⃣ Backup System (Restic / Borg / TrueNAS SCALE)
- **What it is:** Data backup and snapshot solutions.
- **Why run it:**  
  - Protect configs, VM images, and important data.  
  - Automate snapshots and off-site replication.  
  - Ensures resilience if hardware or services fail.  

---

## ✅ Summary

These services provide a **solid foundation** for the HomeLab environment:  

- **Network Control:** Pi-hole, Reverse Proxy  
- **Storage & Collaboration:** Nextcloud, Media Server, Vaultwarden  
- **Monitoring & Security:** Grafana/Prometheus, ELK/Loki, Threat Intelligence  
- **Development & Backups:** Git Server, Backup Systems  

As the HomeLab expands, these services will create a flexible, secure, and enterprise-like environment for both **personal use** and **professional learning**.
