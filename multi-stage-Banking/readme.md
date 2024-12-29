# Bank Management System

A Flask-based banking system with PostgreSQL database, using Docker for containerization.

## Features

- Account management (create, view balance)
- Transaction handling (deposits, withdrawals)
- PostgreSQL database integration
- Docker multi-stage build for optimized container size
- RESTful API endpoints

## Project Structure

```
.
├── app/
│   ├── models/          # Database models
│   │   ├── base.py
│   │   ├── account.py
│   │   └── customer.py
│   ├── services/        # Business logic
│   │   └── account_service.py
│   ├── database.py      # Database configuration
│   └── main.py         # API endpoints
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Prerequisites

- Docker Desktop for Mac
- Docker Compose

## Setup

1. Clone the repository
2. Navigate to the project directory
3. Build and run the containers:
   ```bash
   docker-compose up --build
   ```

## API Endpoints

### Create Account
```bash
POST /account
Content-Type: application/json

{
    "customer_id": 1,
    "account_type": "savings"
}
```

### Check Balance
```bash
GET /account/{account_id}/balance
```

### Deposit
```bash
POST /account/{account_id}/deposit
Content-Type: application/json

{
    "amount": 100.00
}
```

### Withdraw
```bash
POST /account/{account_id}/withdraw
Content-Type: application/json

{
    "amount": 50.00
}
```

## Docker Configuration

The project uses a multi-stage Dockerfile to create an optimized container:
- Builder stage: Compiles dependencies
- Final stage: Contains only runtime components
- Reduced image size for production deployment

## Database

PostgreSQL database with:
- Persistent volume storage
- Automatic table creation
- SQLAlchemy ORM integration

## Development

To stop the containers:
```bash
docker-compose down
```

To view logs:
```bash
docker-compose logs -f
```

## Environment Variables

- `DATABASE_URL`: PostgreSQL connection string
- `POSTGRES_USER`: Database user
- `POSTGRES_PASSWORD`: Database password
- `POSTGRES_DB`: Database name

## Security Notes

- Update default database credentials before production use
- Implement proper authentication and authorization
- Add input validation and error handling
- Use environment variables for sensitive data
