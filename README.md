# Keycloak Deployment with Docker Compose

This guide provides step-by-step instructions to set up a Keycloak instance using Docker Compose, including PostgreSQL and Traefik for reverse proxy and SSL management.

---

## Prerequisites

- **sudo** privileges on the server.
- Installed versions of **Docker** and **Docker Compose**.

---

## Setup Instructions

1. **Create and Configure PostgreSQL Data Directory**

   - Create a directory for PostgreSQL data:
     ```bash
     mkdir /path/to/postgresql_data
     ```

   - Change ownership of the directory to user `1001`:
     ```bash
     sudo chown -R 1001:1001 /path/to/postgresql_data
     ```

   - Set the appropriate permissions:
     ```bash
     chmod 700 -R /path/to/postgresql_data
     ```

2. **Install Docker**

   - Update your system’s package index:
     ```bash
     sudo apt update
     ```

   - Install Docker:
     ```bash
     sudo apt install docker.io
     ```

3. **Install Docker Compose**

   - Install Docker Compose:
     ```bash
     sudo apt install docker-compose
     ```

   - Verify the installations:
     ```bash
     docker --version
     docker-compose --version
     ```

4. **Create a Shared Docker Network for Proxy and Services**

   - Create a Docker network for reverse proxy (Traefik) and services to communicate:
     ```bash
     docker network create proxy
     ```

5. **Prepare Let's Encrypt for SSL**

   - Create a directory for Let's Encrypt configuration:
     ```bash
     mkdir ./letsencrypt
     ```

   - Create an ACME configuration file:
     ```bash
     touch ./letsencrypt/acme.json
     ```

   - Set secure permissions for the ACME file:
     ```bash
     chmod 600 ./letsencrypt/acme.json
     ```

6. **Run Docker Compose to Start the Services**

   - Start the Keycloak, PostgreSQL, and Traefik services using Docker Compose:
     ```bash
     docker-compose up -d
     ```

7. **Stop the Services**

   - To stop the services, run:
     ```bash
     docker-compose down
     ```

8. **Check the Logs of Running Containers**

   - To view logs for a specific container:
     ```bash
     docker logs <container_name>
     ```

9. **Restart Containers If Needed**

   - To restart the containers:
     ```bash
     docker-compose restart
     ```

10. **Remove Services and Networks Created by Docker Compose**

    - To remove all services and networks created by Docker Compose:
      ```bash
      docker-compose down --volumes
      ```

---

## Notes

- Ensure the paths used in this guide match the ones defined in your `docker-compose.yml` file.
- After the setup, you can access Keycloak via the configured URL or server IP address.

---

## Troubleshooting

- If you encounter issues, check container logs using:
  ```bash
  docker logs <container_name>
