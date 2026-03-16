# Docker

All services on this server run in Docker containers managed with Docker Compose. I went with Docker because it keeps each service isolated.

Each service lives in its own folder with a `docker-compose.yml`. Data is stored in volumes on the RAID array at /srv/storage, which means containers can be deleted and recreated without losing anything.

## Why Docker Compose instead of plain `docker run`
 
Running a container with `docker run` works, but the command gets long fast and disappears when the terminal closes. Compose puts everything in a file that stays on disk, can be version-controlled, and is easy to read back later.
 
Instead of:
```bash
docker run -d -p 8096:8096 -v /srv/storage/media:/media --restart unless-stopped jellyfin/jellyfin
```
 
You write it once in `docker-compose.yml` and just run `docker compose up -d` every time.

## Installation

Docker was installed following the official apt repository method from the Docker documentation.

```bash
# Add Docker's official GPG key and repository
sudo apt-get install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Docker Engine and Compose plugin
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Allow running Docker without sudo
sudo usermod -aG docker $USER
```
