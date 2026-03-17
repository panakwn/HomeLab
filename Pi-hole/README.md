# Pi-hole

Network-wide DNS server and ad blocker. All DNS queries from devices on the local network pass through Pi-hole, which blocks requests to known ad and tracking domains before they reach the internet.

## Why Pi-hole instead of a browser extension

Browser extensions only block ads in the browser. Pi-hole blocks at the DNS level — ads are blocked on every device on the network, including phones, smart TVs, and apps, without installing anything on each device.

## Access

- Dashboard: `http://192.168.1.10/admin`

## How it works

The router's DHCP server is configured to hand out `192.168.1.10` as the DNS server for all devices. When a device tries to resolve a domain that's on the blocklist, Pi-hole returns an empty response instead of the real IP — the request never leaves the network.

Upstream DNS (for legitimate queries) is Google (`8.8.8.8` / `8.8.4.4`).

## Setup notes

- Pi-hole v6 requires `network_mode: host` in Docker so it can bind directly to port 53 on the host
- `systemd-resolved` must be disabled on the server before running Pi-hole, otherwise port 53 is already in use
- After disabling `systemd-resolved`, a static `nameserver 8.8.8.8` entry is added to `/etc/resolv.conf` so the server itself still has DNS

## docker-compose.yml

```yaml
services:
  pihole:
    image: pihole/pihole
    container_name: pihole
    network_mode: host
    environment:
      - TZ=Europe/Athens
      - FTLCONF_webserver_api_password=<password>
    volumes:
      - /srv/storage/pihole-config/etc:/etc/pihole
      - /srv/storage/pihole-config/dnsmasq:/etc/dnsmasq.d
    restart: unless-stopped
```
