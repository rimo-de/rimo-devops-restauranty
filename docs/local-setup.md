# Local Setup

This guide explains how to run the Restauranty microservices application locally for development and testing.

---

## Prerequisites

Make sure the following tools are installed:

- **Node.js v20** – required to run the backend services and React frontend.
- **Docker** – used to run MongoDB locally without installing it directly on your machine.
- **HAProxy (optional)** – used later to route requests through a single entry point.

---

## Start MongoDB

The application uses **MongoDB as the database**.
Instead of installing MongoDB locally, we run it as a Docker container.

```bash
docker run -d --name rimo-mongo -p 27017:27017 mongo
```

Explanation:

- `-d` → runs the container in detached mode
- `--name rimo-mongo` → assigns a readable container name
- `-p 27017:27017` → maps the default MongoDB port from container to host

MongoDB will now be available at:

```bash
mongodb://localhost:27017
```

---

## Run Backend Microservices

The application backend is composed of **three independent Node.js microservices**:

- **auth** – handles authentication and JWT tokens
- **discounts** – manages coupons and marketing campaigns
- **items** – manages menu items and related data

Each service runs on its **own port** and connects to the same MongoDB database.

---

## Start Auth Service

```bash
cd app/backend/auth
npm install
cp .env.example .env
node server.js
```

Explanation:

- `npm install` installs the dependencies defined in `package.json`.
- `.env` stores environment variables such as database connection and JWT secret.
- `node server.js` starts the authentication service.

Expected output:

```bash
Server listening on http://localhost:3001
Connected to Mongo
```

---

## Start Discounts Service

```bash
cd app/backend/discounts
npm install
cp .env.example .env
node server.js
```

This service runs on:

```bash
http://localhost:3002
```

It manages coupon codes and promotional campaigns.

---

## Start Items Service

```bash
cd app/backend/items
npm install
cp .env.example .env
node server.js
```

This service runs on:

```bash
http://localhost:3003
```

It manages restaurant menu items and related data.

---

## Run Frontend

The frontend is a **React application** that communicates with the backend APIs.

```bash
cd app/client
npm install
npm start
```

Explanation:

- Installs React dependencies
- Starts the development server

The frontend will run on:

```bash
http://localhost:3000
```

---

## Access the Application

Open the following URL in your browser:

```bash
http://localhost:3000
```

You should see the **Restauranty dashboard interface**, which communicates with the backend microservices and MongoDB database.
