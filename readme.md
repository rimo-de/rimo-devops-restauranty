# Restauranty App

This project demonstrates a **production-style DevOps deployment** for a microservices-based restaurant application.
The goal is to containerize, deploy, automate, and monitor the application using modern DevOps practices.

The original application consists of **Node.js microservices + React frontend + MongoDB**, deployed using **Docker, Kubernetes, and CI/CD pipelines**.

---

## Documentation Overview

| Topic                     | Detailed Explanation                                                                                                                                                  |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Project Architecture**  | Overview of the system architecture including microservices, frontend, database, and infrastructure components.<br><br>📄 [Architecture Details](app/architecture.md) |
| **Local Setup**           | Instructions to run the application locally for development and testing.<br> <br>📄 [Local Setup Guide](docs/local-setup.md)                                          |
| **Docker Usage**          | Containerization of all services using Docker and orchestration using Docker Compose.<br><br>📄 [Docker Setup](docs/docker.md)                                        |
| **Kubernetes Deployment** | Deployment of all services using Kubernetes including deployments, services, and ingress routing.<br><br>📄 [Kubernetes Deployment](docs/kubernetes.md)               |
| **CI/CD Pipeline**        | Automated build and deployment pipeline implemented using GitHub Actions.<br><br>📄 [CI/CD Pipeline](docs/ci-cd.md)                                                   |
| **Monitoring**            | Monitoring and observability setup using tools such as Prometheus and Grafana.<br><br>📄 [Monitoring Setup](docs/monitoring.md)                                       |
| **Security**              | Security best practices including secret management, authentication handling, and infrastructure protection.<br><br>📄 [Security Guide](docs/security.md)             |
