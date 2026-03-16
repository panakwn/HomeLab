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
- **Netdata** — server monitoring, HDD health, and email alerts
- **Uptime Kuma** — service uptime monitoring
- **Home Assistant** — home automation
- **Zigbee2MQTT + Mosquitto** — Zigbee device integration via MQTT
- **WireGuard** — self-hosted VPN for remote access

(Each service has its own folder with a README explaining the setup and a "docker-compose.yml")

## IoT & Automation
 
Home Assistant runs alongside a Zigbee coordinator (Sonoff ZBDongle-E) and a small network of Zigbee devices — motion/presence sensors, door sensors, and smart bulbs. Device communication goes through Zigbee2MQTT and a local Mosquitto MQTT broker, keeping everything local with no cloud dependency.
 
A separate ESP32-based project controls the power and reset buttons of a PC remotely via Home Assistant.

## Hardware

- **CPU:** AMD FX-8320 (8 cores)
- **RAM:** 22GB DDR3
- **OS Disk:** 223.6GB SSD (Ubuntu Server)
- **Storage:** 3x 931.5GB HDDs (in RAID1)
