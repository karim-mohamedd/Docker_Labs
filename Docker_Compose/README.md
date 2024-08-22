
---

# Docker Compose 

This project uses Docker Compose to define and run multi-container Docker applications. Docker Compose allows you to manage your application services, networks, and volumes in a single file and orchestrate them with simple commands.

## Prerequisites

- **Docker**: Ensure Docker is installed and running on your machine. [Install Docker](https://docs.docker.com/get-docker/).
- **Docker Compose**: Docker Compose is included with Docker Desktop. For Linux, install Docker Compose separately. [Install Docker Compose](https://docs.docker.com/compose/install/).

## Project Structure

This project includes the following files:

- `docker-compose.yml`: Defines the services, networks, and volumes for the application.
- `Dockerfile`: Defines the Docker image build process for each service.
- `nginx.conf` (optional): Custom NGINX configuration file (if using NGINX).

## Getting Started

Follow these steps to get started with Docker Compose:

### 1. Clone the Repository

```bash
git clone https://github.com/karim-mohamedd/Docker_Labs.git
cd Docker_Labs
```

### 2. Review `docker-compose.yml`

The `docker-compose.yml` file defines the services for your application. Here is an example configuration:

**docker-compose.yml:**

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    networks:
      - webnet

  app:
    build:
      context: ./app
      dockerfile: Dockerfile
    networks:
      - webnet

networks:
  webnet:
    driver: bridge
```

### 3. Build and Start the Application

Run the following command to build and start all services defined in `docker-compose.yml`:

```bash
docker-compose up
```

- Use `docker-compose up -d` to run in detached mode.
- Use `docker-compose up --build` to rebuild images before starting.

### 4. Stopping the Application

To stop and remove all containers, networks, and volumes defined in `docker-compose.yml`, run:

```bash
docker-compose down
```

### 5. Scaling Services

To scale a specific service (e.g., increase the number of replicas for `web`), use:

```bash
docker-compose up --scale web=3
```

### 6. Viewing Logs

To view logs from all services:

```bash
docker-compose logs
```

To view logs from a specific service (e.g., `app`):

```bash
docker-compose logs app
```

### 7. Accessing the Application

- **Web Service:** Access the web service via `http://localhost` in your browser.

## Customization

- **Add More Services:** Update `docker-compose.yml` to add additional services or change configurations.
- **Custom NGINX Configuration:** Place your `nginx.conf` file in the project root and modify the `docker-compose.yml` to copy it into the NGINX container:

  ```yaml
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
      - ./nginx.conf:/etc/nginx/nginx.conf
  ```

## Troubleshooting

- **Service Not Starting:** Check the logs with `docker-compose logs` to identify issues.
- **Port Conflicts:** Ensure the ports defined in `docker-compose.yml` are not used by other applications on your machine.
- **Permissions Issues:** Verify that you have the necessary permissions for files and directories used in volume mounts.

## References

- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [NGINX Documentation](https://nginx.org/en/docs/)


---
