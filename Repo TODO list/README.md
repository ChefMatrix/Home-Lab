# Need to do:
## 3. Port mapping sheets
Add `/Documentation/Ports.md` mapping:
- RB5009: ether1=WAN (vlan10 ISP), ether2=trunk to Cisco (allowed VLANs), ether3+=access (if any)
- Cisco: list trunk ports (to RB5009/AP) + access ports with their VLANs
This saves hours later when you forget which port does what.

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
