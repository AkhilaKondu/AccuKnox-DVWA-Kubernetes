# AccuKnox DVWA Kubernetes Security Lab

A hands-on application security project demonstrating common web vulnerabilities using Damn Vulnerable Web Application (DVWA) deployed on a local Kubernetes cluster with Minikube and Docker.

This project was developed as part of the AccuKnox Solution Engineer Trainee assignment.

## Project Overview

The objective of this project is to deploy DVWA in a local Kubernetes environment, demonstrate three common web application attack surfaces, capture screenshots as evidence, and document security mitigations.

The lab is intended for authorized security testing in a local environment.

## Technologies Used

- Kubernetes
- Minikube
- Docker
- DVWA (Damn Vulnerable Web Application)
- MariaDB
- Kubernetes YAML
- HTML and CSS
- Git and GitHub

## Architecture

The application runs locally on a Minikube Kubernetes cluster.

The deployment includes:

- **DVWA application:** Web application used for security demonstrations.
- **MariaDB:** Database used by DVWA.
- **Kubernetes Deployment:** Manages the application and database pods.
- **Kubernetes Service:** Provides access to the DVWA application.
- **PersistentVolumeClaim:** Provides persistent storage for the database.
- **Kubernetes Secret:** Holds database credentials in the example configuration.

## Project Setup

### Prerequisites

Install and configure:

- Docker Desktop
- Minikube
- kubectl
- Git

Start your local Kubernetes cluster:

```bash
minikube start --driver=docker
```

Verify the cluster:

```bash
kubectl get nodes
```

Check the available pods:

```bash
kubectl get pods -A
```

### Deploying DVWA

The repository contains `k8s/dvwa.example.yaml`, an example Kubernetes manifest with placeholder credentials.

**Before deploying:** Copy the example manifest to a separate local file, replace the placeholder credentials with your own values, and configure the database credentials consistently. Do not commit real credentials to GitHub.

For example:

```bash
cp k8s/dvwa.example.yaml k8s/dvwa.local.yaml
```

Edit `k8s/dvwa.local.yaml` and replace the placeholder values before applying it.

Deploy the local configuration:

```bash
kubectl apply -f k8s/dvwa.local.yaml
```

Check deployment status:

```bash
kubectl get pods
kubectl get services
```

When the DVWA pod is ready, forward the service port:

```bash
kubectl port-forward service/dvwa 8081:80
```

Open the application locally:

http://127.0.0.1:8081

Use the credentials configured for your local DVWA installation.

**Note:** The example manifest is provided for reference. Adjust resource names or configuration if your local deployment differs.

## Attack Demonstrations

### 1. SQL Injection

**Objective:** Demonstrate how unsafe SQL query construction can expose unintended database records.

**Observation:** A crafted input returned multiple records instead of only the expected result.

**Mitigation:**
- Use parameterized SQL queries.
- Avoid constructing SQL statements by concatenating user input.
- Apply least-privilege database permissions.
- Validate input appropriately.

### 2. Reflected Cross-Site Scripting (XSS)

**Objective:** Demonstrate how untrusted input reflected into an HTTP response can execute JavaScript in a browser.

**Observation:** A test input triggered a JavaScript alert in the local DVWA application.

**Mitigation:**
- Use context-aware output encoding.
- Validate and sanitize input where appropriate.
- Apply a suitable Content Security Policy.
- Avoid inserting untrusted content directly into executable browser contexts.

### 3. OS Command Injection

**Objective:** Demonstrate how unsafe operating-system command construction can execute unintended commands.

**Observation:** The local demonstration displayed command output, including the web application's execution identity.

**Mitigation:**
- Avoid shell commands when safer APIs are available.
- Use strict input validation and allowlists.
- Avoid passing untrusted input to operating-system shells.
- Apply least privilege to the application process.

## Evidence and Screenshots

The `screenshots/` directory contains evidence captured during the local demonstrations.

| Screenshot | Description |
|---|---|
| `01-sql-injection.png` | SQL injection demonstration |
| `02-reflected-xss.png` | Reflected XSS demonstration |
| `03-command-injection.png` | Command injection demonstration |
| `04-dvwa-login.png` | DVWA login page, if included |

The login screenshot is optional. Add it to the `screenshots/` directory if you have captured it.

## Project Website

The project website documents the lab, demonstrations, and mitigations.

**Website:**  
https://akhilakondu.github.io/AccuKnox-DVWA-Kubernetes/

**GitHub Repository:**  
https://github.com/AkhilaKondu/AccuKnox-DVWA-Kubernetes

## Project Structure

```text
AccuKnox-DVWA-Kubernetes/
├── index.html
├── README.md
├── .gitignore
├── k8s/
│   └── dvwa.example.yaml
└── screenshots/
    ├── 01-sql-injection.png
    ├── 02-reflected-xss.png
    ├── 03-command-injection.png
    └── 04-dvwa-login.png
```

The login screenshot may be absent if it has not been captured yet. The local deployment manifest is intentionally excluded from the public repository when it contains local credentials.

## Security Considerations

DVWA is intentionally vulnerable and must only be used in an isolated, authorized testing environment.

- Do not expose the vulnerable application directly to the public internet.
- Do not deploy this demonstration configuration in production.
- Never commit real passwords, access tokens, or other secrets.
- Use secure configurations and least-privilege permissions for real applications.

## Conclusion

This project provided practical experience with local Kubernetes deployment, application security testing, evidence collection, and mitigation of common web vulnerabilities.

The demonstrations highlight why input handling, output encoding, safe command execution, and least-privilege access are important for application security.
