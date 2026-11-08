# 🏠 Ultra-Lightweight Homelab (HP EliteBook 8440p)

A bare-metal, self-hosted home server running on repurposed hardware. This project demonstrates how to run a functional media and network stack on extreme hardware constraints (2GB RAM) without the overhead of Docker.

## 🖥️ Hardware & Environment
- **Device**: HP EliteBook 8440p (Repurposed Laptop)
- **CPU**: Intel Core i5 with vPro
- **RAM**: 2GB (Strict memory management required)
- **Power**: AC only (No battery; immediate shutdown on power loss)
- **OS**: Debian 13 (Headless / CLI only)
- **User**: `sambid` @ `Sam-server`

## 🚀 Bare-Metal Services
1. **OpenSSH**: Secure remote CLI access.
2. **AdGuard Home**: Network-wide DNS ad-blocking and privacy protection.
3. **Netdata**: Real-time, low-overhead performance and health monitoring.
4. **Navidrome**: Lightweight, self-hosted music streaming server.
5. **slskd**: SoulSeek daemon for music discovery and direct library integration.

## ⚙️ Design Philosophy
- **No Docker**: The 2GB RAM limit makes containerization overhead prohibitive. All services run natively (bare-metal).
- **Shared Media Library**: `slskd` downloads directly into the directory monitored by `Navidrome` for seamless, ad-free music discovery and playback.
- **Resilience**: Equipped with `zram-tools`, `earlyoom`, `fail2ban`, and `unattended-upgrades` to maximize stability and security.

## 📚 Documentation
- [Troubleshooting Guide](docs/troubleshooting.md) - Solutions to common pitfalls (e.g., slskd YAML schema changes, Navidrome path mismatches).
- [Security & Maintenance](docs/security.md) - Hardening the server and managing the no-battery risk.

---
*Built with patience, terminal commands, and a lot of `journalctl`.*
