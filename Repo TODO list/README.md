# Need to do:
## 4. Config snippets (Winbox/CLI) with “How to reproduce”
Create `/Configuration/mikrotik.md` and `/Configuration/cisco.md` with copy‑pastable snippets (DHCP client on wan-vlan10, bridge VLAN filtering, VLAN interfaces, pools, NAT, firewall; on Cisco: trunk + access examples). You already have a Configuration/ dir—perfect place for it. 

## 5. Ops notes: issues + fixes you hit
Turn your troubleshooting from this setup into `/Networking Journal/2025‑08‑RB5009‑AP‑VLAN‑notes.md`:
- TP‑Link AP mode + “Share Network”
- AP Isolation caused no‑internet on Wi‑Fi
- TP‑Link lost static IP → found via DHCP leases
You’ve got a `Networking Journal/` folder—use it as a changelog/ops log.

## 6. Backups & exports
Add a `/Configuration/backups/` (sanitized) and note where RouterOS `backups/exports` and Cisco show run are stored; include a one‑liner on how to restore.
