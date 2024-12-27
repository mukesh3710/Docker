# Flask Hello World Docker Application

A simple containerized Flask application that demonstrates basic Docker deployment and Flask routing.

## Features

- Simple Hello World endpoint
- Health check endpoint
- Containerized with Docker
- Production-ready configuration

## Prerequisites

- Docker
- Python 3.9+ (for local development)

## Project Structure

```
.
├── app.py              # Flask application
├── requirements.txt    # Python dependencies
├── Dockerfile         # Docker configuration
└── README.md          # Documentation
```

## Quick Start

1. Build the Docker image:
```bash
docker build -t flask-app .
```

2. Run the container:
```bash
docker run -p 5000:5000 flask-app
```

3. Access the application:
- Main endpoint: http://localhost:5000
- Health check: http://localhost:5000/health

## Local Development

1. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the application:
```bash
python app.py
```

## API Endpoints

- `GET /`: Returns "Hello, Docker!"
- `GET /health`: Returns health status

## Docker Commands

- Build image: `docker build -t flask-app .`
- Run container: `docker run -p 5000:5000 flask-app`
- Stop container: `docker stop $(docker ps -q --filter ancestor=flask-app)`
- List containers: `docker ps`

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT
