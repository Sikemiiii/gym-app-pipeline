# Gym App CI/CD Pipeline: Automated QA & Containerization

## 📌 Project Overview
This repository contains a fully automated Continuous Integration and Continuous Deployment (CI/CD) pipeline built for a multi-tier Gym Application. The core objective of this architecture is to ensure zero broken code reaches production by strictly enforcing automated API testing before containerization.

## 🏗️ Architecture Flow
This pipeline uses a **Two-Stage Gate** approach. If the automated QA tests fail (simulating a broken payment gateway or auth endpoint), the pipeline halts, preventing a faulty Docker build.

```mermaid
graph TD;
    A[Developer Pushes Code] --> B{Stage 1: API Testing Gate};
    B -->|Tests Pass| C[Stage 2: Containerization];
    B -->|Tests Fail| D[Pipeline Halts - Alert Sent];
    C --> E[Build Frontend Docker Image];
    C --> F[Build Backend Docker Image];'''

## 🛠️ Tools & Technologies Used
* **Source Control:** Git & GitHub
* **CI/CD Automation:** GitHub Actions
* **API Testing / QA:** Postman & Newman (CLI)
* **Containerization:** Docker
* **Environment:** Node.js, Alpine Linux

## 🚀 Pipeline Steps
1. **Source Trigger:** The workflow triggers automatically on any push to the `main` branch.
2. **Environment Setup:** Provisions an `ubuntu-latest` runner and configures Node.js.
3. **Automated QA Validation:** Executes a Postman collection via Newman to validate critical endpoints (e.g., Paystack payment integration).
4. **Conditional Build:** Upon successful test validation, the pipeline builds lightweight, secure Docker images for both the frontend (`nginx:alpine`) and the backend (`node:18-alpine`).
