# 🛡️ Security & Maintenance

This document outlines the security hardening and maintenance routines applied to this 2GB RAM bare-metal homelab to ensure stability, privacy, and resilience.

## 🔒 Network Security (UFW)
The Uncomplicated Firewall (UFW) is enabled and configured to deny all incoming traffic by default, only allowing explicitly required services.

**Allowed Ports:**
- `22/tcp`: SSH (Remote management)
- `53/tcp`, `53/udp`: DNS (AdGuard Home)
- `80/tcp`, `443/tcp`: HTTP/HTTPS (AdGuard Home Web UI)
- `4533/tcp`: Navidrome (Music streaming)
- `5030/tcp`: slskd (SoulSeek Web UI - *Note: Keep this restricted to local LAN*)

**Commands applied:**
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp comment 'SSH'
sudo ufw allow 53/tcp comment 'AdGuard DNS'
sudo ufw allow 53/udp comment 'AdGuard DNS'
sudo ufw allow 80/tcp comment 'AdGuard Web'
sudo ufw allow 443/tcp comment 'AdGuard Web HTTPS'
sudo ufw allow 4533/tcp comment 'Navidrome'
sudo ufw allow 5030/tcp comment 'slskd Web UI'
sudo ufw enable
