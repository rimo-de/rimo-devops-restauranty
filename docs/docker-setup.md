# Docker Setup

This document explains how the Restauranty application was containerized using Docker and orchestrated using Docker Compose.

The stack includes:

- MongoDB
- Auth service
- Discounts service
- Items service
- React client
- HAProxy

---

## 1. Build Backend Service Images

Separate Dockerfiles were created for the three backend microservices:

- `docker/auth/Dockerfile`
- `docker/discounts/Dockerfile`
- `docker/items/Dockerfile`

Each image installs Node.js dependencies and starts the service with `node server.js`.

### Build auth image

```bash
docker build -f docker/auth/Dockerfile -t restaurant-auth
```

![Docker Setup 1](../img/Docker-setup-1.png)

### Build discounts image

```bash
docker build -f docker/discounts/Dockerfile -t restaurant-discounts .
```

![Docker Setup 2](../img/Docker-setup-2.png)

### Build items image

```bash
docker build -f docker/items/Dockerfile -t restaurant-items .
```

![Docker Setup 3](../img/Docker-setup-3.png)

---

## 2. Build Frontend Image

The React frontend uses a multi-stage Docker build:

- Stage 1: build the React application using Node.js
- Stage 2: serve the generated static files using Nginx

```bash
docker build -f docker/client/Dockerfile -t restaurant-client .
```

![Docker Setup 4](../img/Docker-setup-4.png)

---

## 3. Run the Stack with Docker Compose

A docker-compose.yml file was created to orchestrate all services together.

It starts:

- MongoDB
- Auth service
- Discounts service
- Items service
- Client
- HAProxy

```bash
docker compose up --build
```

![Docker Setup 5](../img/Docker-setup-5.png)

---

## 4. Recreate HAProxy After Config Fix

During setup, the HAProxy container initially failed because the mounted haproxy.cfg file had a formatting issue. After fixing the configuration file, HAProxy was recreated.

```bash
docker compose up -d haproxy --force-recreate
```

![Docker Setup 6](../img/Docker-setup-6.png)

---

## 5. Verify Running Containers

Once the stack was started successfully, all containers were running as expected.

````bash
docker compose ps
```

![Docker Setup 7](../img/Docker-setup-7.png)

Docker Desktop also confirmed that all services were healthy and running.

![Docker Setup 8](../img/Docker-setup-8.png)

---

## 6. Test the Application

The application was tested through the HAProxy entry point.

```bash
curl -I http://localhost:8080
```

![Docker Setup 9](../img/Docker-setup-9.png)

This confirms that HAProxy is routing requests correctly to the frontend and backend services inside the Docker network.

````
