# Docker Init Command

The `docker init` command is used to initialize and scaffold a project for Docker usage. This is especially helpful for setting up basic configuration files such as `Dockerfile` and `.dockerignore`.

## Syntax
```bash
docker init [OPTIONS]
```

## Options
- `--name`: Specify a name for the project (default is the directory name).
- `--dependency`: Add runtime dependencies for the project (e.g., Flask for Python).
- `--help`: Display help for the command.

---

## Example: Initializing a Python Flask Project

### Command
```bash
docker init --name flask-app --dependency flask
```

### Resulting Files

1. **Dockerfile**
   ```dockerfile
   # Start from an official Python image
   FROM python:3.9-slim

   # Set the working directory
   WORKDIR /app

   # Copy project files
   COPY . .

   # Install dependencies
   RUN pip install flask

   # Expose the application port
   EXPOSE 5000

   # Command to run the application
   CMD ["python", "app.py"]
   ```

2. **.dockerignore**
   ```plaintext
   __pycache__/
   *.pyc
   .env
   .git
   .vscode
   ```

---

## Next Steps
1. Add your application code (e.g., `app.py` for Flask).
2. Build the Docker image:
   ```bash
   docker build -t flask-app .
   ```
3. Run the container:
   ```bash
   docker run -p 5000:5000 flask-app
   ```
4. Access your app at `http://localhost:5000`.

---

**Note**: Ensure Docker is installed and running on your system before using `docker init`.
