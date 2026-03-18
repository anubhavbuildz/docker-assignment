# 🚀 Dockerized Apache Deployment – Case Study

## 📌 Problem Statement

You are a DevOps Engineer tasked with Dockerizing a custom application for production.

### Assumptions

- Software: **Apache**
- Base OS: **Ubuntu**
- No pre-built image available

### Requirements

1. Create and push a base image (Ubuntu + Apache) to Docker Hub
2. Developers should only provide code (no Docker knowledge required)
3. Provide a Dockerfile for developers to build their application image

---

## 🏗️ Architecture Overview

![Architecture Flow](./architecture.png)

### 🔄 Flow Explanation

1. **DevOps Engineer (Dev-1)**
   - Builds a **base image** with Ubuntu + Apache
   - Pushes it to Docker Hub

2. **Docker Hub**
   - Stores:
     - Base Image
     - Application Image (after developer adds code)

3. **Developer (Dev-2)**
   - Uses the base image
   - Adds application code
   - Builds final application image

4. **Production**
   - Pulls final image
   - Runs containerized application

---

## 📁 Project Structure

```bash
case-study/
├── Dockerfile.base
├── README.md
├── architecture.png
└── developer/
    ├── Dockerfile
    └── index.html
```

---

## 🧱 Base Image (DevOps)

### Dockerfile: `Dockerfile.base`

```dockerfile
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apache2 && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
```

### 🔨 Build Base Image

```bash
docker build -f Dockerfile.base -t anubhavbuildz/ubuntu-apache-base:1.0 .
```

### 📤 Push to Docker Hub

```bash
docker login
docker push anubhavbuildz/ubuntu-apache-base:1.0
```

---

## 👨‍💻 Developer Image

### Dockerfile: `developer/Dockerfile`

```dockerfile
FROM anubhavbuildz/ubuntu-apache-base:1.0

COPY . /var/www/html/

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
```

### 📄 Sample App (`index.html`)

A simple HTML file that will replace the default Apache page.

---

## 🔨 Build Application Image

```bash
cd developer
docker build -t anubhavbuildz/custom-apache-app:1.0 .
```

### 📤 Push Final Image

```bash
docker push anubhavbuildz/custom-apache-app:1.0
```

\*\*\*for reference only

---

## 🚀 Run in Production

```bash
docker run -d --name apache-app -p 80:80 anubhavbuildz/custom-apache-app:1.0
```

Open in browser:

```
http://localhost
```

---

## ✅ Key Benefits

- 🔁 Reusable base image
- 👨‍💻 Developers only focus on code
- 📦 Standardized environment
- 🚀 Easy deployment to production
- 🔒 Isolation using containers

---

## 🧠 DevOps Insight

This architecture follows:

> **"Build once, reuse everywhere"**

- Base image = platform
- App image = business logic

---

## 🏁 Conclusion

A custom Ubuntu + Apache base image is created and pushed to Docker Hub. Developers build on top of this image by simply adding their code. This ensures consistency, scalability, and simplified deployment across environments.

---

## ⚡ Author

**Anubhav Sharma**
DevOps & Cloud Engineer
