# Docker Compose Django Project with PostgreSQL

## Overview
This project demonstrates how to Dockerize a Django application with a PostgreSQL backend using Docker Compose. It simplifies the setup of multi-container applications by defining both the Django app and the PostgreSQL database in a single `docker-compose.yml` file. This setup ensures that the services are networked together and can communicate with each other seamlessly.

## Prerequisites
Before you begin, ensure that you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Project Setup

### 1. Clone the Repository
Clone this repository to your local machine:
```bash
git clone https://github.com/your-username/docker-compose-django-postgresql.git
cd docker-compose-django-postgresql
```

### 2. Install Python Dependencies
Ensure you have Python dependencies installed using the `requirements.txt` file:
```bash
pip3 install -r requirements.txt
```

### 3. Dockerize the Application
The project contains the following important files:
- **`Dockerfile`**: Defines how the Django app container is built.
- **`.dockerignore`**: Ensures unnecessary files are not copied into the container.
- **`docker-compose.yml`**: Defines both the Django application and PostgreSQL database services.

### 4. Build and Start the Containers
Run the following command to build and start the containers:
```bash
docker-compose up --build
```

### 5. Run Migrations
Once the containers are running, apply database migrations:
```bash
docker-compose exec web python3 manage.py migrate
```

### 6. Access the Application
Open your browser and navigate to:
```
http://<EC2_PUBLIC_IP>:8000
```
You should see the Django welcome page if everything is working correctly.

## Project Structure
```
docker-compose-django-postgresql/
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── requirements.txt
├── myproject/
│   ├── myproject/
│   └── myapp/
├── manage.py
└── README.md
```

## Troubleshooting

### 1. PostgreSQL Permissions Issue
**Issue:** The PostgreSQL container fails to start due to permission issues on the data directory.

**Solution:** Run the following command to fix permissions:
```bash
docker exec -it postgres_db chown -R postgres:postgres /var/lib/postgresql/data
```

### 2. Missing `psycopg2` Dependency
**Issue:** You might encounter a `ModuleNotFoundError` for `psycopg2` when Django attempts to connect to PostgreSQL.

**Solution:** Ensure `psycopg2` is in `requirements.txt`, then reinstall dependencies:
```bash
pip install -r requirements.txt
```

### 3. Connection Refused Error
**Issue:** When accessing the app, you might see an `ERR_CONNECTION_REFUSED` error.

**Solution:** Modify the `runserver` command to bind the app to `0.0.0.0` instead of `127.0.0.1`:
```bash
python3 manage.py runserver 0.0.0.0:8000
```

## Notes
- The project uses PostgreSQL as the database and Django as the web framework.
- Containers are set up for development mode. For production deployments:
  - Use a production-ready WSGI server like Gunicorn.
  - Secure PostgreSQL with proper credentials and configurations.

## Contributing
Feel free to fork the repository, submit issues, or create pull requests for improvements. If you encounter any issues or have suggestions, don’t hesitate to open an issue.

## License
This project is licensed under the MIT License - see the `LICENSE` file for details.

---
**How to Use This File:**
- Copy this content into a new `README.md` file in your GitHub project directory.
- Update the repository URL in the `git clone` command.

This README serves as a complete guide to setting up, running, and troubleshooting the project.

