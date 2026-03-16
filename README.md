# Homelab

Personal homelab running on Ubuntu Server 24.04 LTS. Built for self-hosting, learning Linux administration, and hands-on experience with networking and containerization.

## Hardware

- **CPU:** AMD FX-8320 (8 cores)
- **RAM:** 22GB DDR3
- **OS Disk:** 223.6GB SSD
- **Storage:** 3x 931.5GB HDDs in RAID1

## Services

- **Jellyfin** — media streaming server
- **Samba** — NAS / LAN file sharing
- **Pi-hole** — DNS server and network-wide ad blocking
- **Nginx Proxy Manager** — reverse proxy for all services
- **Uptime Kuma** — service monitoring
- **Tailscale** — remote access VPN

Each service has its own folder with a README and `docker-compose.yml`.

## Storage

Three drives configured in a RAID1 (mirroring) array using `mdadm`. RAID1 was chosen for redundancy — if one drive fails, data is intact on the remaining drives. Mounted at `/mnt/storage`.

## Security

- SSH key authentication only (password login disabled)
- UFW firewall, allowing only necessary ports
- Remote access via Tailscale VPN
