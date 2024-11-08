# Multi-Service Kubernetes Deployment for Preschool and Skate Web Applications

This repository provides Kubernetes manifests for deploying and managing two web applications: **Preschool** and **Skate**. Each application is independently deployed with its own set of resources, including Deployments, Services, Horizontal Pod Autoscalers (HPA), and Ingress rules for external access.

## Architecture Overview

The setup includes the following:

1. **Preschool Web Application**
   - **Deployment**: Configured with rolling updates, resource limits, and scaling options.
   - **Service**: Exposed internally using ClusterIP.
   - **Horizontal Pod Autoscaler (HPA)**: Automatically scales based on CPU utilization.
   
2. **Skate Web Application**
   - **Deployment**: Similar to the Preschool app, with rolling updates and resource management.
   - **Service**: Exposed internally using ClusterIP.
   - **Horizontal Pod Autoscaler (HPA)**: Scales automatically based on CPU load.

3. **Ingress**: Provides external access to the applications using path-based routing.

## Components

### 1. Ingress

The Ingress resource routes incoming requests to each application based on URL paths:
- Requests to `/preschool` are directed to the **Preschool** service (`pre-school-svs`).
- Requests to `/skate` are directed to the **Skate** service (`skate-svs`).

### 2. Horizontal Pod Autoscalers (HPAs)

Each application includes an HPA that adjusts the number of running pods based on CPU usage:
- **Preschool HPA**: Scales between 1-4 replicas when CPU usage exceeds 70%.
- **Skate HPA**: Scales between 1-4 replicas, also at a 70% CPU threshold.

### 3. Deployments

Both web applications are deployed with:
- **Rolling update strategy** for smooth updates.
- **Resource limits and requests** to manage CPU and memory usage efficiently.
- **Replica count** set to 2 initially, with further scaling managed by the HPA.

### 4. Services

Each application has an internal **ClusterIP Service** to route traffic to its pods:
- **Preschool Service** (`pre-school-svs`) directs traffic to the Preschool app pods.
- **Skate Service** (`skate-svs`) directs traffic to the Skate app pods.

## Getting Started

To deploy the configurations:

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
2. Apply the configurations in the following order:
  kubectl apply -f ingress.yaml
  kubectl apply -f pre-school-deployment.yaml
  kubectl apply -f pre-school-service.yaml
  kubectl apply -f pre-school-hpa.yaml
  kubectl apply -f skate-deployment.yaml
  kubectl apply -f skate-service.yaml
  kubectl apply -f skate-hpa.yaml
## Notes
Ensure your Kubernetes cluster has an Ingress Controller (e.g., NGINX) to enable external access via Ingress.
Adjust replica counts, CPU/memory limits, and scaling parameters to suit your environment's needs.
Confirm that the required images (shaikkhajaibrahim/preschool:1.1 and shaikkhajaibrahim/skateboard:1.0) are accessible.


