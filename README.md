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

## Project SetUp

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

## Prerequisites
### This guide assumes an Ubuntu/Debian-like environment and sudo privileges.

# Installations

## System Update & Common Packages

```
sudo apt update
sudo apt upgrade -y

# Common tools : It installs commonly used tools required for DevOps, development, networking, package building, HTTPS communication, and certificates.
sudo apt install -y bash-completion wget git zip unzip curl jq net-tools build-essential ca-certificates apt-transport-https gnupg fontconfig

```
### Below is what each package does:

| Package | Purpose |
| ------ | ------ |
| bash-completion | Auto-complete commands |
| wget | Download files |
| git | Version control |
| zip/unzip | File compression |
| curl | API calls, downloads |
| jq | JSON processing |
| net-tools | Network troubleshooting   |
| build-essentialna|Compilers & build tools |
|ca-certificates|HTTPS certificate trust|
|apt-transport-https|Install via HTTPS|
|gnupg|Secure package verification|
|fontconfig|Font management|

## Reload bash completion if needed:

```
source /etc/bash_completion
```

## Install latest Git:

```
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git -y
```

# Java
## Install OpenJDK (choose 17 or 21 depending on your needs) :

```
# OpenJDK 17
sudo apt install -y openjdk-17-jdk

# OR OpenJDK 21
sudo apt install -y openjdk-21-jdk
```

### Verify:

```
java --version
```

# Jenkins

### Official docs: https://www.jenkins.io/doc/book/installing/linux/

```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install -y jenkins
sudo systemctl enable --now jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

```

#### Initial admin password:

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

```

#### Then open: http://your-server-ip:8080

#### Note: Jenkins requires a compatible Java runtime. Check the Jenkins documentation for supported Java versions.

## Jenkins Plugins to Install

- Eclipse Temurin installer
- NodeJS
- Email Extension
- OWASP Dependency-Check
- Pipeline: Stage View
- SonarQube Scanner
- Prometheus metrics
- Docker 
- Docker API
- Docker Commons
- Docker Pipeline
- docker-build-step

#### Note : Restart the jenkins after the installations of all the plugins

# Docker

### Official docs: https://docs.docker.com/engine/install/ubuntu/

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Add user to docker group (log out / in or newgrp to apply)
sudo usermod -aG docker $USER
newgrp docker
docker ps
```

#### If Jenkins needs Docker access:

```
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

#### Check Docker status:

```
sudo systemctl status docker
```

# Trivy (Vulnerability Scanner)
### Docs: https://trivy.dev/docs/latest/getting-started/installation/

```
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install -y trivy


trivy --version
```

# Prometheus
### Official downloads: https://prometheus.io/download/
#### Generic install steps:

```
# Create a prometheus user
sudo useradd --system --no-create-home --shell /usr/sbin/nologin prometheus

wget -O prometheus.tar.gz "https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz"
tar -xvf prometheus.tar.gz
cd prometheus-*/

sudo mkdir -p /data /etc/prometheus
sudo mv prometheus promtool /usr/local/bin/
sudo mv consoles/ console_libraries/ /etc/prometheus/
sudo mv prometheus.yml /etc/prometheus/prometheus.yml

sudo chown -R prometheus:prometheus /etc/prometheus /data
```
### Systemd service (/etc/systemd/system/prometheus.service) :

```
sudo vim /etc/systemd/system/prometheus.service
```

#### Add the below to /etc/systemd/system/prometheus.service

```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/data \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090

[Install]
WantedBy=multi-user.target
```

#### Enable & start:

```
sudo systemctl daemon-reload
sudo systemctl enable --now prometheus
sudo systemctl start prometheus
sudo systemctl status prometheus
```

### Access: http://ip-address:9090

# Node Exporter
### Docs: https://prometheus.io/docs/guides/node-exporter/

```
# come out the prometheus directory
cd ~

sudo useradd --system --no-create-home --shell /usr/sbin/nologin node_exporter

wget -O node_exporter.tar.gz "https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz"
tar -xvf node_exporter.tar.gz
sudo mv node_exporter-*/node_exporter /usr/local/bin/
rm -rf node_exporter*
```

### Systemd service: (/etc/systemd/system/node_exporter.service)
```
sudo vim /etc/systemd/system/node_exporter.service
```

```
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
ExecStart=/usr/local/bin/node_exporter --collector.logind

[Install]
WantedBy=multi-user.target
```
### Enable & start:

```
sudo systemctl daemon-reload
sudo systemctl enable --now node_exporter
sudo systemctl start node_exporter
sudo systemctl status node_exporter
```

### Prometheus scrape config:
#### Add to /etc/prometheus/prometheus.yml:

```
  - job_name: "node_exporter"
    static_configs:
      - targets: ["<ip-address>:9100"]

  - job_name: "jenkins"
    metrics_path: /prometheus
    static_configs:
      - targets: ["<jenkins-ip>:8080"]
```

#### Validate config:

```
promtool check config /etc/prometheus/prometheus.yml
sudo systemctl restart prometheus
```

# Grafana
### Docs: https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/
```
sudo apt-get install -y apt-transport-https software-properties-common wget

sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null

echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

sudo apt-get update
sudo apt-get install -y grafana

sudo systemctl daemon-reload
sudo systemctl enable --now grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```

##### Access: http://ip-address:3000

### Datasource: http://promethues-ip:9090

## Dashboard id
- Node_Exporter 1860 Docs: https://grafana.com/grafana/dashboards/1860-node-exporter-full/
- jenkins 9964 Docs: https://grafana.com/grafana/dashboards/9964-jenkins-performance-and-health-overview/
- kubernetes 18283 Docs: https://grafana.com/grafana/dashboards/18283-kubernetes-dashboard/

## SonarQube Docker Container Run for Analysis
```
docker run -d --name sonarqube \
  -p 9000:9000 \
  -v sonarqube_data:/opt/sonarqube/data \
  -v sonarqube_logs:/opt/sonarqube/logs \
  -v sonarqube_extensions:/opt/sonarqube/extensions \
  sonarqube:lts-community
```

```
docker ps
OR
docker images
```
### Access: http://ip-address:9000

## Jenkins Credentials to Store
|Purpose|ID (Should match with the JenkinsFile)|Type|Notes|
| ------ | ------ | ------ | ------ | 
|Email|mail-cred|Username/app password||
|SonarQube|sonar-token|Secret text|From SonarQube application|
|Docker Hub|docker-cred|Secret text|From your Docker Hub profile|

#### Webhook example: http://<jenkins-ip>:8080/sonarqube-webhook/

## Jenkins Tools Configuration:
 - JDK [jdk17]
 - SonarQube Scanner installations [sonar-scanner]
 - NodeJS [node16]
 - Dependency-Check installations [dp-check]
 - Docker installations [docker]

## Jenkins System Configuration
### SonarQube servers:
- Name: sonar-server
- URL: http://:9000
- Credentials: Add from Jenkins credentials

### Extended E-mail Notification:
- SMTP server: smtp.gmail.com
- SMTP Port: 465
- Use SSL
- Default user e-mail suffix: @gmail.com

### E-mail Notification:
- SMTP server: smtp.gmail.com
- Default user e-mail suffix: @gmail.com
- Use SMTP Authentication: Yes
- User Name: example@gmail.com
- Password: Use credentials
- Use TLS: Yes
- SMTP Port: 587
- Reply-To Address: example@gmail.com

## Build now and See the configuration pipeline of the jenkins  - End of CI
#### Note : You can access the application using the public-ip

# EKS cluster setup and ALB Ingress Kubernetes Setup
#### This covers the installation and setup for AWS CLI, kubectl, eksctl, and helm, and creating/configuring an EKS cluster with AWS Load Balancer Controller.

### 1. AWS CLI Installation
#### Refer: [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

```
sudo apt install -y unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
### 2. kubectl Installation

#### Refer: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
