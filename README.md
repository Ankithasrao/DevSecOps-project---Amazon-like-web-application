# Amazon DevSecOps CI/CD Project 🚀

This repository demonstrates a complete **end-to-end DevSecOps CI/CD pipeline** for an Amazon-like web application using modern **cloud-native, containerized, and security-first deployment practices**.  
It integrates **CI/CD automation, containerization, vulnerability scanning, Kubernetes orchestration, and monitoring** into a single workflow.

This project is ideal for:
- Learning **DevSecOps in real projects**
- Understanding **secure CI/CD pipelines**
- Deploying **containerized applications to Kubernetes**
- Practicing **monitoring and observability**

---

## 📌 Project Features

✅ Automated CI/CD using Jenkins  
✅ Docker containerization  
✅ Static code analysis & vulnerability scanning  
✅ Kubernetes-based deployment  
✅ Continuous monitoring with Prometheus & Grafana  
✅ DevSecOps best practices  
✅ Production-like deployment pipeline  

---

## 🏗️ High-Level Architecture

1. Developer pushes code to GitHub  
2. Jenkins pipeline is triggered automatically  
3. Code is built and tested  
4. Docker image is created  
5. Image is scanned for vulnerabilities  
6. Secure image is pushed to the registry  
7. Application is deployed to Kubernetes  
8. Monitoring is enabled using Prometheus & Grafana  

---

## 🛠️ Tools & Technologies Used

| Tool | Purpose |
|------|---------|
| GitHub | Source code management |
| Jenkins | CI/CD automation |
| Docker | Application containerization |
| Trivy | Docker image vulnerability scanning |
| SonarQube | Static code analysis & quality gates |
| Kubernetes | Container orchestration & deployment |
| Prometheus | Monitoring & metrics collection |
| Grafana | Visualization & dashboards |
| Ubuntu | Base OS for CI/CD & infrastructure |
| Node Exporter | System-level monitoring |

---

## 🔐 DevSecOps Implementation

Security is integrated at every stage of the pipeline:

- ✅ **Static Code Analysis** using SonarQube  
- ✅ **Container Image Scanning** using Trivy  
- ✅ **Secure Kubernetes Deployment**  
- ✅ **Monitoring & Alerting** for runtime security  

This ensures **shift-left security** and continuous compliance.

---

## 🔄 CI/CD Workflow

1. Code Commit → GitHub  
2. Jenkins Job Triggers  
3. Build & Unit Testing  
4. Docker Image Build  
5. Image Security Scan  
6. Push to Image Registry  
7. Deploy to Kubernetes  
8. Monitor with Prometheus & Grafana  

---

## 📁 Repository Structure (Sample)

```text
.
├── Jenkinsfile
├── Dockerfile
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
├── monitoring/
│   ├── prometheus.yaml
│   ├── grafana-dashboards/
├── src/
├── README.md
```

### Project SetUp

#### Ports to Enable in Security Group

| Service | Port |
| ------ | ------ |
| HTTP | 80 |
| HTTPS | 443 |
| SSH | 22 |
| Jenkins | 8080 |
| SonarQube | 9000 |
| Prometheus | 9090|
| Node Exporter | 9100   |
| Grafana|3000 |

### Prerequisites
### This guide assumes an Ubuntu/Debian-like environment and sudo privileges.
