# AccuKnox DVWA Kubernetes Security Lab

## Project Overview
This project deploys Damn Vulnerable Web Application (DVWA) on a local Kubernetes cluster using Minikube and Docker.

The objective is to demonstrate common web application vulnerabilities in an authorized local security lab.

## Technologies Used
- Kubernetes
- Minikube
- Docker
- DVWA
- YAML
- HTML and CSS

## Attack Demonstrations

### 1. SQL Injection
Demonstrated how unsafe SQL queries can expose unintended database records.

**Mitigation:** Use parameterized queries and least-privilege database accounts.

### 2. Reflected Cross-Site Scripting (XSS)
Demonstrated how untrusted input can execute JavaScript in a browser.

**Mitigation:** Use context-aware output encoding and validate input.

### 3. OS Command Injection
Demonstrated how unsafe command construction can execute unintended operating-system commands.

**Mitigation:** Avoid shell commands where possible and validate input.

## Project Structure

```text
AccuKnox-DVWA-Kubernetes/
├── index.html
├── README.md
├── k8s/
│   └── dvwa.yaml
└── screenshots/
