# End-to-End DevSecOps CI/CD Platform on AWS

A complete end-to-end DevSecOps project demonstrating automated infrastructure provisioning, Continuous Integration, security and code quality validation, GitOps-based Continuous Deployment, Kubernetes orchestration, monitoring, and centralized logging on AWS.

The project deploys a full-stack Reddit Clone application consisting of a Django REST API backend and a Next.js frontend to Amazon EKS.

The complete delivery lifecycle is automated from source code changes to production-style Kubernetes deployment.

---

## Project Background

This project was developed as part of the final project for the National Telecommunication Institute (NTI) DevOps training program.

The complete platform was designed and implemented collaboratively by a team of five engineers.

The project was originally divided into separate repositories for Continuous Integration, Continuous Deployment, and Infrastructure as Code. This repository consolidates the three components into a single portfolio repository while preserving their original Git commit history.

The platform demonstrates a complete DevSecOps workflow covering infrastructure provisioning, automated CI pipelines, security scanning, containerization, GitOps delivery, Kubernetes deployment, monitoring, and centralized logging.

---

## My Contributions

As a member of the five-engineer team, my primary responsibility was designing and implementing the Continuous Integration and DevSecOps pipeline.

My contributions included:

- Designing and implementing Jenkins CI pipelines for the backend and frontend applications.
- Designing the CI workflow and defining the different pipeline stages and quality gates.
- Creating and optimizing Docker images for the Django backend and Next.js frontend.
- Implementing multi-stage Docker builds and running application containers as non-root users.
- Integrating SonarQube for static code analysis and code quality validation.
- Configuring SonarQube Quality Gates to validate code quality before container images are published.
- Integrating OWASP Dependency Check to detect vulnerable application dependencies.
- Integrating Trivy to scan Docker images for HIGH and CRITICAL vulnerabilities.
- Implementing automated application testing and code coverage reporting.
- Integrating security and quality checks as blocking CI pipeline gates.
- Publishing validated Docker images to Amazon ECR using commit SHA-based image tags.
- Implementing GitHub Actions CI workflows for both backend and frontend applications.
- Implementing path-based change detection to trigger the appropriate CI workflow.
- Automating the update of Helm image tags in the GitOps CD repository after successful CI execution.
- Connecting the CI workflow with the GitOps deployment process used by Argo CD.
- Implementing CI pipeline success and failure notifications through n8n webhooks.

My main focus throughout the project was CI automation, containerization, code quality, and DevSecOps security controls.

---

## Architecture Overview

The platform follows a complete automated DevSecOps delivery workflow:

```text
Developer
    |
    v
GitHub
    |
    v
CI Pipeline
Jenkins / GitHub Actions
    |
    +--> Dependency Security Scan
    |        OWASP Dependency Check
    |
    +--> Automated Tests
    |        pytest / Jest
    |
    +--> Code Quality Analysis
    |        SonarQube
    |        Quality Gate
    |
    +--> Docker Image Build
    |
    +--> Container Security Scan
    |        Trivy
    |
    v
Amazon ECR
    |
    v
Update Helm Image Tag
    |
    v
GitOps Repository
    |
    v
Argo CD
    |
    v
Amazon EKS
    |
    +--> Django Backend
    |
    +--> Next.js Frontend
    |
    +--> Prometheus / Grafana
    |
    +--> Elasticsearch / Kibana / Filebeat
```

---

## End-to-End Workflow

1. A developer pushes application changes to GitHub.
2. The CI workflow detects whether the backend or frontend source code has changed.
3. Application dependencies are installed.
4. OWASP Dependency Check scans application dependencies for known vulnerabilities.
5. Automated application tests are executed.
6. Code coverage reports are generated.
7. SonarQube performs static code analysis.
8. The SonarQube Quality Gate validates code quality requirements.
9. A Docker image is built using a multi-stage Dockerfile.
10. Trivy scans the Docker image for HIGH and CRITICAL vulnerabilities.
11. Only validated Docker images are pushed to Amazon ECR.
12. Images are tagged using the Git commit SHA.
13. The CI workflow updates the corresponding image tag in the Helm values file.
14. The GitOps repository is updated automatically.
15. Argo CD detects the Git change.
16. Argo CD synchronizes the desired state with the Amazon EKS cluster.
17. The new application version is deployed to Kubernetes.
18. Prometheus and Grafana provide monitoring and observability.
19. Filebeat, Elasticsearch, and Kibana provide centralized logging.
20. n8n sends pipeline status notifications.

---

## Repository Structure

```text
NTI-end-to-end-devops-ci-cd-project/
|
├── ci/
|   ├── .github/
|   |   └── workflows/
|   ├── docs/
|   └── src/
|       ├── backend/
|       |   ├── Dockerfile
|       |   ├── Jenkinsfile
|       |   └── ...
|       |
|       └── frontend/
|           ├── Dockerfile
|           ├── JenkinsFile
|           └── ...
|
├── cd/
|   ├── argocd/
|   |   ├── apps/
|   |   ├── install/
|   |   └── root-app.yaml
|   |
|   ├── helm-charts/
|   |   ├── backend/
|   |   ├── frontend/
|   |   ├── gateway/
|   |   ├── monitoring/
|   |   ├── elasticsearch/
|   |   ├── kibana/
|   |   └── filebeat/
|   |
|   ├── k8s/
|   └── n8n/
|
├── infrastructure/
|   ├── modules/
|   ├── .github/
|   |   └── workflows/
|   └── ...
|
└── README.md
```

The three major directories preserve the original commit history of the separate project repositories using Git subtree integration.

---

## Technology Stack

| Category | Technologies |
|---|---|
| Cloud | AWS |
| Infrastructure as Code | Terraform |
| Containerization | Docker |
| Container Registry | Amazon ECR |
| Container Orchestration | Kubernetes, Amazon EKS |
| Continuous Integration | Jenkins, GitHub Actions |
| Continuous Deployment | Argo CD |
| GitOps | Git, GitHub, Argo CD |
| Package Management | Helm |
| Code Quality | SonarQube |
| Dependency Security | OWASP Dependency Check |
| Container Security | Trivy |
| Monitoring | Prometheus, Grafana |
| Logging | Elasticsearch, Kibana, Filebeat |
| Notifications | n8n |
| Backend | Django, Django REST Framework |
| Frontend | Next.js, TypeScript |
| Database | Amazon RDS for PostgreSQL |
| Object Storage | Amazon S3 |
| TLS | cert-manager, Let's Encrypt |
| Traffic Management | Kubernetes Gateway API, NGINX Gateway Fabric |

---

## Continuous Integration

The CI layer validates application changes before they are allowed to enter the deployment workflow.

The project contains CI implementations using both Jenkins and GitHub Actions.

### Jenkins Pipelines

Jenkins pipelines were designed for the backend and frontend applications.

The pipelines automate:

```text
Checkout
   |
   v
Install Dependencies
   |
   v
Dependency Security Scan
   |
   v
Application Tests
   |
   v
Code Quality Analysis
   |
   v
SonarQube Quality Gate
   |
   v
Docker Image Build
   |
   v
Trivy Image Scan
   |
   v
Push Image
   |
   v
Trigger GitOps Workflow
```

Pipeline definitions are available in:

```text
ci/src/backend/Jenkinsfile
ci/src/frontend/JenkinsFile
```

---

## GitHub Actions CI

GitHub Actions workflows provide automated CI pipelines for both application components.

```text
ci/.github/workflows/backend-ci.yml
ci/.github/workflows/frontend-ci.yml
```

The workflows support path-based change detection, allowing backend and frontend pipelines to execute only when their respective application source code changes.

### Backend Pipeline

| Stage | Tool | Purpose |
|---|---|---|
| Change Detection | dorny/paths-filter | Detect backend source changes |
| Dependency Installation | pip | Install Python dependencies |
| Dependency Scan | OWASP Dependency Check | Detect vulnerable dependencies |
| Unit Tests | pytest | Execute backend tests |
| Code Coverage | coverage | Generate coverage reports |
| Code Quality | SonarQube | Static code analysis |
| Quality Gate | SonarQube | Validate quality requirements |
| Docker Build | Docker | Build backend container image |
| Image Scan | Trivy | Scan image vulnerabilities |
| Registry Push | Amazon ECR | Publish validated image |
| GitOps Update | Git / yq | Update Helm image tag |
| Notification | n8n | Report pipeline status |

### Frontend Pipeline

| Stage | Tool | Purpose |
|---|---|---|
| Change Detection | dorny/paths-filter | Detect frontend source changes |
| Dependency Installation | npm | Install Node.js dependencies |
| Dependency Scan | OWASP Dependency Check | Detect vulnerable dependencies |
| Linting | ESLint | Validate source code |
| Type Checking | TypeScript | Validate application types |
| Build | Next.js | Build production application |
| Code Quality | SonarQube | Static code analysis |
| Quality Gate | SonarQube | Validate quality requirements |
| Docker Build | Docker | Build frontend container image |
| Image Scan | Trivy | Scan image vulnerabilities |
| Registry Push | Amazon ECR | Publish validated image |
| GitOps Update | Git / yq | Update Helm image tag |
| Notification | n8n | Report pipeline status |

---

## DevSecOps Security Gates

Security is integrated directly into the CI workflow rather than being treated as a separate final step.

The pipelines implement multiple security checkpoints.

| Security Gate | Tool | Scope |
|---|---|---|
| Dependency Vulnerability Scanning | OWASP Dependency Check | Application dependencies |
| Static Code Analysis | SonarQube | Application source code |
| Code Quality Gate | SonarQube Quality Gate | Bugs, code smells, coverage |
| Container Vulnerability Scanning | Trivy | Docker images |
| Registry Image Scanning | Amazon ECR | Published container images |

### OWASP Dependency Check

OWASP Dependency Check scans application dependencies for publicly known vulnerabilities.

The CI pipeline is configured to reject dependencies that exceed the configured CVSS vulnerability threshold.

### SonarQube

SonarQube performs static code analysis for both backend and frontend applications.

The analysis evaluates:

- Bugs
- Code smells
- Maintainability
- Code coverage
- Quality Gate status

The CI pipeline waits for the SonarQube Quality Gate result before continuing.

A failed Quality Gate prevents an invalid build from progressing through the delivery workflow.

### Trivy

Trivy scans the final Docker images before they are pushed to Amazon ECR.

The pipeline checks operating system packages and application dependencies inside the container image.

HIGH and CRITICAL vulnerabilities are configured as blocking conditions in the CI workflow.

---

## Containerization

Both application components are fully containerized.

### Backend Image

The Django backend uses a multi-stage Docker build.

Key container practices include:

- Python 3.12 slim base image
- Separate build and runtime stages
- Reduced final image contents
- Non-root runtime user
- Gunicorn application server
- Commit SHA-based image versioning

### Frontend Image

The Next.js frontend uses a multi-stage Docker build.

The build separates:

```text
Dependencies
    |
    v
Application Build
    |
    v
Minimal Runtime Image
```

Key practices include:

- Alpine-based Node.js image
- Multi-stage Docker build
- Next.js standalone output
- Non-root runtime user
- Reduced runtime image contents
- Commit SHA-based image versioning

---

## Infrastructure as Code

The AWS infrastructure is provisioned using Terraform.

The infrastructure follows a modular design and provisions the complete environment required by the application.

### AWS Resources

The Terraform configuration provisions:

- Amazon VPC
- Public subnets
- Private subnets
- Internet Gateway
- NAT Gateway
- Route tables
- Security Groups
- Amazon EKS
- EKS Managed Node Group
- Amazon RDS for PostgreSQL
- Amazon S3
- Amazon ECR
- IAM roles and policies

### Network Architecture

The VPC spans two Availability Zones in `us-east-1`.

```text
VPC 10.0.0.0/16
|
+-- us-east-1a
|   |
|   +-- Public Subnet
|   +-- Private Subnet
|
+-- us-east-1b
    |
    +-- Public Subnet
    +-- Private Subnet
```

EKS worker nodes and the RDS database are deployed in private subnets.

Private resources use a NAT Gateway for outbound internet connectivity.

### Terraform State

Terraform remote state is stored using:

- Amazon S3
- DynamoDB state locking

The project uses a dual-account architecture separating the Terraform state account from the AWS account hosting the application infrastructure.

---

## GitOps Continuous Deployment

Continuous Deployment is implemented using Argo CD and Helm.

The Git repository acts as the source of truth for the desired Kubernetes state.

After a successful CI pipeline:

```text
CI Pipeline
    |
    v
Update Helm values.yaml
    |
    v
Git Commit
    |
    v
GitOps Repository
    |
    v
Argo CD Detects Change
    |
    v
Argo CD Sync
    |
    v
Amazon EKS
```

Argo CD automatically reconciles the Kubernetes cluster with the desired state stored in Git.

---

## Argo CD App-of-Apps Pattern

The project implements the Argo CD App-of-Apps pattern.

A root Argo CD Application manages the platform applications.

```text
Root Application
|
+-- Gateway
+-- Backend
+-- Frontend
+-- Monitoring
+-- Elasticsearch
+-- Kibana
+-- Filebeat
```

Argo CD sync waves control the deployment order of platform components.

| Sync Wave | Component |
|---|---|
| 0 | Gateway and TLS |
| 1 | Backend |
| 2 | Frontend |
| 3 | Monitoring and Elasticsearch |
| 4 | Kibana and Filebeat |

---

## Kubernetes and Helm

Application and platform components are packaged using Helm charts.

The repository includes Helm charts for:

- Django backend
- Next.js frontend
- NGINX Gateway
- Monitoring stack
- Elasticsearch
- Kibana
- Filebeat

Kubernetes resources include:

- Deployments
- Services
- ConfigMaps
- Secrets
- HTTPRoutes
- Horizontal Pod Autoscalers
- NetworkPolicies
- ServiceMonitors
- Kubernetes Jobs

---

## Monitoring and Observability

The monitoring stack is based on `kube-prometheus-stack`.

It includes:

- Prometheus
- Grafana
- Alertmanager
- node-exporter

The Django application exposes Prometheus metrics through the `/metrics` endpoint.

A Kubernetes ServiceMonitor configures Prometheus to automatically scrape backend metrics.

Grafana provides application and cluster visualization.

---

## Centralized Logging

The platform uses the ELK stack for centralized Kubernetes logging.

### Logging Flow

```text
Kubernetes Pods
    |
    v
Filebeat
    |
    v
Elasticsearch
    |
    v
Kibana
```

Filebeat runs as a DaemonSet and collects container logs from Kubernetes nodes.

Logs are forwarded to Elasticsearch for storage and indexing.

Kibana provides log search and visualization.

---

## Networking and TLS

The application uses the Kubernetes Gateway API with NGINX Gateway Fabric.

Traffic flow:

```text
Internet
    |
    v
NGINX Gateway
    |
    +--> Frontend HTTPRoute
    |
    +--> Backend HTTPRoute
```

TLS certificate management is automated using cert-manager and Let's Encrypt.

HTTP traffic is redirected to HTTPS.

---

## Application Stack

### Backend

The backend is implemented using:

- Python 3.12
- Django
- Django REST Framework
- JWT authentication
- Gunicorn
- PostgreSQL
- Amazon S3 integration
- django-prometheus

The backend exposes Kubernetes readiness and liveness health endpoints and Prometheus metrics.

### Frontend

The frontend is implemented using:

- Next.js
- React
- TypeScript
- Chakra UI
- Recoil
- Axios

The application provides community, post, comment, voting, and authentication functionality.

---

## Image Versioning Strategy

Docker images are tagged using the Git commit SHA.

Example:

```text
reddit-backend:a1b2c3d
reddit-frontend:a1b2c3d
```

This provides traceability between:

```text
Git Commit
    |
    v
CI Pipeline
    |
    v
Docker Image
    |
    v
Kubernetes Deployment
```

Each deployed container image can be traced back to the exact source code revision that created it.

---

## Key DevOps Practices Demonstrated

- Infrastructure as Code
- Modular Terraform architecture
- Automated CI pipelines
- Jenkins Pipeline as Code
- GitHub Actions
- DevSecOps security integration
- Shift-left security testing
- Automated dependency scanning
- Static code analysis
- Automated Quality Gates
- Container vulnerability scanning
- Multi-stage Docker builds
- Non-root containers
- Immutable commit-based image versioning
- GitOps Continuous Deployment
- Argo CD App-of-Apps pattern
- Helm-based Kubernetes deployments
- Kubernetes Gateway API
- Automated TLS management
- Kubernetes monitoring
- Centralized container logging
- CI/CD notifications
- Automated infrastructure lifecycle management

---

## Detailed Documentation

Each project component contains its own detailed documentation.

### Continuous Integration

See:

```text
ci/README.md
```

Contains detailed application and CI pipeline documentation.

### Continuous Deployment

See:

```text
cd/README.md
```

Contains detailed Argo CD, Helm, Kubernetes, monitoring, logging, and GitOps documentation.

### Infrastructure

See:

```text
infrastructure/README.md
```

Contains detailed Terraform and AWS infrastructure documentation.

---

## Original Project Repositories

The project was originally developed across separate repositories for CI, CD, and infrastructure.

This repository combines the three project components into a single portfolio view while preserving the original Git history.

- CI: `https://github.com/MohammedMourad1/nti-final-project-ci`
- CD: `https://github.com/MohammedMourad1/nti-final-project-cd`
- Infrastructure: `https://github.com/MohammedMourad1/nti-final-project-infra`

---

## Author

Mohammed Mourad

DevOps and Cloud Engineer

GitHub: `https://github.com/MohammedMourad1`

---

## Acknowledgments

This project was developed collaboratively by a team of five engineers as part of the National Telecommunication Institute (NTI) DevOps training program final project.

The complete platform represents the combined work of the team across cloud infrastructure, Kubernetes, Continuous Integration, GitOps Continuous Deployment, monitoring, logging, and application delivery.

My primary contribution focused on the Continuous Integration and DevSecOps implementation, including Jenkins pipeline design, Docker image creation, GitHub Actions workflows, SonarQube code quality analysis, OWASP dependency vulnerability scanning, Trivy container image scanning, automated testing, and CI-to-GitOps integration.
