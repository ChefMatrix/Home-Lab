# 🧾 2025-09-03 – Cloudflare Tunnel & Authelia Setup

Today was a reasonably busy day working on my HomeLab. A lot of it was laying down the **fundamentals** for future services.

---

## 🌐 Cloudflare Tunnel & DNS

Before starting with Authelia, I first configured a **Cloudflare Tunnel**.  
- Purpose: expose services to the internet **without opening ports** (a safer approach for home networks, especially in cybersecurity).  
- DNS setup: I added subdomains like `auth.mydomain.com` and `whoami.mydomain.com` in Cloudflare, pointing them to the same tunnel.  
- Each hostname forwards traffic internally to **Traefik** (reverse proxy) on port 80.

### 🛠 Issue Encountered – Error 530
- Initially, I kept hitting a **530 error** (Cloudflare: hostname not attached properly).  
- Cause: I had created **two separate tunnels**.  
- Fix: consolidated everything into a **single tunnel** and re-attached hostnames → resolved.

---

## 🔀 Internal Reverse Proxy (Traefik)

Configured **Traefik** to handle all requests coming from Cloudflare Tunnel:  
- Routes traffic based on host headers to the correct containers.  
- Manages middlewares (e.g., routing `auth.mydomain.com` to Authelia).  
- Keeps all apps managed in one central location.

---

## 🔒 Authelia Setup (Work in Progress)

Started deploying **Authelia**, a free open-source authentication server.  
- GUI / web interface is up and running.  
- Current blocker: not receiving the **one-time password (OTP)** required for initial configuration.  

### Troubleshooting
- Searching forums, docs, and using ChatGPT for fixes.  
- Next step: integrate Authelia with Traefik so that:  
  - Cloudflare secures the **edge**.  
  - Authelia enforces **2FA and authentication** before apps are accessible.  

---

## ⏳ End of Day Thoughts

By the end of the day (technically **12:16 AM**), I had Cloudflare Tunnel, DNS, and Traefik functioning well. Authelia is partly working but not yet fully configured.  

The plan is to finish the authentication layer soon, so the HomeLab has **edge protection (Cloudflare)** and **application-level security (Authelia)** combined.
