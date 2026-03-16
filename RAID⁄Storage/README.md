# NAS & Storage

Network attached storage powered by a 3-drive RAID1 array, shared over the local network via Samba.

## Storage

Three 931.5GB drives configured in a RAID1 (mirroring) array using Linux's software RAID (`mdadm`).

RAID1 was chosen for redundancy — if one drive fails, data remains intact on the other two. The trade-off is that usable capacity equals one drive's size (~931GB).

The array is mounted at `/srv/storage` with two subdirectories:

- `media/` — used by Jellyfin for movies, series, and music
- `files/` — general file storage, shared over the network via Samba

## Why software RAID over hardware RAID

Software RAID via `mdadm` was chosen over a dedicated hardware RAID controller because it's transparent — the array state is readable directly from the OS, easier to debug, and not tied to proprietary hardware. If the controller fails, the array can be rebuilt on any Linux machine.

## Setup

**1. Verify drives are detected**
```bash
lsblk
```

**2. Check array health**
```bash
cat /proc/mdstat
```
A healthy array shows `[3/3] [UUU]`.

**3. Format the array**
```bash
sudo mkfs.ext4 /dev/md0
```

**4. Mount**
```bash
sudo mkdir -p /srv/storage/media
sudo mkdir -p /srv/storage/files
sudo mount /dev/md0 /srv/storage
```

**5. Auto-mount on boot via `/etc/fstab`**

UUID is used instead of device name (e.g. `/dev/sda`) because device names can change between reboots.
```bash
UUID=<your-uuid> /srv/storage ext4 defaults 0 2
```

## File Sharing

Samba runs in Docker and shares `/srv/storage/files` over the local network. See [`docker-compose.yml`](docker-compose.yml) for the full configuration.
