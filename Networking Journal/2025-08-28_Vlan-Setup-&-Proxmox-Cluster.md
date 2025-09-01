# 🧾 2025-08-10 – VLAN Setup, Proxmox Cluster & Networking Progress

After configuring the VLANs in my network and establishing five distinct VLANs, I now have:

- **Main VLAN** for the trusted devices and network.
- **IoT VLAN** for all my smart devices.
- **Guest VLAN** for visitors and non-critical devices.
- **Lab VLAN** for testing and pentesting environments.
- **Management VLAN** for the management of routers, switches, and APs.

### 🎯 Challenges & Learning

Setting this up was a bit tricky and complicated, mainly because I had to get familiar with the router OS format, the UI, and refine my understanding of networking. But thankfully, everything is now working, and I have internet connectivity across the VLANs in my network. I’ve also set up subnetting, which feels great.

### ⚠️ Issues Encountered

One of the issues I encountered was with my PC, which had a manual IP set. I spent around an hour trying to figure out why I wasn’t getting internet access, only to realize it was stuck on a manual IP in the `0.88` range. That was a funny but frustrating moment once I figured it out.

---

### 🖥 New Micro PC Setup

Currently, I’ve bought a **new micro PC** — a solid **i5 with 8GB of RAM** and **500GB of storage**. This will be the first part of my cluster. I already have an old PC that I used to own, which is now set up with **Proxmox**, and I’m adding this new micro PC to the cluster. Over time, I plan to keep expanding the cluster, which is pretty exciting!

---

### 🔐 Proxmox Setup & Next Steps

Right now, I’ve **successfully set up** my **Proxmox server**, and it’s running well. I’ve configured the firewall between the LAN and the network to allow access from my PC. The next steps are to configure the Proxmox environment to interact with my **home lab**.

I’ll be adding things like:
- **Pi-hole** for ad-blocking.
- **Retainer** for backup solutions.
- **Nginx proxy** for reverse proxy management.
- **NextCloud** for self-hosted cloud services.

### 🧠 Long-Term Goals

I also plan to integrate my **Threat Intelligence** and **SIEM network** into the environment, to explore what I can do with them and how far I can expand this side of the network.

---

### ✅ Current Status

- **VLANs:** Configured and functional.
- **Proxmox server:** Set up and running.
- **Cluster:** Starting with the first micro PC, with plans to expand.
- **Next Steps:** Configuring home lab services (Pi-hole, Nginx, NextCloud, etc.), and integrating Threat Intelligence.
