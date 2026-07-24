# Flask CI/CD Pipeline using Jenkins and GitHub Actions

## Project Overview

This project demonstrates the implementation of Continuous Integration and Continuous Deployment (CI/CD) for a Flask web application using **Jenkins** and **GitHub Actions**.

The pipeline automates the following tasks:

- Installing project dependencies
- Running automated tests using PyTest
- Building the application
- Deploying the application to a staging environment
- Deploying to production after a release tag
- Sending build notifications (Jenkins)
- Triggering builds automatically using GitHub Webhooks

---

# Repository

Original Repository

https://github.com/mohanDevOps-arch/flask_Practice

Forked Repository

https://github.com/<your-github-username>/flask_Practice

---

# Prerequisites

Before running this project, install the following software:

- Python 3.10 or later
- Git
- Jenkins
- pip
- GitHub Account
- GitHub Repository
- Ubuntu/Linux Server (or Windows with Jenkins)
- Java 17 (required for Jenkins)

### Verify Installation

```bash
python3 --version
git --version
java --version
jenkins --version
```

---

# Project Structure

```
flask_Practice/
│
├── app.py
├── requirements.txt
├── Jenkinsfile
├── README.md
│
├── tests/
│   └── test_app.py
│
└── .github/
    └── workflows/
        └── ci-cd.yml
```

---

# Jenkins CI/CD Pipeline

The Jenkins pipeline is defined inside the **Jenkinsfile**.

It contains the following stages.

## 1. Build Stage

- Create Python Virtual Environment
- Upgrade pip
- Install dependencies

Command executed:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

## 2. Test Stage

Runs all unit tests using PyTest.

```bash
pytest
```

If all tests pass, Jenkins proceeds to deployment.

---

## 3. Deploy Stage

Deploys the Flask application to the staging environment.

Example deployment command

```bash
python3 app.py
```

---

## Jenkins Pipeline Flow

```
Git Push
    │
    ▼
GitHub Webhook
    │
    ▼
Jenkins Pipeline
    │
    ├── Build
    ├── Test
    └── Deploy
```

---

# GitHub Actions Workflow

The workflow file is located at

```
.github/workflows/ci-cd.yml
```

The workflow performs the following jobs.

## Test Job

- Checkout repository
- Setup Python
- Install dependencies
- Execute PyTest

---

## Build Job

Runs only after successful tests.

Example

```
Build Application
```

---

## Deploy to Staging

Runs automatically when code is pushed to

```
staging
```

branch.

---

## Deploy to Production

Runs automatically whenever a Git tag (release) is pushed.

Example

```
git tag v1.0
git push origin v1.0
```

---

# GitHub Actions Workflow Flow

```
Push to Main
      │
      ▼
Install Dependencies
      │
      ▼
Run Tests
      │
      ▼
Build
```

Push to staging

```
Deploy to Staging
```

Release Tag

```
Deploy to Production
```

---

# Webhook Configuration

Configure GitHub Webhook to trigger Jenkins automatically.

GitHub Repository

Settings

↓

Webhooks

↓

Add Webhook

Payload URL

```
http://<jenkins-server-ip>:8080/github-webhook/
```

Content Type

```
application/json
```

Select

```
Just the push event
```

Save the webhook.

In Jenkins enable

```
GitHub hook trigger for GITScm polling
```

---

# GitHub Secrets Configuration

Store sensitive credentials inside GitHub Secrets.

Navigate to

```
Repository

↓

Settings

↓

Secrets and Variables

↓

Actions
```

Example Secrets

| Secret Name | Purpose |
|-------------|---------|
| HOST | Server IP |
| USERNAME | SSH Username |
| PASSWORD | SSH Password |
| SSH_KEY | SSH Private Key |
| API_TOKEN | Deployment Token |

Use them inside workflow

```yaml
env:
  HOST: ${{ secrets.HOST }}
  API_TOKEN: ${{ secrets.API_TOKEN }}
```

---

# Email Notification (Jenkins)

Jenkins can notify users after each build.

SMTP Example

```
SMTP Server : smtp.gmail.com

Port : 587

TLS : Enabled
```

Notifications

- Build Success
- Build Failure

---

# How to Run Locally

Clone repository

```bash
git clone https://github.com/<your-github-username>/flask_Practice.git
```

Go to project

```bash
cd flask_Practice
```

Create virtual environment

```bash
python3 -m venv venv
```

Activate environment

Linux/Mac

```bash
source venv/bin/activate
```

Windows

```powershell
venv\Scripts\activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

Run Flask application

```bash
python app.py
```

Application URL

```
http://127.0.0.1:5000
```

Run tests

```bash
pytest
```

---

# Screenshots

Include the following screenshots in the repository.

## Jenkins

- Jenkins Dashboard
- Pipeline Execution
- Build Stage
- Test Stage
- Deploy Stage
- Console Output
- Email Notification

---

## GitHub Actions

- Workflow Run
- Test Job
- Build Job
- Deploy to Staging
- Deploy to Production

---

# Repository Link

Original Repository

https://github.com/mohanDevOps-arch/flask_Practice

Forked Repository

https://github.com/<your-github-username>/flask_Practice

---

# Future Improvements

- Dockerize the Flask application
- Deploy using Kubernetes
- Integrate SonarQube for code quality
- Add code coverage reports
- Deploy to AWS EC2 or Azure App Service
- Add Slack or Microsoft Teams notifications

---

# Author

**Name:** Srishti Joshi

AWS Cloud Engineer | DevOps Engineer
