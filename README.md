# Docker Compose Django Project with PostgreSQL

## Overview

This project demonstrates how to Dockerize a Django application with a PostgreSQL backend using Docker Compose. It simplifies the setup of multi-container applications by defining both the Django app and the PostgreSQL database in a single `docker-compose.yml` file. This setup allows you to run the application and database in isolated containers while ensuring that the services are networked together and can communicate with each other.

## Project Setup

### Prerequisites

Before you begin, ensure that you have the following installed:

- Docker
- Docker Compose

You can install Docker and Docker Compose from the official [Docker website](https://docs.docker.com/get-docker/) and [Docker Compose documentation](https://docs.docker.com/compose/install/).

### Steps to Set Up the Project

1. **Clone the Repository**:
   Clone this repository to your local machine:
   ```bash
   git clone https://github.com/your-username/docker-compose-django-postgresql.git
   cd docker-compose-django-postgresql
Install Python Dependencies: If you haven't already, you need to install the required Python dependencies using the requirements.txt file. Run:
bash
pip3 install -r requirements.txt
Dockerize the Application: The Dockerfile defines the process for containerizing the Django app, and the .dockerignore ensures unnecessary files are not copied into the container. The docker-compose.yml file defines the web app and PostgreSQL database services.

Build and Start the Containers: Use the following command to build and start the containers:
bash
docker-compose up --build
Run Migrations: After the containers are up, run the database migrations:
docker-compose exec web python3 manage.py migrate
Access the Application: Open your browser and go to:
http://<EC2_PUBLIC_IP>:8000
You should see the Django welcome page if everything is working correctly.

File Structure
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
Troubleshooting
While setting up the project, you might encounter the following issues:

PostgreSQL Permissions:

Issue: The PostgreSQL container fails to start due to permission issues on the data directory.

Solution: Run the following command to fix the permissions:

bash
docker exec -it postgres_db chown -R postgres:postgres /var/lib/postgresql/data
Missing Dependency (psycopg2):

Issue: You might encounter a ModuleNotFoundError for psycopg2 when Django attempts to connect to PostgreSQL.

Solution: Ensure that psycopg2 is included in the requirements.txt file, then install it:

bash
pip install -r requirements.txt
Connection Refused Error:

Issue: When accessing the app, you might see an ERR_CONNECTION_REFUSED error.

Solution: Modify the runserver command to bind the app to 0.0.0.0 instead of 127.0.0.1:

python3 manage.py runserver 0.0.0.0:8000
Notes
The project uses PostgreSQL as the database and Django as the web framework.

The containers are set up to run in development mode, so you should make further adjustments for production deployments, such as using a production-ready WSGI server like Gunicorn.

Contributing
Feel free to fork the repository, submit issues, or create pull requests for improvements. If you encounter any issues or have suggestions, don't hesitate to open an issue.

License
This project is licensed under the MIT License - see the LICENSE file for details.


### How to Use This File:
- You can copy this content into a new `README.md` file in your GitHub project directory.
- Update the `git clone` link with your own GitHub repository link. Replace `https://github.com/your-username/docker-compose-django-postgresql.git` with the correct link to your repository.

This file serves as an introductory document to guide users on setting up the project, troubleshooting common issues, and understanding its structure and setup.







