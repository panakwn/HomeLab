# Homelab

This is my personal homelab — an old desktop repurposed as a home server. I built it mainly to self-host my media and have a NAS, but it's also where I learn and experiment with Linux, networking, and Docker.

## Security

- SSH key authentication only (password login disabled)
- UFW firewall, allowing only necessary ports
- Remote access via WireGuard VPN only

## Services

- **Samba** — NAS / LAN file sharing
- **Pi-hole** — DNS server and network-wide ad blocking
- **Jellyfin** — media streaming server
- **Nginx Proxy Manager** — reverse proxy for all services
- **Uptime Kuma** — service monitoring
- **WireGuard** — remote access VPN

(Each service has its own folder with a README explaining the setup and a "docker-compose.yml")

## Hardware

- **CPU:** AMD FX-8320 (8 cores)
- **RAM:** 22GB DDR3
- **OS Disk:** 223.6GB SSD (Ubuntu Server)
- **Storage:** 3x 931.5GB HDDs (in RAID1)
