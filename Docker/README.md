# Docker

All services on this server run in Docker containers managed with Docker Compose. I went with Docker because it keeps each service isolated.

Each service lives in its own folder with a `docker-compose.yml`. All data is stored in volumes on the RAID array at `/srv/storage`, so containers are disposable but data is not.

## Why Docker Compose over plain Docker

Running containers with `docker run` works fine for quick tests, but Compose lets me define everything in a file — ports, volumes, restart policy — and check it into version control. It also makes it easier to manage multiple containers that depend on each other.

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
