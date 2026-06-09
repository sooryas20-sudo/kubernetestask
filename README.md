# kubernetestask

# Kubernetes Infrastructure Isolation - Task

This project demonstrates the deployment of a local single-node Kubernetes cluster using **Minikube** on an AWS EC2 instance (Amazon Linux 2023 platform) and explores the core concepts of logical cluster multi-tenancy through **Kubernetes Namespaces**.

## 🛠️ Tech Stack & Drivers Used
* **Compute Infrastructure:** AWS EC2 (`t2.medium` instance to satisfy the minimum 2 vCPU / 2GB RAM master node constraint)
* **Host Operating System:** Amazon Linux 2023 (RPM-based platform)
* **Container Virtualization Driver:** Docker Engine v29.2.1
* **Orchestration Platform:** Minikube v1.35.1 (Kubernetes v1.35.1 Control Plane)
* **Cluster Management CLI:** Kubectl

---

## 🚀 Implementation & Setup Steps

### 1. Engine & Control Plane Setup
The instance package dependencies were brought up-to-date, the core Docker daemon engine was initialized, and non-root execution permissions were applied to the system user. 

```bash
# Deployed Docker Engine
sudo dnf install docker -y
sudo systemctl start docker && sudo systemctl enable docker
sudo usermod -aG docker ec2-user && newgrp docker

# Installed Control Plane Binary Components
curl -LO [https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64](https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64)
sudo install minikube-linux-amd64 /usr/local/bin/minikube

curl -LO "[https://dl.k8s.io/release/$](https://dl.k8s.io/release/$)(curl -L -s [https://dl.k8s.io/release/stable.txt](https://dl.k8s.io/release/stable.txt))/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
