# easy-mlflow
A simple end-to-end docker compose-based setup for quickly deploying MLFlow anywhere! A basic username/password based authentication is also included.

## Features
- MLFlow with proxied artifact storage access
- MySQL-based backend
- S3-based artifact storage backend
- NGINX Reverse proxy for both UI and API with basic auth.

## Prerequisites
- Docker (with compose)
- Internet Access
- An S3 bucket and the required IAM credentials to access it
- apache2-utils (Debian, Ubuntu)
- Port 80 not in use

## Setup
### Generate credentials
Run the following command to with the desired username to generate the username and password combo
```
htpasswd -c .htpasswd <desired-username>
```
The credentials will be saved in a .htpasswd file.

### Modify environment variables
Edit the .env file and provide suitable values for the following keys:
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- MLFLOW_TRACKING_USERNAME (should be the same username as the one used in the previous step)
- MLFLOW_TRACKING_PASSWORD (should be the same password as the one used in the previous step)

## Start services
Run the following command in the terminal:
```
docker compose up -d
```
The MLFlow instance can now be accessed at http://localhost/mlflow.

If the services are deployed in an EC2 instance, MLFlow can also be accessed using the public URL of the instance.

## Troubleshooting
Run the following in the terminal to view the logs
```
docker compose logs nginx
docker compose logs mlflow
```
