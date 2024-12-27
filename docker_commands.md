# Docker Command Cheatsheet

## General Commands

### Version and Info
- **Check Docker version**
  ```bash
  docker --version
  ```
- **Get system-wide Docker information**
  ```bash
  docker info
  ```

---

## Container Management

### Running Containers
- **Run a container interactively**
  ```bash
  docker run -it <image_name>
  ```
- **Run a container in detached mode**
  ```bash
  docker run -d <image_name>
  ```
- **Run a container with port mapping**
  ```bash
  docker run -p <host_port>:<container_port> <image_name>
  ```
- **Run a container with a custom name**
  ```bash
  docker run --name <container_name> <image_name>
  ```

### Managing Containers
- **List running containers**
  ```bash
  docker ps
  ```
- **List all containers (including stopped ones)**
  ```bash
  docker ps -a
  ```
- **Stop a container**
  ```bash
  docker stop <container_id|container_name>
  ```
- **Start a stopped container**
  ```bash
  docker start <container_id|container_name>
  ```
- **Restart a container**
  ```bash
  docker restart <container_id|container_name>
  ```
- **Remove a container**
  ```bash
  docker rm <container_id|container_name>
  ```

---

## Image Management

### Building and Managing Images
- **Build an image from a Dockerfile**
  ```bash
  docker build -t <image_name> .
  ```
- **List all images**
  ```bash
  docker images
  ```
- **Remove an image**
  ```bash
  docker rmi <image_id|image_name>
  ```
- **Pull an image from Docker Hub**
  ```bash
  docker pull <image_name>
  ```
- **Push an image to Docker Hub**
  ```bash
  docker push <image_name>
  ```

---

## Logs and Debugging

### Viewing Logs
- **View container logs**
  ```bash
  docker logs <container_id|container_name>
  ```
- **Follow logs in real-time**
  ```bash
  docker logs -f <container_id|container_name>
  ```

### Debugging
- **Access a running container’s shell**
  ```bash
  docker exec -it <container_id|container_name> /bin/bash
  ```
- **Inspect container details**
  ```bash
  docker inspect <container_id|container_name>
  ```

---

## Volumes and Networks

### Volumes
- **List all volumes**
  ```bash
  docker volume ls
  ```
- **Create a volume**
  ```bash
  docker volume create <volume_name>
  ```
- **Remove a volume**
  ```bash
  docker volume rm <volume_name>
  ```

### Networks
- **List all networks**
  ```bash
  docker network ls
  ```
- **Create a network**
  ```bash
  docker network create <network_name>
  ```
- **Connect a container to a network**
  ```bash
  docker network connect <network_name> <container_name>
  ```
- **Disconnect a container from a network**
  ```bash
  docker network disconnect <network_name> <container_name>
  ```

---

## Docker Compose

### Basic Commands
- **Start services defined in `docker-compose.yml`**
  ```bash
  docker-compose up
  ```
- **Start services in detached mode**
  ```bash
  docker-compose up -d
  ```
- **Stop services**
  ```bash
  docker-compose down
  ```

### Useful Flags
- **Rebuild images before starting**
  ```bash
  docker-compose up --build
  ```
- **View logs of all services**
  ```bash
  docker-compose logs
  ```
- **Follow logs in real-time**
  ```bash
  docker-compose logs -f
  
