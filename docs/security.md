# Security & Compliance

This document summarizes the security practices implemented for the Restauranty microservices project.Managed secrets are managed using **GitHub Actions Secrets** and **Kubernetes Secrets**.

---

## 1. GitHub Repository Secrets

The CI/CD pipeline requires access to Docker Hub, AWS, and MongoDB credentials. These values are securely stored in **GitHub repository secrets** and referenced inside the GitHub Actions workflow.

Configured secrets include:

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- DOCKERHUB_USERNAME
- DOCKERHUB_TOKEN
- MONGODB_URI

These secrets are injected into the CI/CD workflow during pipeline execution and are not visible in the repository code.

![GitHub Secrets](img/security-1.png)

---

## 2. Kubernetes Secret for MongoDB

The MongoDB connection string used by the microservices is stored as a **Kubernetes Secret** inside the cluster rather than being hardcoded in the deployment files.

```bash
kubectl create secret generic mongo-secret
--from-literal=MONGO_URI="mongodb+srv://mongo-user:**\*\***@mongodb.plxma3m.mongodb.net/restauranty?retryWrites=true&w=majority"
-n restauranty
```

This secret is referenced in the Kubernetes deployment manifests using `secretKeyRef`.

env:

```bash
- name: MONGODB_URI
  valueFrom:
  secretKeyRef:
  name: mongo-secret
  key: MONGO_URI
```

---

## 3. Verify Secret in Kubernetes

To verify that the secret exists in the cluster, run:

```bash
kubectl get secrets -n restauranty
```

To inspect the secret details:

```bash
kubectl describe secret mongo-secret -n restauranty
```

![Kubernetes Secrets](img/security-2.png)

These commands confirm that sensitive credentials are stored securely in the Kubernetes cluster.

---
