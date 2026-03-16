# Jellyfin
 
Self-hosted media server for streaming movies, series, and music across the local network and remotely via WireGuard.
 
## Why Jellyfin
 
Jellyfin is fully open source and runs entirely locally — no subscription, no account required, no data leaving the network.
 
## Access
 
- Local: `http://192.168.1.10:8096`
- Remote: same address via WireGuard VPN
 
## Storage
 
Media files are stored on the RAID1 array at `/srv/storage/media`. The Jellyfin config (metadata, users, settings) is stored at `/srv/storage/jellyfin-config`, so it survives container recreation.
 
## docker-compose.yml
 
```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    ports:
      - "8096:8096"
    volumes:
      - /srv/storage/media:/media
      - /srv/storage/jellyfin-config:/config
    restart: unless-stopped
```
