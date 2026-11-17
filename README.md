# DevOps Assignment 2: Build, Containerize and Automate

> **Course:** DevOps for Cloud Computing (CSC418)  
> **Student Name:** Huzaifa  
> **Roll Number:** SP23-BCS-034  
> **Docker Hub Repository:** [coffethebest/devops-a2](https://hub.docker.com/r/coffethebest/devops-a2)  

---

## 📌 Project Overview
This project demonstrates end-to-end DevOps practices combining Git/GitHub version control, Docker containerization, GitHub Actions CI/CD automation, and GitHub Webhooks.

The application is a lightweight, responsive personal portfolio built with plain HTML and CSS served by high-performance Nginx.

---

## 🛠️ Tech Stack & DevOps Components
- **HTML5 & CSS3:** Static portfolio web application.
- **Git & GitHub:** Version control, feature branching (`feature-endpoint`), and Pull Request code review workflow.
- **Docker:** Multi-stage lightweight Nginx container (`nginx:alpine`).
- **GitHub Actions:** Continuous Integration (CI) and Continuous Deployment (CD) pipeline validating the page and pushing automated container images to Docker Hub.
- **GitHub Webhook:** Real-time event notifications delivered to `webhook.site` on `push` and `pull_request` triggers.

---

## 🚀 Running the Project Locally (Docker)

### 1. Build the Docker Image
```bash
docker build -t coffethebest/devops-a2:manual .
```

### 2. Run the Container
```bash
docker run -d -p 8080:80 --name page coffethebest/devops-a2:manual
```

### 3. Access in Browser
Navigate to:
```
http://localhost:8080
```

---

## ⚙️ CI/CD Pipeline (`.github/workflows/ci.yml`)
The GitHub Actions workflow triggers on:
- Every `push` to the `main` branch.
- Every `pull_request` against `main`.

### Pipeline Steps:
1. **Checkout Code:** Fetches repository contents using `actions/checkout@v4`.
2. **Page Validation Checks:**
   - Verifies existence of `index.html` and `style.css`.
   - Validates `<title>` tag.
   - Asserts inclusion of student roll number `SP23-BCS-034`.
   - Asserts inclusion of student name `Huzaifa`.
3. **Docker Hub Login:** Authenticates securely via `secrets.DOCKERHUB_USERNAME` and `secrets.DOCKERHUB_TOKEN` (only on `main`).
4. **Build & Push:** Builds container image and pushes to Docker Hub with tag `:latest` (only on `main`).
