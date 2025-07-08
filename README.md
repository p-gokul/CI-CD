# 🛠️ CI/CD Pipelines - Todo App

This repository implements a **Continuous Integration and Continuous Deployment (CI/CD)** workflow using **GitHub Actions** and **AWS CodePipeline** for a full-stack Todo application.

---

## 📸 Architecture Diagrams

### 🧩 Frontend CI-CD

![Frontend CI/CD](/diagrams/frontend-ci-cd.png)

### 🧩 Backend CI-CD

![Backend CI/CD](/diagrams/backend-ci-cd.png)

---

### 🧱 Frontend CI-CD Workflow

1. Developer pushes code to the `main` branch
2. GitHub Actions triggers on `frontend/**` or `.github/workflows/frontend.yaml` path changes.
3. Steps of `frontend.yaml`

| Step                    | Description                                           |
| ----------------------- | ----------------------------------------------------- |
| Checkout                | Clones the repository                                 |
| AWS Credentials         | Sets up AWS access via GitHub Secrets                 |
| Setup Node.js + Bun     | Installs Node 22 and Bun runtime                      |
| Install & Test          | Installs dependencies and runs tests using `bun test` |
| Build                   | Compiles the frontend assets                          |
| Clean S3                | Deletes old contents in S3 bucket                     |
| Upload to S3            | Uploads the built assets                              |
| CloudFront Invalidation | Clears CDN cache to reflect the latest version        |

### 🧱 Backend Deployment Workflow

1. Developer pushes code to the `main` branch
2. GitHub Actions triggers on `backend/*` or `.github/workflows/backend.yaml` path changes
3. Steps of `backend.yaml`

| Step                | Description                                              |
| ------------------- | -------------------------------------------------------- |
| Checkout            | Clones the repository                                    |
| AWS Credentials     | Sets up AWS access via GitHub Secrets                    |
| Docker Build & Push | Builds Docker image and pushes it to ECR                 |
| ECS Update          | Triggers rolling update on ECS using latest Docker image |

---

## 🔐 Secrets Required

The following secrets must be configured in your GitHub repository:

| Secret Name             | Purpose                |
| ----------------------- | ---------------------- |
| `AWS_ACCESS_KEY_ID`     | IAM access key for AWS |
| `AWS_SECRET_ACCESS_KEY` | IAM secret key for AWS |

---

## 🧪 Tech Stack

- **GitHub Actions** for CI/CD
- **Bun** for frontend package management and testing
- **AWS S3 + CloudFront** for frontend hosting
- **Docker + ECR + ECS** for backend deployment
- **Node.js / Vite** based application

---

## 🚀 Deployment Targets

| Component | Target Platform |
| --------- | --------------- |
| Frontend  | S3 + CloudFront |
| Backend   | ECR + ECS       |

---
