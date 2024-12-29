# Docker Multi-Stage Build

Docker multi-stage builds are a powerful feature that helps optimize image size by separating the build process into multiple stages. Each stage can use a different base image, and only the final stage contains the essential files for the application.

## Benefits of Multi-Stage Builds
- **Smaller Image Size**: Keeps the final image lean by excluding build dependencies.
- **Improved Security**: Reduces attack surface by removing unnecessary tools and libraries.
- **Easier Maintenance**: Separates build and runtime configurations.

---

## Syntax
A multi-stage build uses multiple `FROM` statements in a single `Dockerfile`. Each stage is identified by a name or index and can COPY artifacts from previous stages.

### Example: Multi-Stage Build for a Go Application
```dockerfile
# Stage 1: Build
FROM golang:1.19 AS builder

# Set the working directory
WORKDIR /app

# Copy go.mod and go.sum files and download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy source files and build the application
COPY . .
RUN go build -o main .

# Stage 2: Runtime
FROM alpine:3.18

# Set the working directory
WORKDIR /app

# Copy the built application from the builder stage
COPY --from=builder /app/main .

# Expose application port
EXPOSE 8080

# Command to run the application
CMD ["./main"]
```

---

## Advanced Options

### 1. **Build Arguments (`ARG`)**
Use `ARG` to parameterize builds. For example:
```dockerfile
# Pass a build argument to specify the Go version
ARG GO_VERSION=1.19
FROM golang:${GO_VERSION} AS builder
```
Build command:
```bash
docker build --build-arg GO_VERSION=1.20 -t my-go-app .
```

### 2. **Target Specific Stage (`--target`)**
Build up to a specific stage without completing the entire build process:
```bash
docker build --target builder -t intermediate-build .
```

### 3. **Conditional Copy**
Use `COPY` with conditional expressions for platform-specific files:
```dockerfile
COPY --from=builder /app/main /app/main
COPY --from=builder /app/config-${TARGET_ENV}.yaml /app/config.yaml
```
Set the `TARGET_ENV` build argument:
```bash
docker build --build-arg TARGET_ENV=production -t my-app .
```

### 4. **Multi-Platform Builds**
Use Docker Buildx for multi-platform images:
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t my-app:multi-platform .
```

---

## Best Practices
1. **Use Minimal Base Images**: Keep your runtime image as small as possible (e.g., Alpine).
2. **Leverage `.dockerignore`**: Exclude unnecessary files from the build context.
3. **Name Build Stages**: Use meaningful names for easier maintenance.
4. **Cache Dependencies**: Copy dependency files first to leverage caching (e.g., `go.mod`, `package.json`).
5. **Test Build Locally**: Test intermediate stages using the `--target` flag.

---

By leveraging multi-stage builds, you can create optimized, secure, and maintainable Docker images for your applications.
