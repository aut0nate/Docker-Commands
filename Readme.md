# Docker Commands Cheatsheet

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

This repository contains a collection of Docker commands that I’ve found particularly useful as part of my learning process. I have grouped these into categories for easy reference.

---

## Contents

- [Image Search & Management](#image-search--management)
- [Container Lifecycle](#container-lifecycle)
- [Running Containers](#running-containers)
- [Container & Image Cleanup](#container--image-cleanup)
- [Logs & Monitoring](#logs--monitoring)
- [Inspecting & Debugging](#inspecting--debugging)
- [Authentication & Registry](#authentication--registry)

---

## Image Search & Management

```bash
# Search for Docker images matching the specified name
docker search <image>

# Search for Docker images with at least 100 stars
docker search --filter stars=100 <image>

# Search for official Docker images with at least 100 stars
docker search --filter is-official=true --filter stars=100 <image>

# Limit search results to 5
docker search --limit 5 <image>

# Format search output to show name and star count in a table
docker search --format "table {{.Name}}\t{{.StarCount}}" <image>

# Download (pull) an image from a registry
docker pull <image_name>

# List all Docker images
docker image ls --all

# List all Docker images without truncating output
docker image ls --no-trunc

# List images filtered by label
docker image ls --filter label="<label_key>=<label_value>"

# List all image IDs only
docker image ls --quiet

# Remove an image
docker rmi <image_name_or_id>

# Tag a local image with a new name and tag
docker tag <name_of_image> <docker_username>/<image_name>:<tag>

# Build an image from a Dockerfile in the current directory
docker build -t <image_name>:<tag> .

# Build an image from a specific Dockerfile
docker build -t <image_name>:<tag> -f <docker_file> .
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---

## Container Lifecycle

```bash
# Create a new container from an image (but do not start it)
docker container create <image_name>

# Start a container by name or ID
docker container start <container_name_or_id>

# Start and attach to a container
docker container start --attach <container_name_or_id>

# Stop a running container
docker stop <container_name_or_id>

# Stop a container immediately (timeout 0)
docker stop -t 0 <container_name_or_id>

# Forcefully kill a running container
docker kill <container_id>

# Remove a stopped container
docker rm <container_name_or_id>

# Force remove a container (running or stopped)
docker rm -f <container_name_or_id>

# Remove containers with a status of exited
docker rm $(docker ps -aq -f status=exited)

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---

## Running Containers

```bash
# Run an image (downloads if not present)
docker run <image_name>

# Run an image and name the container
docker run --name '<container_name>' <image_name>

# Run a container in detached mode (background)
docker run -d <image_name>

# Run a container in detached mode and map ports
docker run -d -p <host_port>:<container_port> --name <container_name> <image_name>

# Run an interactive shell session in a Linux container
docker run -it <linux_distro> /bin/sh

# Run a container, execute commands, and remove after exit
docker run --rm --entrypoint sh -v <host_directory>:/tmp/ <image_name> -c "echo '<text_to_write>' > /tmp/file && cat /tmp/file"

# Run an Nginx container named 'website', map local folder to web root, and port 8080 to 80
docker run --name website -v $PWD/website:/usr/share/nginx/html -p 8080:80 --rm nginx
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---

## Container & Image Cleanup

```bash
# Remove unused Docker objects (containers, networks, images, build cache)
docker system prune

# Remove all containers (force)
docker ps -aq | xargs docker rm

# Remove an image
docker rmi <image_name_or_id>
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---

## Logs & Monitoring

```bash
# Fetch logs of a container
docker logs <container_name_or_id>

# Fetch last ~n logs of a container including timestamp
docker logs -t -n <n> <container_name_or_id>

# Display live resource usage stats for a container
docker stats <container_name_or_id>

# Stream real-time Docker events
docker system events
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---

## Inspecting & Debugging

```bash
# Execute an interactive bash shell inside a running container
docker exec -it <container_name_or_id> /bin/bash

# Execute a command in a running container
docker exec <container_name_or_id> <command>

# Execute a command interactively (with TTY)
docker exec --interactive --tty <container_name_or_id> <shell>

# Display processes running inside a container
docker top <container_name_or_id>

# Inspect a container's configuration
docker inspect <container_name_or_id>

# View detailed config with less
docker inspect <container_name_or_id> | less

# Inspect a Docker image
docker image inspect <image_name_or_id>

# Show image config labels in JSON
docker image inspect --format='{{json .Config.Labels}}' <image_name_or_id>

# Show disk usage for Docker (containers, images, volumes)
docker system df
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---

## Authentication & Registry

```bash
# Authenticate to a Docker registry (default: Docker Hub)
docker login

# Push a tagged image to a registry
docker push <docker_username>/<image_name>:<tag>

# Pull a Docker image from a registry
docker pull <docker_username>/<image_name>:<tag>
```

[⬆ ʀᴇᴛᴜʀɴ ᴛᴏ ᴄᴏɴᴛᴇɴᴛꜱ](#contents)

---
