# DevOps-03-Pipeline-Aws-GitOps

## About

This project demonstrates a CI/CD pipeline using GitOps practices, integrating various DevOps tools and AWS services. The primary tools and technologies utilized in this pipeline include Jenkins, Java, GitHub, Maven, Docker, Kubernetes, SonarQube, ArgoCD, Trivy, and AWS Cloud.

## Table of Contents

- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Pipeline Steps](#pipeline-steps)
- [Getting Started](#getting-started)
- [Installation](#installation)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [References](#references)

---

## Project Overview

This project aims to automate the CI/CD process from code commits to deployment on a Kubernetes cluster, ensuring code quality and security through tools like SonarQube and Trivy. 

## Technologies Used

- **Jenkins**: Continuous integration server.
- **Java**: Application programming language.
- **GitHub**: Source code repository.
- **Maven**: Dependency management and build automation.
- **Docker & DockerHub**: Containerization and image repository.
- **Kubernetes**: Container orchestration.
- **SonarQube**: Code quality and security analysis.
- **ArgoCD**: GitOps-based continuous delivery.
- **Trivy**: Security scanning for containers.
- **AWS Cloud**: Infrastructure and cloud services.

---

## Pipeline Steps

Below are the key steps in this pipeline. Each section contains detailed instructions on how to set up, configure, and execute each step.

### Step 1: Set Up Jenkins Master and Agent on AWS EC2

1. Launch EC2 instances for Jenkins Master and Jenkins Agent.
2. Install Java, Docker, and Jenkins on Master and Agent nodes.
3. Configure SSH authentication between Master and Agent nodes.
4. Set up Jenkins pipeline to execute on the Agent node.

### Step 2: Configure Jenkins for GitHub Integration

1. Generate a GitHub token and save it in Jenkins.
2. Install required plugins (e.g., GitHub Integration, Pipeline).
3. Configure Jenkins to pull code from the GitHub repository on each commit.

### Step 3: Configure SonarQube on a Separate EC2 Instance

1. Launch an EC2 instance for SonarQube and configure Java and PostgreSQL.
2. Install SonarQube, configure it with PostgreSQL, and open port 9000.
3. Set up a SonarQube webhook for Jenkins integration.

### Step 4: Jenkins Pipeline Configuration (Jenkinsfile)

The pipeline is defined in a `Jenkinsfile` with stages such as:
- Code Checkout from GitHub
- Build with Maven
- Run Tests
- SonarQube Analysis
- Build and Push Docker Image to DockerHub
- Security Scan with Trivy
- Deploy to Kubernetes via ArgoCD

### Step 5: Configure DockerHub for CI/CD Integration

1. Create a DockerHub token and add it to Jenkins.
2. Configure Jenkins to push Docker images to DockerHub.

### Step 6: Create EKS Cluster with eksctl

1. Set up AWS CLI and eksctl on a bootstrap server.
2. Create an EKS cluster with 3 nodes using `eksctl`.
3. Configure `kubectl` to interact with the EKS cluster.

### Step 7: Install and Configure ArgoCD on EKS

1. Install ArgoCD in a dedicated namespace on the EKS cluster.
2. Expose ArgoCD server to external access and configure CLI on the bootstrap server.
3. Configure applications in ArgoCD for GitOps-based deployment.

### Step 8: Integrate Jenkins with SonarQube, DockerHub, and ArgoCD

1. Set up the SonarQube token in Jenkins for code analysis.
2. Set up DockerHub credentials in Jenkins for pushing images.
3. Set up ArgoCD integration for deploying to Kubernetes.

---

## Getting Started

### Prerequisites

- AWS Account
- Jenkins, GitHub, and DockerHub accounts
- Access to AWS CLI, eksctl, kubectl, and ArgoCD CLI

---

## Installation

### Step-by-Step Guide

1. **Create and Configure EC2 Instances**: Follow the setup steps for each EC2 instance.
2. **Install Tools**: Install Jenkins, Docker, SonarQube, etc., as per instructions.
3. **Configure CI/CD Pipeline**: Use the provided `Jenkinsfile` to set up the pipeline stages.
4. **Set Up GitOps with ArgoCD**: Link ArgoCD with the GitHub repository and Kubernetes cluster.

---

## Usage

1. **Start Jenkins Pipeline**: Trigger builds manually or automatically upon code changes.
2. **Monitor ArgoCD for Deployments**: Access ArgoCD UI to see deployment status.
3. **Review SonarQube Reports**: Access SonarQube UI to review code quality reports.

---

## Troubleshooting

### Common Issues

- **SSH Authentication**: Ensure the SSH keys are correctly set up between Jenkins Master and Agent.
- **SonarQube Access**: Verify that port 9000 is open and accessible.
- **Docker Image Push Failures**: Ensure DockerHub credentials are correctly configured in Jenkins.

---

## References

- [AWS Documentation](https://aws.amazon.com/documentation/)
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [ArgoCD Documentation](https://argo-cd.readthedocs.io/)
- [SonarQube Documentation](https://docs.sonarqube.org/)
- [Docker Documentation](https://docs.docker.com/)
- [Trivy Documentation](https://aquasecurity.github.io/trivy/v0.18.3/)

---

