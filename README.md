# High-Fidelity Cloud Simulation & Scaling Testbed for UPI-Retail Networks

## 1. Project Overview

This repository contains a high-fidelity cloud-native simulation environment designed to model, stress-test, and optimize the infrastructure requirements of a high-concurrency UPI-based retail payment network. The system leverages a microservices-based architecture to emulate complex transaction flows, state management, and messaging patterns typical of modern digital payment ecosystems.

The primary objective of this testbed is to evaluate the trade-offs between system availability, latency, and cost-optimized cloud resource allocation.

---

## 2. Architectural Design
![High-Fidelity Simulation Topology](images/Overview Architecture.png)
The simulation environment is architected as a distributed system, mimicking the modularity of production-grade financial gateways.

### Service Decomposition

* **Transaction Logic Layer:** Comprises core services (Catalog, Cart, Checkout, Orders) developed in polyglot environments (Go, Java Spring Boot, Node.js) to simulate heterogeneous service interdependencies.
* **Persistence & State Layer:** Utilizes a mix of relational (MySQL/PostgreSQL) and NoSQL (DynamoDB) databases to demonstrate data-driven scaling strategies.
* **Asynchronous Message Backbone:** Implements RabbitMQ to model event-driven architecture and transaction queuing.
* **Caching Strategy:** Leverages Redis for high-frequency state synchronization and performance optimization.

---

## 3. Engineering Focus Areas

This testbed serves as a sandbox for implementing rigorous DevOps and SRE principles:

* **Scalability Testing:** Evaluating horizontal and vertical auto-scaling behaviors under synthetic load.
* **Infrastructure Optimization:** Applying cost-efficient resource provisioning while maintaining strict performance SLAs.
* **Observability & Monitoring:** Centralized logging, tracing, and metric collection to monitor the health of high-throughput transaction flows.
* **Security Posture:** Enforcing strict network policies and secure service-to-service communication within the containerized ecosystem.

---

## 4. Technology Stack

* **Orchestration:** Kubernetes (EKS/K3s) for container lifecycle management.
* **Deployment:** Infrastructure as Code (IaC) using Terraform.
* **CI/CD:** Automated pipeline integration for rolling updates and canary deployments.
* **Observability:** Prometheus/Grafana stack for real-time performance telemetry.

---

## 5. Motivation & Design Philosophy

Unlike standard reference architectures, this project focuses on the **behavioral analysis of distributed systems.** By analyzing the trade-offs in database consistency, messaging overhead, and service latency, this testbed provides a sandbox to:

1. Quantify the impact of resource constraints on transaction success rates.
2. Develop automated remediation workflows for service bottlenecks.
3. Design cost-optimized architectures that survive regional failover scenarios.

---

## 6. Project References & Attribution

This architecture is based on a modular microservices pattern, utilizing foundational service components originally provided by the AWS Containers team and extended for custom infrastructure simulation.

* **Core Architecture Base:** [aws-containers/retail-store-sample-app](https://github.com/aws-containers/retail-store-sample-app)
* **Simulation Baseline:** [stacksimplify/retail-store-sample-app-aws](https://github.com/stacksimplify/retail-store-sample-app-aws)

*Disclaimer: This project is an independent engineering study designed for infrastructure benchmarking and does not represent the production environment or internal tools of NPCI.*

---
