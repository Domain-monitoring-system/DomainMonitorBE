# Domain Monitor Backend

A robust API service for the Domain Monitoring System that checks domain and SSL certificate status.

## Project Overview

The Domain Monitor Backend is a Flask-based RESTful API that provides authentication, domain monitoring, and scheduled checks for the Domain Monitoring System. It utilizes multi-threading to efficiently scan multiple domains and check their HTTP status and SSL certificates.

## Features

- **User Authentication**: Registration, login, and Google OAuth support
- **Domain Monitoring**: Scan domains for HTTP status and SSL certificate validity
- **Scheduled Checks**: Configure hourly or daily automated domain scans
- **Multi-threaded Processing**: Efficient domain scanning with concurrent processing
- **PostgreSQL Database Integration**: Persistent storage for users and domain status

## Project Structure

```
domain-monitor-backend/
├── app.py                      # Main application entry point
├── config.py                   # Configuration and environment variables
├── utils.py                    # Utility functions
├── .env                        # Environment variables (not tracked in git)
├── requirements.txt            # Python dependencies
├── Dockerfile                  # Docker configuration
└── modules/
    ├── __init__.py
    ├── DataManagement.py       # Data storage and retrieval (file-based)
    ├── DBManagement.py         # Database operations (PostgreSQL)
    ├── domains_check_MT.py     # Multi-threaded domain checking
    └── login.py                # Authentication logic
```

## Setup and Installation

### Prerequisites

- Python 3.9+
- PostgreSQL (for production environments)
- Docker (optional)

### Local Development Setup

1. Clone the repository
   ```bash
   git clone https://github.com/Domain-monitoring-system/DomainMonitorBE.git
   cd domain-monitor-backend
   ```

2. Create and activate a virtual environment
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies
   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

5. Run the application
   ```bash
   python app.py
   ```

### Docker Setup

1. Build the Docker image
   ```bash
   docker build -t domain-monitor-backend .
   ```

2. Run the container
   ```bash
   docker run -p 5001:5001 --env-file .env domain-monitor-backend
   ```

## API Endpoints

### Authentication

- `POST /api/login`: Authenticate user
- `POST /api/register`: Register new user
- `GET /api/check-username`: Check username availability

### Domain Management

- `GET /api/domains`: Get user domains
- `DELETE /api/domains`: Remove a domain
- `POST /api/check-domains`: Check domain status

### Scheduler

- `POST /api/schedule/hourly`: Schedule hourly checks
- `POST /api/schedule/daily`: Schedule daily checks
- `GET /api/schedule/status`: Get schedule status
- `POST /api/schedule/stop`: Stop scheduled tasks

## Configuration

The application configuration is managed through environment variables defined in `.env` file:

```
# Flask Configuration
FLASK_DEBUG=False
PORT=5001
HOST=0.0.0.0

# Database Configuration
DB_NAME=moniDB
DB_USER=myuser
DB_PASSWORD=mypassword
DB_HOST=localhost
DB_PORT=5432

# Google OAuth Configuration
GOOGLE_CLIENT_ID=your-client-id
GOOGLE_CLIENT_SECRET=your-client-secret
GOOGLE_CALLBACK_URL=http://localhost:8080/google-login/callback

# Domain Check Configuration
HTTP_CHECK_TIMEOUT=1.5
SSL_CHECK_TIMEOUT=2.0
DOMAIN_CHECK_TIMEOUT=30.0
MAX_WORKERS=50
```

## Database Integration

This application connects to a PostgreSQL database for data persistence. The database schema is maintained in a separate repository:

- [DomainMonitorDB](https://github.com/Domain-monitoring-system/DomainMonitoringDB)

The schema includes tables for:
- Users and authentication
- Domain scan results
- Scheduled tasks

Please refer to the database repository for the complete schema definition, migrations, and data models.

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -am 'Add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Submit a pull request

## License

[MIT License](LICENSE)