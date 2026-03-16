# Samba

Network file sharing over the local network, giving access to the storage array from any device (Windows, Linux, macOS).

## Access

- Windows: `\\192.168.1.10\files`
- Linux/macOS: `smb://192.168.1.10/files`

## Storage

The share maps to `/srv/storage/files` on the RAID array. The Jellyfin media library lives inside this share at `files/Jellyfin/`.

## docker-compose.yml

```yaml
services:
  samba:
    image: dperson/samba
    container_name: samba
    ports:
      - "445:445"
      - "139:139"
    volumes:
      - /srv/storage/files:/share
    environment:
      - SHARE=files;/share;yes;no;no;all
      - USER=panakwn;<password>
    restart: unless-stopped
```

## Notes

- `/srv/storage/files` needs `chmod 777` for the container to write files correctly
- Password in the compose file is the Samba share password, separate from the system user password
