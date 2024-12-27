# Understanding Docker: A Beginner's Guide

Docker is a platform that makes it easier to create, deploy, and run applications using containers. Let's break down the key concepts and workflow with simple examples.

## Docker Architecture

The Docker architecture consists of three main components:

1. **Docker Client (CLI)**
   - The command-line interface we use to interact with Docker
   - Examples: `docker build`, `docker run`, `docker pull`

2. **Docker Daemon**
   - The background service that manages Docker objects
   - Handles container lifecycle, images, and networking

3. **Docker Registry**
   - Stores Docker images
   - Docker Hub is the default public registry
   - Can also use private registries

## Basic Docker Workflow

Let's walk through a simple example:

1. **Create a Dockerfile**
```dockerfile
FROM node:14
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

2. **Build an Image**
```bash
docker build -t myapp:1.0 .
```

3. **Run a Container**
```bash
docker run -p 3000:3000 myapp:1.0
```

## Common Docker Commands

```bash
# List images
docker images

# List containers
docker ps

# Pull an image
docker pull nginx

# Stop a container
docker stop container_id

# Remove a container
docker rm container_id
```

## Best Practices

1. **Use Official Base Images**
   - More secure and maintained
   - Example: `FROM node:14-alpine`

2. **Minimize Layers**
   - Combine related commands
   - Use multi-stage builds

3. **Keep Images Small**
   - Use `.dockerignore`
   - Choose lightweight base images

4. **Tag Images Properly**
   - Use semantic versioning
   - Example: `myapp:1.0.0`

## Simple Example: Node.js Application

1. **Create a simple Express app**
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello Docker!');
});

app.listen(3000);
```

2. **Dockerfile**
```dockerfile
FROM node:14-alpine
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
```

3. **Build and Run**
```bash
docker build -t myapp .
docker run -p 3000:3000 myapp
```

Visit `http://localhost:3000` to see your containerized app!
