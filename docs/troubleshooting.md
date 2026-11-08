# 🛠️ Troubleshooting & Lessons Learned

This document records the specific challenges faced and solved during the setup of this 2GB RAM homelab.

## 1. The `slskd` Configuration Loop
**Problem**: The `slskd.service` would continuously fail to start, showing `Inactive (dead)` in systemd.
**Root Causes & Solutions**:
- **Non-existent directories**: The config pointed to `/home/sambid/Music/Soulseek/incomplete` before the folders were created. *Fix*: `mkdir -p` for all required directories.
- **Invalid `ContentPath`**: The YAML required a relative path for the web root. *Fix*: Changed to `contentPath: "wwwroot"` and set `WorkingDirectory=/opt/slskd` in the systemd service.
- **YAML Schema Changes**: Newer versions of slskd moved the `global` and `groups` keys, causing silent failures. *Fix*: Updated the `.yml` template to match the latest schema.

## 2. Navidrome "Missing Music" After slskd Setup
**Problem**: Navidrome suddenly couldn't find the music library.
**Root Cause**: During the `slskd` directory restructuring, the base music folder path was altered or permissions were changed.
**Fix**: Ensured both `slskd` (downloads) and `Navidrome` (scan path) point to the exact same absolute path (e.g., `/home/sambid/Music`), and verified that the `sambid` user has read/write permissions to it.

## 3. Memory Pressure (2GB RAM)
**Problem**: Occasional system freezes when multiple services spike.
**Fix**: Installed and configured `zram-tools` (to compress RAM) and `earlyoom` (to gracefully kill non-essential processes before the kernel panics). Avoided all Docker containers to save ~300-500MB of baseline overhead.
