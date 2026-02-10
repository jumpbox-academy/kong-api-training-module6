# 🚀 Security and Authentication with Kong

This repository contains a hands-on lab for practicing:

- Running Kong Gateway in DB-less (declarative) mode
- Sending traffic through Kong
- Understanding plugin key-auth

Everything runs using **Docker Compose** and **Kong in DB-less mode**.

## 📁 Prerequisites

Make sure you have installed:

- Docker
- Docker Compose
- Git

---

You can verify your Docker installation with:
```bash
docker --version

docker compose version
```

## ✅ Getting Started
### 1.Create a Docker Network

Create a dedicated network for Kong:
```bash
docker network create kong-net
```

To check existing Docker networks, run:
```bash
docker network ls
```

You should see kong-net listed.

---

### 2.Start Kong Gateway

Start all services using Docker Compose:
```bash
docker compose up -d
```

Test the backend directly (bypass Kong)
```bash
curl http://localhost:3000/v1/hello
```
Expected response:
```
{"version":"v1","message":"Hello from Backend V1","request_id":"n/a"}
```

Call through Kong Gateway (without API Key):
```bash
curl -i http://localhost:8000/api/v1/hello
```
You should get
```
401 Unauthorized
```
(This is expected because Kong requires an API key.)

Call through Kong Gateway (with API Key):
```bash
curl -H "apikey:lfomvny#ash@" http://localhost:8000/api/v1/hello
```

Example response:
```
{
  "version": "v1",
  "message": "Hello from Backend V1",
  "request_id": "..."
}
```

---
## 🧹 3.Cleanup (Stop and Remove Containers)
When you are done, you can stop and remove all running containers:
```bash
docker compose down
```

If you also want to remove the custom network:
```bash
docker network rm kong-net
```