# AWS EKS Infrastructure

Terraform configuration to provision the AWS infrastructure for my [Kubernetes microservices project](https://github.com/adityasingh307/three-tier-devops-project).

## Architecture

- Custom VPC across 3 Availability Zones
- 3 public and 3 private subnets
- Internet Gateway and NAT Gateways
- Amazon EKS cluster
- Managed node group using EC2 `t3.medium` instances
- S3 remote state with DynamoDB locking

## Prerequisites

- AWS CLI configured with appropriate permissions
- Terraform
- kubectl

## Deployment

**1. Create the remote backend** (first time only):

```bash
cd backend
terraform init
terraform plan
terraform apply
```

**2. Deploy the infrastructure:**

```bash
cd ..
terraform init
terraform fmt -recursive
terraform validate
terraform plan
terraform apply
```

**3. Configure kubectl:**

```bash
aws eks update-kubeconfig \
  --region us-west-2 \
  --name my-eks-cluster
```

## Cleanup

Destroy the EKS infrastructure when it is no longer needed:

```bash
terraform destroy
```

The backend resources are managed separately and are not removed by this command.

**Note:** AWS resources such as NAT Gateways, EKS and EC2 instances incur charges. Destroy unused infrastructure to avoid unnecessary costs.
