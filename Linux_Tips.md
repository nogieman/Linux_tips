Fish stuff:::
random -- generate random numbers
prevd, nextd --> navigate through directories
ctrl+l = clear
alt + l = ls

Setting mysql::
download mysql-server
marianadb

--------------------

chmod +x "Name" ---> to make a file executable

________________________

USING GPU IN PYCHARM

add the code before everything: 
###

import torch

# GPU availability
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

###


Paste themes folder in /usr/share

________________________

Use OhMyZsh!

____________________________

GPU Drivers in linux:

Follow this: https://wiki.debian.org/NvidiaGraphicsDrivers#trixie-535

and don't forget to check if you're using wayland or X11

______________________________

Boot up issues!

If dkms failed, look tips in this chat: https://chatgpt.com/share/68452241-34a4-8008-bba3-4fa8aa390c16

WAYLAND CRASHED FOR SOME REASON!!!

BACK TO X11 ON 13TH JUNE 2025

______________________________

INSTALLING DOCKER AND CONFIG AND REMOVAL :: FROM ChatGPT chat: (:: Train indicates start and end of gpt canvas file)
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

# Docker Setup, Usage, and Cleanup Guide

This guide contains a complete sequence of shell commands (with brief explanations) for installing Docker, running GUI apps inside a container, and fully cleaning up Docker afterwards. Suitable for Debian/Ubuntu-based systems.

---

## 🚀 Docker Installation

```bash
# Update package index
sudo apt update

# Install packages needed to use apt over HTTPS
sudo apt install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Add Docker's official GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Set up the Docker repository
echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update and install Docker packages
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Check Docker version
docker --version
```

---

## 🧑‍🔧 Post-install Configuration

```bash
# Add your user to the docker group (so you can run without sudo)
sudo usermod -aG docker $USER

# You MUST log out and back in for this to take effect
```

To test:

```bash
docker run hello-world
```

---

## 🐳 Dockerfile Example for Efinity GUI

**Dockerfile**:

```Dockerfile
FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y \
    x11-apps libgl1 libx11-xcb1 libxcb1 libxrender1 libxcb-glx0 \
    libxkbcommon-x11-0 libgtk-3-0 libnss3 libdbus-glib-1-2 \
    libasound2 libatk-bridge2.0-0 python3 unzip wget sudo \
    libfontconfig1 libxss1 libglu1-mesa libxcb-xinerama0 \
    && apt clean && rm -rf /var/lib/apt/lists/*

# Optional: add a user
RUN useradd -m efxuser && echo "efxuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER efxuser
WORKDIR /home/efxuser

CMD ["bash"]
```

Build image:

```bash
docker build -t efinity-docker .
```

---

## 🖼️ Running GUI Apps in Docker (X11)

```bash
# Allow Docker containers to access host X server
xhost +local:docker

# Run Docker container with display forwarding
# (replace /opt/efinix with your mounted path)
docker run -it \
  --env DISPLAY=$DISPLAY \
  --env QT_X11_NO_MITSHM=1 \
  --env LIBGL_ALWAYS_INDIRECT=1 \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume /opt/efinix:/opt/efinix \
  --privileged \
  --cap-add=SYS_PTRACE \
  --security-opt seccomp=unconfined \
  efinity-docker \
  bash
```

Inside container, run GUI app:

```bash
cd /opt/efinix/efinity/2024.1/bin
./efinity
```

---

## 🧹 Full Docker Cleanup

```bash
# Stop all running containers
docker ps -q | xargs -r docker stop

# Remove all containers
docker container prune -f

# Remove all images
docker image prune -a -f

# Remove all volumes
docker volume prune -f

# Remove Docker itself
sudo apt purge -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo apt autoremove -y

# Optional: Remove Docker-related directories
sudo rm -rf /var/lib/docker /etc/docker /var/run/docker.sock
```

You may also want to remove the `docker` group:

```bash
sudo groupdel docker
```

---

✅ **Done!** This file helps you redo or reverse your Docker setup later. Save and keep it safe.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
_______________________________________________________________________________________
