Here’s the complete README.md for your IAC-EKS repository:

# IAC-EKS

![Terraform](https://img.shields.io/badge/Terraform-1.6.3-blue.svg) ![AWS](https://img.shields.io/badge/AWS-Verified-brightgreen.svg) ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-Enabled-blueviolet.svg)

**Infrastructure as Code (IaC) for Amazon Elastic Kubernetes Service (EKS)**

This repository provides Terraform configurations to deploy a scalable, secure, and production-ready EKS cluster on AWS. It includes networking, IAM roles, EKS control plane, and worker nodes for seamless containerized application deployment.

---

## 🚀 Features

- **VPC Setup**: Creates a VPC with public/private subnets across multiple Availability Zones.
- **EKS Cluster**: Provisions an EKS cluster with required IAM roles and security groups.
- **Node Groups**: Supports managed and self-managed worker node groups.
- **Fargate Profiles**: Optional serverless compute with AWS Fargate.
- **CI/CD Integration**: GitHub Actions workflows for automated deployment.
- **Security Best Practices**: Implements IAM roles, security groups, and AWS security features.

---

## 🛠️ Prerequisites

- **AWS Account**: With necessary permissions.
- **Terraform**: v1.6.3 or compatible.
- **AWS CLI**: Configured credentials.
- **kubectl**: For Kubernetes management.
- **GitHub Account**: For CI/CD integration.

---

## 📂 Repository Structure

```
IAC-EKS/
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── modules/
│       ├── vpc/
│       ├── eks/
│       ├── node_groups/
│       └── fargate_profiles/
├── .github/
│   └── workflows/
│       └── ci-cd.yaml
└── README.md
```

- `terraform/`: Terraform configurations and modules.
- `.github/`: GitHub Actions workflows for CI/CD.

---

## 🧭 Deployment Guide

### 1. Clone the Repository

```bash
git clone https://github.com/KIRANMORAB/IAC-EKS.git
cd IAC-EKS
```

### 2. Initialize Terraform

```bash
terraform init
```

### 3. Configure Variables

Edit `terraform/variables.tf` to set:

- AWS region
- EKS cluster name
- Node instance types
- VPC CIDR blocks

### 4. Plan the Deployment

```bash
terraform plan
```
Review the plan to confirm resources.

### 5. Apply the Configuration

```bash
terraform apply
```
Approve when prompted to provision AWS infrastructure.

### 6. Configure kubectl

```bash
aws eks --region <region> update-kubeconfig --name <cluster_name>
```
Replace `<region>` and `<cluster_name>` with your values.

---

## 🔄 CI/CD Pipeline

The workflow `.github/workflows/ci-cd.yaml` automates:

- **Build**: Packages code.
- **Test**: Runs tests.
- **Deploy**: Deploys to EKS.

To use CI/CD:

- Keep application code in a separate repo.
- Set GitHub Secrets for AWS credentials and variables.
- Push changes to trigger the pipeline.

---

## 🔐 Security Considerations

- **IAM Roles**: Grant minimum permissions.
- **Security Groups**: Restrict resource access.
- **Secrets Management**: Use AWS Secrets Manager or SSM Parameter Store.

---

## ⚖️ Scaling: kOps vs EKS

**kOps**

- Scale nodes by editing instance groups:
    ```bash
    kops edit ig nodes
    kops update cluster --yes
    kops rolling-update cluster --yes
    ```
- Masters are EC2 instances you manage.
- Autoscaling requires Cluster Autoscaler.

**EKS**

- Scale managed node groups:
    ```bash
    aws eks update-nodegroup-config --cluster-name my-eks-cluster --nodegroup-name my-node-group --scaling-config minSize=2,maxSize=5,desiredSize=4
    ```
- Masters are managed by AWS.
- Autoscaling via Cluster Autoscaler.

---

## 📄 License

MIT License - see the LICENSE file.

