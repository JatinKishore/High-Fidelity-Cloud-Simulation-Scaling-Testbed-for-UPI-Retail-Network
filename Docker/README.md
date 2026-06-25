# Simulation Host: Infrastructure Provisioning & Container Orchestration

This module provides the core procedures for initializing the compute environment and managing the microservices fleet for the **High-Fidelity UPI Retail Network Simulation**. This environment is engineered to model distributed transaction flows and evaluate system performance under synthetic load.

---

## 1. Environment Initialization

We utilize an optimized **Amazon Linux 2023** host to minimize virtualization overhead and ensure a high-fidelity environment for containerized microservices.

### Infrastructure Setup

```bash
# System synchronization and security hardening
sudo dnf update -y

# Container runtime installation
sudo dnf install docker -y
sudo systemctl enable docker
sudo systemctl start docker

# Apply operational privileges
sudo usermod -aG docker ec2-user

```

> **Note:** Execute `newgrp docker` or re-authenticate your SSH session to apply permission changes.

---

## 2. Container Orchestration & Lifecycle

Our microservices fleet consists of modular components (Catalog, Cart, Checkout, Orders, UI) designed to simulate distributed retail transaction flows typical of a UPI ecosystem.

### Runtime Deployment

Use the following workflow to deploy simulation components:

```bash
# Pull validated service image
docker pull retail-store-ui:1.0.0

# Provision containerized service
docker run --name retail-ui -p 8888:8080 -d retail-store-ui:1.0.0

```

### Operational Management

* **Status Audit:** `docker ps`
* **Health Check:** `docker exec -it retail-ui curl http://localhost:8080`
* **Process Termination:** `docker stop retail-ui && docker rm retail-ui`

---

## 3. Custom Build Engineering

To simulate continuous feature deployment and iterative testing, we maintain a custom build pipeline for the retail microservices.

### Patching & Deployment

We automate the injection of configuration changes (e.g., UI version tagging) to validate deployment throughput:

```bash
# 1. Environment Preparation
mkdir ui-simulation && cd ui-simulation

# 2. Automated Configuration Patching
sed -i 's/Secret Shop<\/span>/Secret Shop - V2 Version<\/span>/' home.html

# 3. Custom Image Construction
docker build -t retail-store-ui:2.0.0 .

# 4. Registry Push (for cluster-wide deployment)
docker login
docker tag retail-store-ui:2.0.0 <YOUR_USER>/retail-store-ui:2.0.0
docker push <YOUR_USER>/retail-store-ui:2.0.0

```

---

## 4. Simulation Topology Logic

Our container architecture is designed to model high-concurrency retail transactions:

* **UI Service:** Manages client-side requests and session state.
* **Backend Fleet:** Java/Go microservices managing transaction integrity and order processing.
* **Event-Driven Backbone:** Integration with Redis and RabbitMQ to simulate asynchronous payment gateway communication.

---

## 5. Lifecycle Hygiene

To maintain environment fidelity and cost-optimized architectural standards, we adhere to the following:

1. **Automated Purging:** Use `docker system prune` to clear dangling layers post-simulation.
2. **Compute Decommissioning:** Always terminate the host instance after performance metric capture to adhere to cost-optimization policies.
3. **Security Posture:** Infrastructure is hardened via restricted Security Groups and the principle of least-privilege runtime access.

---

