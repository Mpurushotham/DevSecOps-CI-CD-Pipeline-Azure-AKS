# 🚀 Azure DevSecOps CI/CD Pipeline for AKS

[![Build Status](https://dev.azure.com/your-org/ecommerce-app/_apis/build/status/main-pipeline?branchName=main)](https://dev.azure.com/your-org/ecommerce-app/_build/latest?definitionId=1&branchName=main)
[![Security Rating](https://sonarqube.company.com/api/project_badges/measure?project=ecommerce-app&metric=security_rating)](https://sonarqube.company.com/dashboard?id=ecommerce-app)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> Enterprise-grade DevSecOps CI/CD pipeline for deploying a 3-tier e-commerce application to Azure Kubernetes Service with comprehensive security scanning at every stage.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Features](#-features)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Pipeline Stages](#-pipeline-stages)
- [Security](#-security)
- [Deployment](#-deployment)
- [Monitoring](#-monitoring)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

This repository contains a production-ready, enterprise-grade DevSecOps CI/CD pipeline that implements **Security at Every Stage** (Shift-Left Security) for deploying applications to Azure Kubernetes Service.

### Key Statistics

| Metric | Value |
|--------|-------|
| **Pipeline Stages** | 11 comprehensive stages |
| **Security Scans** | 12 different security tools |
| **Deployment Time** | ~2.5 hours (full production) |
| **Rollback Time** | 2 minutes (automated) |
| **Test Coverage** | Unit, Integration, E2E, Performance, DAST |
| **Deployment Strategy** | Blue-Green (Zero Downtime) |
| **Uptime Target** | 99.9% |

### What This Pipeline Does

✅ Scans code for secrets and vulnerabilities  
✅ Validates infrastructure security  
✅ Builds and scans container images  
✅ Runs comprehensive testing  
✅ Deploys with zero downtime  
✅ Monitors and alerts automatically  
✅ Generates compliance reports  

---

## 🏗️ Architecture

### 3-Tier Application Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     PRESENTATION TIER                        │
│                                                               │
│  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓  │
│  ┃  Frontend (React SPA)                                 ┃  │
│  ┃  • Nginx web server                                   ┃  │
│  ┃  • Client-side rendering                              ┃  │
│  ┃  • 3-15 replicas (auto-scaling)                       ┃  │
│  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛  │
└────────────────────────────┬────────────────────────────────┘
                             │
                             │ HTTPS/TLS
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                     APPLICATION TIER                         │
│                                                               │
│  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓  │
│  ┃  Backend API (Node.js/Express)                        ┃  │
│  ┃  • RESTful API endpoints                              ┃  │
│  ┃  • JWT authentication                                 ┃  │
│  ┃  • Business logic layer                               ┃  │
│  ┃  • 3-20 replicas (auto-scaling)                       ┃  │
│  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛  │
└────────────────────────────┬────────────────────────────────┘
                             │
                             │ PostgreSQL Protocol
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                         DATA TIER                            │
│                                                               │
│  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓  │
│  ┃  PostgreSQL Database                                  ┃  │
│  ┃  • StatefulSet deployment                             ┃  │
│  ┃  • Persistent volume storage                          ┃  │
│  ┃  • Automated backups (30-day retention)               ┃  │
│  ┃  • High availability enabled                          ┃  │
│  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛  │
└─────────────────────────────────────────────────────────────┘
```

### Azure Infrastructure

```
Azure Subscription
├── Resource Group (rg-ecommerce-prod)
│   ├── Azure Kubernetes Service (AKS)
│   │   ├── System Node Pool (3-10 nodes)
│   │   └── User Node Pool (3-20 nodes)
│   ├── Azure Container Registry (ACR)
│   ├── Azure Key Vault
│   ├── Azure Database for PostgreSQL
│   ├── Application Insights
│   ├── Log Analytics Workspace
│   ├── Virtual Network
│   │   ├── AKS Subnet
│   │   ├── Database Subnet
│   │   └── Network Security Groups
│   └── Storage Account (Backups)
```

---

## ✨ Features

### 🔒 Security Features

- **12-Layer Security Scanning**
  - Secret detection (Gitleaks)
  - SAST (SonarQube, Snyk)
  - IaC scanning (Checkov, tfsec)
  - Container scanning (Trivy)
  - DAST (OWASP ZAP)
  - Policy enforcement (OPA/Conftest)
  - Image signing (Cosign)
  - CIS Kubernetes benchmarks

- **Secrets Management**
  - Azure Key Vault integration
  - No secrets in code or config
  - Automatic secret rotation

- **Network Security**
  - Network policies for isolation
  - Private endpoints for ACR
  - TLS/SSL everywhere

- **Access Control**
  - Azure AD integration
  - RBAC for Kubernetes
  - Least privilege principles

### 🚀 DevOps Features

- **Zero-Downtime Deployments**
  - Blue-green deployment strategy
  - Automated smoke tests
  - Instant rollback (2 minutes)

- **Automated Testing**
  - Unit tests (Jest/Mocha)
  - Integration tests (Newman/Postman)
  - E2E tests (Playwright)
  - Performance tests (K6)
  - Security tests (OWASP ZAP)

- **Infrastructure as Code**
  - Terraform for Azure resources
  - Kubernetes manifests
  - Helm charts
  - Version controlled

- **Monitoring & Observability**
  - Application Insights APM
  - Azure Monitor for containers
  - Custom dashboards
  - Proactive alerting

### 🔄 CI/CD Features

- **Automated Pipeline**
  - Triggered on git push
  - Branch-based workflows
  - Manual approval gates
  - Parallel execution

- **Quality Gates**
  - Code coverage >80%
  - No critical vulnerabilities
  - Security policies enforced
  - Performance baselines met

- **Compliance & Reporting**
  - Automated compliance checks
  - SBOM generation
  - Audit trails
  - Security reports

---

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have:

- Azure subscription with Owner role
- Azure DevOps organization
- Azure CLI installed
- kubectl installed
- Terraform installed (v1.6+)
- Docker installed
- Git installed

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/azure-devsecops-pipeline.git
cd azure-devsecops-pipeline
```

### 2. Set Up Azure Resources

```bash
# Login to Azure
az login

# Set your subscription
az account set --subscription "Your-Subscription-Name"

# Create resource group for Terraform state
az group create --name rg-terraform-state --location eastus

# Create storage account for Terraform state
az storage account create \
  --name sttfstateprod \
  --resource-group rg-terraform-state \
  --location eastus \
  --sku Standard_LRS

# Create container
az storage container create \
  --name tfstate \
  --account-name sttfstateprod
```

### 3. Create Service Principal

```bash
# Create service principal for pipeline
az ad sp create-for-rbac \
  --name sp-devops-pipeline \
  --role Contributor \
  --scopes /subscriptions/{subscription-id} \
  --sdk-auth > azure-credentials.json

# Save the output - you'll need it for Azure DevOps
```

### 4. Configure Azure DevOps

1. **Import Repository**
   - Go to Azure DevOps
   - Create new project: `ecommerce-app`
   - Import this repository

2. **Create Service Connections**
   - Go to Project Settings → Service connections
   - Create Azure Resource Manager connection
   - Create Kubernetes service connections (staging & production)

3. **Create Variable Groups**
   - Go to Pipelines → Library
   - Create `ecommerce-prod-secrets` variable group
   - Add required secrets (see [Configuration](#configuration))

4. **Create Pipeline**
   - Go to Pipelines → Create Pipeline
   - Select your repository
   - Use existing YAML: `.azure-pipelines/azure-pipelines.yml`
   - Save and run

### 5. Deploy Infrastructure

```bash
# Navigate to Terraform directory
cd infrastructure/terraform

# Initialize Terraform
terraform init

# Review plan
terraform plan -out=tfplan

# Apply (creates AKS, ACR, Key Vault, etc.)
terraform apply tfplan
```

### 6. First Deployment

```bash
# Create feature branch
git checkout -b feature/initial-setup

# Push to trigger pipeline
git add .
git commit -m "Initial setup"
git push origin feature/initial-setup

# Create pull request in Azure DevOps
# Pipeline will run automatically
# Merge to main to deploy to production
```

---

## 📁 Project Structure

```
azure-devsecops-pipeline/
│
├── .azure-pipelines/
│   ├── azure-pipelines.yml           # Main CI/CD pipeline
│   ├── templates/
│   │   ├── security-scan.yml         # Security scanning template
│   │   ├── build-stage.yml           # Build stage template
│   │   └── deploy-stage.yml          # Deployment template
│   └── variables/
│       ├── dev.yml                   # Dev environment variables
│       ├── staging.yml               # Staging variables
│       └── production.yml            # Production variables
│
├── src/
│   ├── frontend/                     # React frontend application
│   │   ├── public/
│   │   ├── src/
│   │   │   ├── components/
│   │   │   ├── pages/
│   │   │   ├── services/
│   │   │   ├── utils/
│   │   │   └── App.js
│   │   ├── tests/
│   │   ├── Dockerfile
│   │   ├── nginx.conf
│   │   ├── package.json
│   │   └── .env.example
│   │
│   └── backend/                      # Node.js backend API
│       ├── src/
│       │   ├── controllers/
│       │   ├── models/
│       │   ├── routes/
│       │   ├── middleware/
│       │   ├── services/
│       │   ├── utils/
│       │   └── server.js
│       ├── tests/
│       ├── Dockerfile
│       ├── package.json
│       └── .env.example
│
├── infrastructure/
│   ├── terraform/                    # Terraform IaC
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   ├── providers.tf
│   │   ├── backend.tf
│   │   └── modules/
│   │       ├── aks/
│   │       ├── acr/
│   │       ├── keyvault/
│   │       ├── networking/
│   │       └── postgresql/
│   │
│   └── scripts/
│       ├── setup-azure.sh
│       ├── cleanup.sh
│       └── backup-db.sh
│
├── k8s/                              # Kubernetes manifests
│   ├── base/
│   │   ├── namespace.yaml
│   │   ├── configmap.yaml
│   │   ├── secrets.yaml
│   │   └── networkpolicy.yaml
│   ├── frontend/
│   │   ├── deployment-blue.yaml
│   │   ├── deployment-green.yaml
│   │   ├── service.yaml
│   │   ├── hpa.yaml
│   │   └── pdb.yaml
│   ├── backend/
│   │   ├── deployment-blue.yaml
│   │   ├── deployment-green.yaml
│   │   ├── service.yaml
│   │   ├── hpa.yaml
│   │   └── pdb.yaml
│   ├── database/
│   │   ├── statefulset.yaml
│   │   ├── service.yaml
│   │   ├── pvc.yaml
│   │   └── backup-cronjob.yaml
│   ├── ingress/
│   │   ├── ingress-staging.yaml
│   │   ├── ingress-production.yaml
│   │   └── certificate.yaml
│   └── monitoring/
│       ├── servicemonitor.yaml
│       └── prometheusrule.yaml
│
├── helm/                             # Helm charts
│   └── ecommerce-app/
│       ├── Chart.yaml
│       ├── values.yaml
│       ├── values-staging.yaml
│       ├── values-production.yaml
│       └── templates/
│           ├── deployment.yaml
│           ├── service.yaml
│           ├── ingress.yaml
│           └── _helpers.tpl
│
├── database/
│   └── migrations/                   # Flyway migrations
│       ├── V1.0__initial_schema.sql
│       ├── V1.1__add_products.sql
│       ├── V1.2__add_orders.sql
│       └── V1.3__add_indexes.sql
│
├── tests/
│   ├── unit/                         # Unit tests
│   │   ├── frontend/
│   │   └── backend/
│   ├── integration/                  # Integration tests
│   │   ├── api-tests.postman_collection.json
│   │   ├── staging.postman_environment.json
│   │   └── production.postman_environment.json
│   ├── e2e/                          # End-to-end tests
│   │   ├── playwright.config.ts
│   │   ├── tests/
│   │   │   ├── auth.spec.ts
│   │   │   ├── products.spec.ts
│   │   │   └── checkout.spec.ts
│   │   └── package.json
│   └── performance/                  # Performance tests
│       ├── baseline.js
│       ├── load-test.js
│       └── stress-test.js
│
├── opa-policies/                     # Open Policy Agent policies
│   ├── deny-privileged.rego
│   ├── require-resources.rego
│   ├── require-probes.rego
│   ├── approved-registries.rego
│   ├── require-labels.rego
│   ├── ingress-tls.rego
│   ├── readonly-filesystem.rego
│   └── drop-capabilities.rego
│
├── monitoring/
│   ├── dashboards/                   # Grafana dashboards
│   │   ├── application-metrics.json
│   │   ├── infrastructure.json
│   │   └── security.json
│   ├── alerts/                       # Alert rules
│   │   ├── application-alerts.yaml
│   │   ├── infrastructure-alerts.yaml
│   │   └── security-alerts.yaml
│   └── slo/                          # Service Level Objectives
│       └── slo-definitions.yaml
│
├── docs/                             # Documentation
│   ├── ARCHITECTURE.md
│   ├── SECURITY.md
│   ├── DEPLOYMENT.md
│   ├── MONITORING.md
│   ├── TROUBLESHOOTING.md
│   ├── RUNBOOKS.md
│   ├── API.md
│   └── images/
│       ├── architecture-diagram.png
│       ├── pipeline-flow.png
│       └── security-layers.png
│
├── scripts/                          # Utility scripts
│   ├── local-dev/
│   │   ├── start-dev.sh
│   │   ├── stop-dev.sh
│   │   └── reset-db.sh
│   ├── deployment/
│   │   ├── deploy-staging.sh
│   │   ├── deploy-production.sh
│   │   └── rollback.sh
│   └── maintenance/
│       ├── backup.sh
│       ├── restore.sh
│       └── cleanup-old-resources.sh
│
├── .github/                          # GitHub specific
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│       └── pr-validation.yml
│
├── .gitignore
├── .dockerignore
├── .editorconfig
├── .prettierrc
├── .eslintrc.json
├── sonar-project.properties          # SonarQube configuration
├── trivy.yaml                        # Trivy configuration
├── LICENSE
├── README.md                         # This file
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
└── CHANGELOG.md
```

---

## 📋 Prerequisites

### Required Tools

| Tool | Version | Purpose |
|------|---------|---------|
| Azure CLI | 2.50+ | Azure resource management |
| kubectl | 1.28+ | Kubernetes management |
| Terraform | 1.6+ | Infrastructure as Code |
| Docker | 24.0+ | Container building |
| Node.js | 18 LTS | Application runtime |
| Helm | 3.12+ | Kubernetes package manager |
| Git | 2.40+ | Version control |

### Azure Prerequisites

- **Azure Subscription** with Owner or Contributor role
- **Azure DevOps** organization and project
- **Sufficient Quotas**:
  - 20 vCPUs for AKS
  - 5 Public IP addresses
  - Premium storage account

### External Services

- **SonarQube** server (or SonarCloud)
- **Snyk** account and API token
- **Domain name** for application
- **SSL certificates** (or use Let's Encrypt)

---

## 🔧 Installation

### Step 1: Environment Setup

```bash
# Clone repository
git clone https://github.com/your-org/azure-devsecops-pipeline.git
cd azure-devsecops-pipeline

# Install dependencies
npm install -g @azure/cli
npm install -g kubectl
npm install -g terraform
npm install -g helm
```

### Step 2: Configure Azure

```bash
# Login to Azure
az login

# Set subscription
az account set --subscription "your-subscription-id"

# Register required providers
az provider register --namespace Microsoft.ContainerService
az provider register --namespace Microsoft.ContainerRegistry
az provider register --namespace Microsoft.KeyVault
az provider register --namespace Microsoft.OperationalInsights
```

### Step 3: Create Configuration Files

Create `.env` files from examples:

```bash
# Frontend
cp src/frontend/.env.example src/frontend/.env

# Backend
cp src/backend/.env.example src/backend/.env
```

### Step 4: Configure Secrets

Update Azure DevOps variable groups with required secrets:

**Variable Group: `ecommerce-prod-secrets`**

```yaml
Variables:
  - AZURE_CLIENT_ID: <service-principal-app-id>
  - AZURE_CLIENT_SECRET: <service-principal-password> # Secret
  - AZURE_TENANT_ID: <tenant-id>
  - AZURE_SUBSCRIPTION_ID: <subscription-id>
  - DB_PASSWORD: <strong-password> # Secret
  - JWT_SECRET: <random-secret-key> # Secret
  - APPINSIGHTS_KEY: <instrumentation-key> # Secret
  - ACR_USERNAME: <acr-username>
  - ACR_PASSWORD: <acr-password> # Secret
```

### Step 5: Deploy Infrastructure

```bash
cd infrastructure/terraform

# Initialize
terraform init

# Plan
terraform plan -out=tfplan

# Apply
terraform apply tfplan

# Save outputs
terraform output -json > ../../outputs.json
```

### Step 6: Configure Kubernetes

```bash
# Get AKS credentials
az aks get-credentials \
  --resource-group rg-ecommerce-prod \
  --name aks-ecommerce-prod

# Verify connection
kubectl cluster-info
kubectl get nodes

# Apply base configurations
kubectl apply -f k8s/base/
```

### Step 7: Set Up Pipeline

1. Go to Azure DevOps
2. Pipelines → New Pipeline
3. Select "Azure Repos Git"
4. Select your repository
5. Use existing Azure Pipelines YAML file
6. Path: `.azure-pipelines/azure-pipelines.yml`
7. Run pipeline

---

## 🔄 Pipeline Stages

### Overview

The pipeline consists of 11 stages that ensure security, quality, and reliability:

```
1. Code Quality & Security     →  8-10 min
2. Infrastructure Security      →  15-20 min
3. Build & Container Security   →  10-15 min
4. Database Migration           →  5-10 min
5. K8s Manifest Security        →  3-5 min
6. Staging Deployment           →  8-12 min
7. Integration & DAST Testing   →  15-20 min
8. Production Deployment        →  15-20 min
9. Post-Deployment Validation   →  5-8 min
10. Compliance & Reporting      →  10-15 min
11. Cleanup                     →  5-10 min
────────────────────────────────────────────
Total Duration: ~2.5 hours
```

### Detailed Stage Information

For detailed information about each stage, see [docs/PIPELINE_STAGES.md](docs/PIPELINE_STAGES.md)

---

## 🔒 Security

### Security Layers

This pipeline implements a **12-layer security approach**:

1. **Secret Scanning** (Gitleaks)
2. **Static Code Analysis** (SonarQube)
3. **SAST** (Snyk Code)
4. **IaC Security** (Checkov, tfsec)
5. **Container Scanning** (Trivy)
6. **Image Signing** (Cosign)
7. **K8s Security** (Kubesec)
8. **Policy Enforcement** (OPA/Conftest)
9. **Network Policies** (Calico)
10. **DAST** (OWASP ZAP)
11. **CIS Compliance** (kube-bench)
12. **SBOM** (Syft)

### Security Best Practices

✅ No secrets in code or config files  
✅ All containers run as non-root  
✅ Read-only root filesystems  
✅ Network policies for isolation  
✅ TLS/SSL encryption everywhere  
✅ Regular security scanning  
✅ Automated patching  
✅ Audit logging enabled  

For more details, see [docs/SECURITY.md](docs/SECURITY.md)

---

## 🚀 Deployment

### Deployment Strategies

#### Blue-Green Deployment (Production)

```bash
# Deploy to blue environment
kubectl apply -f k8s/backend/deployment-blue.yaml
kubectl apply -f k8s/frontend/deployment-blue.yaml

# Run smoke tests
./scripts/deployment/smoke-test.sh blue

# Switch traffic to blue
kubectl apply -f k8s/backend/service-blue.yaml
kubectl apply -f k8s/frontend/service-blue.yaml

# Monitor for 5 minutes
./scripts/deployment/monitor.sh

# Rollback if needed
./scripts/deployment/rollback.sh green
```

#### Rolling Update (Staging)

```bash
# Update image
kubectl set image deployment/backend \
  backend=acr.azurecr.io/backend:new-version \
  -n staging

# Watch rollout
kubectl rollout status deployment/backend -n staging
```

### Manual Deployment

If you need to deploy manually:

```bash
# Deploy to staging
./scripts/deployment/deploy-staging.sh

# Deploy to production (requires approval)
./scripts/deployment/deploy-production.sh
```

For more details, see [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)

---

## 📊 Monitoring

### Application Insights

Access your Application Insights dashboard:
```
https://portal.azure.com/#resource/subscriptions/{sub-id}/resourceGroups/rg-ecommerce-prod/providers/microsoft.insights/components/appi-ecommerce-prod
```

### Key Metrics

- **Availability**: Target 99.9%
- **Response Time**: P95 < 500ms
- **Error Rate**: < 0.1%
- **Request Rate**: Monitored in real-time

### Grafana Dashboards

Import dashboards from `monitoring/dashboards/`:
- Application Metrics
- Infrastructure Health
- Security Metrics

### Alerts

Configured alerts:
- High error rate (>100 errors/5min)
- Slow response time (>2s avg)
- Pod crashes (>3 restarts/10min)
- High CPU usage (>80%/15min)
- Database connection failures

For more details, see [docs/MONITORING.md](docs/MONITORING.md)

---

## 🐛 Troubleshooting

### Common Issues

#### Pipeline Fails at Security Scan
```bash
# View detailed scan results
az pipelines runs show --id <run-id> --open

# Fix issues and re-run
git add .
git commit -m "fix: security vulnerabilities"
git push
```

#### Pods Not Starting
```bash
# Check pod status
kubectl get pods -n production

# View logs
kubectl logs <pod-name> -n production

# Describe pod for events
kubectl describe pod <pod-name> -n production
```

#### Database Connection Issues
```bash
# Test database connectivity
kubectl run -it --rm debug \
  --image=postgres:14 \
  --restart=Never \
  -- psql -h postgres.production -U dbuser -d ecommerce
```

For more troubleshooting guides, see [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Standards

- Follow the existing code style
- Write meaningful commit messages
- Add tests for new features
- Update documentation
- Ensure all security scans pass

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Authors

- **DevOps Team** - *Initial work* - [Your Organization](https://github.com/your-org)

See also the list of [contributors](https://github.com/your-org/azure-devsecops-pipeline/contributors) who participated in this project.

---

## 🙏 Acknowledgments

- Azure DevOps team for excellent CI/CD platform
- Open source security tools community
- Kubernetes community
- All contributors and testers

---

## 📞 Support

### Getting Help

- **Documentation**: [docs/](docs/)
- **Issues**: [GitHub Issues](https://github.com/your-org/azure-devsecops-pipeline/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-org/azure-devsecops-pipeline/discussions)
- **Email**: devops@company.com

### Enterprise Support

For enterprise support and consulting:
- Email: enterprise@company.com
- Website: https://company.com/support

---

## 📚 Additional Resources

### Documentation
- [Architecture Documentation](docs/ARCHITECTURE.md)
- [Security Documentation](docs/SECURITY.md)
- [Deployment Guide](docs/DEPLOYMENT.md)
- [Monitoring Guide](docs/MONITORING.md)
- [API Documentation](docs/API.md)
- [Runbooks](docs/RUNBOOKS.md)

### External Links
- [Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/)
- [Azure DevOps Pipelines](https://docs.microsoft.com/azure/devops/pipelines/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

---

## 🗺️ Roadmap

### Q4 2024
- [ ] Multi-region deployment
- [ ] Advanced A/B testing
- [ ] Chaos engineering integration
- [ ] Cost optimization improvements

### Q1 2025
- [ ] GitOps with Flux/ArgoCD
- [ ] Service mesh (Istio)
- [ ] Advanced observability
- [ ] ML-based anomaly detection

---

## ⭐ Star History

If you find this project useful, please consider giving it a star!

[![Star History Chart](https://api.star-history.com/svg?repos=your-org/azure-devsecops-pipeline&type=Date)](https://star-history.com/#your-org/azure-devsecops-pipeline&Date)

---

**Made with ❤️ by the DevOps Team** | [Report Bug](https://github.com/your-org/azure-devsecops-pipeline/issues) | [Request Feature](https://github.com/your-org/azure-devsecops-pipeline/issues)
