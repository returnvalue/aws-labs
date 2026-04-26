# AWS Cloud Architecture & DevOps Master Labs (LocalStack Pro)

![AWS](https://img.shields.io/badge/AWS-Master_Labs-FF9900?style=for-the-badge&logo=amazonaws)
![LocalStack](https://img.shields.io/badge/LocalStack-Pro-000000?style=for-the-badge)

Welcome to the comprehensive collection of AWS hands-on labs. This master repository serves as a central index for advanced cloud architecture, security, and DevOps workflows simulated entirely on [LocalStack Pro](https://localstack.cloud/).

## 🗺️ Table of Contents
* [AWS Identity and Access Management (IAM) Labs (LocalStack Pro)](#aws-identity-and-access-management-iam-labs-localstack-pro)
* [AWS Advanced VPC Architecture Labs (LocalStack Pro)](#aws-advanced-vpc-architecture-labs-localstack-pro)
* [AWS Elastic Compute Cloud (EC2) Labs (LocalStack Pro)](#aws-elastic-compute-cloud-ec2-labs-localstack-pro)
* [AWS Simple Storage Service (S3) Labs (LocalStack Pro)](#aws-simple-storage-service-s3-labs-localstack-pro)
* [AWS Relational Database Service (RDS) Labs (LocalStack Pro)](#aws-relational-database-service-rds-labs-localstack-pro)
* [AWS Lambda Serverless Labs (LocalStack Pro)](#aws-lambda-serverless-labs-localstack-pro)
* [AWS CloudWatch Monitoring Labs (LocalStack Pro)](#aws-cloudwatch-monitoring-labs-localstack-pro)
* [AWS Elastic Container Service (ECS) Labs (LocalStack Pro)](#aws-elastic-container-service-ecs-labs-localstack-pro)
* [AWS Elastic Kubernetes Service (EKS) Labs (LocalStack Pro)](#aws-elastic-kubernetes-service-eks-labs-localstack-pro)
* [AWS API Gateway Serverless Labs (LocalStack Pro)](#aws-api-gateway-serverless-labs-localstack-pro)
* [AWS CI/CD Pipeline Labs (LocalStack Pro)](#aws-cicd-pipeline-labs-localstack-pro)
* [AWS Infrastructure as Code (Terraform) Labs (LocalStack Pro)](#aws-infrastructure-as-code-terraform-labs-localstack-pro)

---

# AWS Identity and Access Management (IAM) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating advanced AWS Identity and Access Management (IAM) security concepts. Using [LocalStack Pro](https://localstack.cloud/), we simulate a localized AWS cloud environment to practice identity federation, policy evaluation logic, conditional access, and cross-account role assumption without risking real-world cloud environments.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS security best practices (SAA-C03), these labs demonstrate:
* **IAM Fundamentals:** Creating Users, Groups, and attaching Identity-Based Managed Policies.
* **Service Roles & Trust Policies:** Instead of embedding access keys, we use IAM Roles (Trust Policies + Permissions Policies) to securely grant compute services (like Lambda or EC2) access to other AWS resources.
* **Policy Evaluation Logic:** Proving that an `Explicit Deny` always overrides an `Allow`.
* **Policy Conditions:** Restricting the exact types of EC2 instances a user can provision using the `Condition` block (e.g., `ec2:InstanceType`).
* **Permissions Boundaries:** Defining the absolute maximum permissions an IAM entity can have, mitigating the risk of privilege escalation.
* **Cross-Account Access & STS:** Generating temporary security credentials using `AssumeRole` while preventing the "Confused Deputy" problem via the `ExternalId` condition.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/awslabs/iam.git
   cd iam
   ```

2. Configure your LocalStack Auth Token:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

3. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative, end-to-end scenario rather than isolated tasks. You are building one evolving architecture as you progress.
>
> **Session Persistence:** You must run all commands sequentially within the **same terminal session**. The labs rely on bash variables (like `$USER_NAME`, `$ROLE_ARN`, etc.) created in earlier steps. If you close your terminal, these variables will be lost and subsequent labs will fail.

## 📚 Labs Index
1. [Lab 1: IAM Fundamentals (Users, Groups, & Policies)](https://github.com/returnvalue/aws-iam/blob/main/labs/lab1-iam-fundamentals/README.md)
2. [Lab 2: Service Roles & Trust Policies](https://github.com/returnvalue/aws-iam/blob/main/labs/lab2-service-roles-trust-policies/README.md)
3. [Lab 3: Policy Evaluation Logic (Explicit Deny)](https://github.com/returnvalue/aws-iam/blob/main/labs/lab3-policy-evaluation-logic/README.md)
4. [Lab 4: Policy Conditions (Attribute-Based Access Control)](https://github.com/returnvalue/aws-iam/blob/main/labs/lab4-policy-conditions/README.md)
5. [Lab 5: Permissions Boundaries](https://github.com/returnvalue/aws-iam/blob/main/labs/lab5-permissions-boundaries/README.md)
6. [Lab 6: Cross-Account Access & STS AssumeRole](https://github.com/returnvalue/aws-iam/blob/main/labs/lab6-cross-account-sts/README.md)


---

# AWS Advanced VPC Architecture Labs (LocalStack Pro)


This repository contains a comprehensive set of hands-on labs demonstrating advanced Amazon Virtual Private Cloud (VPC) concepts. It bridges the gap between AWS theoretical knowledge (SAA-C03) and practical implementation using [LocalStack Pro](https://localstack.cloud/) to simulate a complete AWS cloud environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS documentation and best practices, these labs walk through the deployment of:
* **Foundational Networking:** Amazon VPC provides an isolated network environment. You have complete control over networking, including IP ranges, subnets, route tables, and gateways. A /24 subnet provides 256 total IP addresses, but AWS reserves 5 IP addresses, leaving 251 available.
* **Routing & Internet Access:** Internet Gateways provide access to the internet, while a NAT Gateway enables outbound internet access for private subnets. Instances in the private subnet remain private with no inbound access from the internet. 
* **Private Connectivity:** VPC Endpoints provide private connectivity to AWS services like S3 and DynamoDB without traversing the internet. 
* **Layered Security:** Security Groups are stateful, meaning if inbound is allowed, return traffic is automatically allowed. Network ACLs are stateless, support Deny rules, and evaluate traffic at the subnet level. Network ACLs do not support rate limiting.
* **Multi-VPC Topologies:** VPC Peering connects two VPCs privately but is not transitive. AWS Transit Gateway acts as a central hub for VPCs and is highly scalable. 
* **Shared Services:** AWS PrivateLink provides private connectivity to services exposed via VPC Endpoint Services without requiring VPC peering or an Internet Gateway.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/awslabs/vpc.git
   cd vpc
   ```

2. Configure your LocalStack Auth Token:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

3. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative, end-to-end scenario rather than isolated tasks. You are building one evolving architecture as you progress.
>
> **Session Persistence:** You must run all commands sequentially within the **same terminal session**. The labs rely on bash variables (like `$VPC_ID`, `$PRIV_RT`, etc.) created in earlier steps. If you close your terminal, these variables will be lost and subsequent labs will fail.

## 📚 Labs Index
1. [Lab 1: Foundational VPC & Subnet Isolation](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab1-vpc-subnets/README.md)
2. [Lab 2: Internet & NAT Gateways](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab2-internet-nat-gateways/README.md)
3. [Lab 3: Secure AWS Access via VPC Endpoints](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab3-vpc-endpoints/README.md)
4. [Lab 4: Defense in Depth (Security Groups vs. NACLs)](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab4-security-groups-nacls/README.md)
5. [Lab 5: 1-to-1 Multi-VPC Architecture (VPC Peering)](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab5-vpc-peering/README.md)
6. [Lab 6: Hub-and-Spoke Topology (AWS Transit Gateway)](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab6-transit-gateway/README.md)
7. [Lab 7: Unidirectional Service Sharing (AWS PrivateLink)](https://github.com/returnvalue/aws-vpc/blob/main/labs/lab7-privatelink/README.md)


---

# AWS Elastic Compute Cloud (EC2) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon EC2 concepts, from foundational networking and instance provisioning to high availability and automated scaling. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS compute environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Network Foundation:** Provisioning custom VPCs, public/private subnets, and internet gateways.
* **EC2 Provisioning:** Launching On-Demand instances with optimized AMI selection.
* **Security & Access:** Implementing stateful Security Groups and instance-level bootstrapping via User Data.
* **High Availability:** Designing for fault tolerance using Multi-AZ deployments.
* **Scaling & Load Balancing:** Exploring Launch Templates, Auto Scaling Groups, and Elastic Load Balancers.
* **Cost Optimization:** Leveraging Spot Instances and Savings Plans logic.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$VPC_ID`, `$SG_ID`, `$AMI_ID`, etc.). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Network Foundation & EC2 Provisioning](https://github.com/returnvalue/aws-ec2/blob/main/labs/lab1-network-foundation-ec2/README.md)
2. [Lab 2: Layer 7 Application Load Balancer (ALB)](https://github.com/returnvalue/aws-ec2/blob/main/labs/lab2-application-load-balancer/README.md)
3. [Lab 3: EC2 Auto Scaling (Launch Templates & ASG)](https://github.com/returnvalue/aws-ec2/blob/main/labs/lab3-auto-scaling-groups/README.md)
4. [Lab 4: Auto Scaling Policies (Target Tracking)](https://github.com/returnvalue/aws-ec2/blob/main/labs/lab4-auto-scaling-policies/README.md)
5. [Lab 5: Cost Optimization (Spot Instances)](https://github.com/returnvalue/aws-ec2/blob/main/labs/lab5-cost-optimization-spot/README.md)


---

# AWS Simple Storage Service (S3) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon S3 concepts, from foundational storage and data protection to advanced security and lifecycle management. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS storage environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Data Protection:** Implementing Versioning to protect against accidental deletes and overwrites.
* **Security & Access Control:** Securing access via Pre-signed URLs for third parties.
* **Lifecycle Management:** Automating data transitions and expiration.
* **Event-Driven Architectures:** Decoupling systems with S3 Event Notifications and SQS.
* **Server-Side Encryption:** Securing data at rest with SSE-S3 and SSE-KMS.
* **Compliance:** Enforcing WORM models with S3 Object Lock.
* **Content Delivery:** Global distribution with Amazon CloudFront.
* **Disaster Recovery:** Cross-Region Replication for mission-critical data.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving storage infrastructure.

## 📚 Labs Index
1. [Lab 1: Foundational S3 & Data Protection (Versioning)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab1-s3-versioning/README.md)
2. [Lab 2: Compliance & Security (SSE-KMS & Object Lock)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab2-s3-compliance-kms/README.md)
3. [Lab 3: Automated Cost Optimization (Lifecycle Policies)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab3-s3-lifecycle-policies/README.md)
4. [Lab 4: Event-Driven Architectures (S3 Event Notifications to SQS)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab4-s3-event-notifications/README.md)
5. [Lab 5: Secure Third-Party Access (Pre-signed URLs)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab5-s3-presigned-urls/README.md)
6. [Lab 6: Content Delivery & Edge Caching (CloudFront Origin)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab6-s3-cloudfront/README.md)
7. [Lab 7: Disaster Recovery (Cross-Region Replication)](https://github.com/returnvalue/aws-s3/blob/main/labs/lab7-s3-replication/README.md)


---

# AWS Relational Database Service (RDS) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon RDS concepts, from foundational networking and instance provisioning to high availability and data security. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS database environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Networking Foundation:** Designing DB Subnet Groups for multi-AZ reliability.
* **RDS Provisioning:** Launching managed relational databases (PostgreSQL).
* **High Availability:** Implementing Multi-AZ deployments for failover.
* **Serverless Databases:** Deploying Amazon Aurora Serverless for unpredictable workloads.
* **Connection Pooling:** Implementing RDS Proxy for serverless scalability and resiliency.
* **Security & Encryption:** Securing data at rest with SSE-KMS and IAM Database Auth.
* **Disaster Recovery:** Managing snapshots and automated backups.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving database infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$VPC_ID`, `$SUBNET_A`, etc.). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Networking Foundation & Base RDS Deployment](https://github.com/returnvalue/aws-rds/blob/main/labs/lab1-rds-networking-foundation/README.md)
2. [Lab 2: High Availability (Multi-AZ Conversion)](https://github.com/returnvalue/aws-rds/blob/main/labs/lab2-rds-high-availability/README.md)
3. [Lab 3: Backup & Retention Policies](https://github.com/returnvalue/aws-rds/blob/main/labs/lab3-rds-backup-retention/README.md)
4. [Lab 4: Advanced Security (Encryption & IAM Auth)](https://github.com/returnvalue/aws-rds/blob/main/labs/lab4-rds-security-encryption/README.md)
5. [Lab 5: Serverless Workloads (Aurora Serverless)](https://github.com/returnvalue/aws-rds/blob/main/labs/lab5-rds-aurora-serverless/README.md)
6. [Lab 6: Serverless Connection Pooling (RDS Proxy)](https://github.com/returnvalue/aws-rds/blob/main/labs/lab6-rds-proxy/README.md)


---

# AWS Lambda Serverless Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon Lambda concepts, from foundational function provisioning to advanced event-driven architectures and triggers. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS serverless environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Function Provisioning:** Deploying serverless compute with specific runtimes and execution roles.
* **Synchronous Web Access:** Exposing functions via built-in Lambda Function URLs.
* **Asynchronous Polling:** Decoupling systems with SQS Event Source Mappings.
* **Safe Deployments:** Implementing function Versions and Aliases for lifecycle management.
* **Code Reusability:** Leveraging Lambda Layers for shared libraries and logic.
* **Scalability & Resiliency:** Using Reserved Concurrency to guarantee compute availability.
* **IAM Execution Roles:** Implementing the principle of least privilege for Lambda functions.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving serverless infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$ROLE_ARN`, `$QUEUE_URL`, `$LAYER_ARN`, `$VERSION`). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Foundational Lambda Provisioning](https://github.com/returnvalue/aws-lambda/blob/main/labs/lab1-lambda-provisioning/README.md)
2. [Lab 2: Synchronous Web Access (Function URLs)](https://github.com/returnvalue/aws-lambda/blob/main/labs/lab2-lambda-function-urls/README.md)
3. [Lab 3: Asynchronous Polling (SQS Event Source Mapping)](https://github.com/returnvalue/aws-lambda/blob/main/labs/lab3-lambda-sqs-trigger/README.md)
4. [Lab 4: Code Reusability (Lambda Layers)](https://github.com/returnvalue/aws-lambda/blob/main/labs/lab4-lambda-layers/README.md)
5. [Lab 5: Safe Deployments (Versions, Aliases & Concurrency)](https://github.com/returnvalue/aws-lambda/blob/main/labs/lab5-lambda-deployments/README.md)


---

# AWS CloudWatch Monitoring Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon CloudWatch concepts, from log management and metric filtering to automated alarms and dashboards. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS monitoring environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Log Management:** Creating log groups and streams to centralize application logs.
* **Metric Filters:** Automatically extracting numerical data from text logs for monitoring.
* **CloudWatch Alarms:** Setting thresholds to trigger notifications or automated actions via SNS.
* **Custom Metrics:** Publishing application-specific data points for monitoring.
* **API Auditing:** Implementing CloudTrail to track account activity for security and compliance.
* **Continuous Compliance:** Using AWS Config to automate resource evaluation and reporting.
* **Secure Operations:** Managing secrets and configuration with SSM Parameter Store.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving monitoring infrastructure.

## 📚 Labs Index
1. [Lab 1: CloudWatch Logs & Metric Filters](https://github.com/returnvalue/aws-cloudwatch/blob/main/labs/lab1-cloudwatch-logs/README.md)
2. [Lab 2: Automated Alerting (CloudWatch Alarms & SNS)](https://github.com/returnvalue/aws-cloudwatch/blob/main/labs/lab2-cloudwatch-alarms/README.md)
3. [Lab 3: API Auditing with AWS CloudTrail](https://github.com/returnvalue/aws-cloudwatch/blob/main/labs/lab3-cloudwatch-audit/README.md)
4. [Lab 4: Continuous Compliance (AWS Config)](https://github.com/returnvalue/aws-cloudwatch/blob/main/labs/lab4-cloudwatch-config/README.md)
5. [Lab 5: Secure Operations (Systems Manager Parameter Store)](https://github.com/returnvalue/aws-cloudwatch/blob/main/labs/lab5-cloudwatch-ssm/README.md)


---

# AWS Elastic Container Service (ECS) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon ECS concepts, from foundational networking and image management to task definitions, services, and high availability. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS container orchestration environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Networking Foundation:** Designing multi-AZ VPCs for container reliability.
* **IAM Security:** Implementing strict separation between Execution and Task roles.
* **Cluster Management:** Provisioning serverless ECS Fargate clusters.
* **Task Definitions:** Defining blueprints using the `awsvpc` network mode.
* **Batch & One-off Jobs:** Running standalone Fargate tasks for migrations and processing.
* **Image Management:** Using Amazon ECR to securely store and version Docker images.
* **Load Balancing:** Distributing traffic to containers via ALB with IP-based targets.
* **Service Orchestration:** Deploying long-running ECS Services with self-healing and ALB integration.
* **Service Auto Scaling:** Implementing dynamic target-tracking scaling based on demand.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving containerized infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$VPC_ID`, `$TASK_SG`, `$TASK_DEF_ARN`, `$TG_ARN`, etc.). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Networking Foundation & ECR Registry](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab1-ecs-foundation/README.md)
2. [Lab 2: IAM Role Separation (Execution vs. Task Roles)](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab2-ecs-iam-roles/README.md)
3. [Lab 3: ECS Cluster & Task Definitions (awsvpc mode)](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab3-ecs-task-definitions/README.md)
4. [Lab 4: Running Standalone Tasks (Fargate)](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab4-ecs-standalone-tasks/README.md)
5. [Lab 5: Application Load Balancer Integration (IP Targets)](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab5-ecs-alb-integration/README.md)
6. [Lab 6: ECS Long-Running Services](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab6-ecs-services/README.md)
7. [Lab 7: Service Auto Scaling (Target Tracking)](https://github.com/returnvalue/aws-ecs/blob/main/labs/lab7-ecs-auto-scaling/README.md)


---

# AWS Elastic Kubernetes Service (EKS) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon EKS concepts, from foundational cluster provisioning and networking to node group management, deployments, and security. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS Kubernetes environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Control Plane Management:** Provisioning managed EKS clusters with IAM service roles.
* **Networking Foundation:** Designing multi-AZ VPCs required for Kubernetes reliability.
* **Worker Nodes:** Deploying and scaling EC2 Managed Node Groups.
* **Serverless Kubernetes:** Using Fargate Profiles to run pods without managing nodes.
* **EKS Security:** Implementing IRSA (IAM Roles for Service Accounts) and modern Access Entries.
* **Cluster Add-ons:** Managing operational software like VPC CNI natively via the EKS API.
* **Cluster Connectivity:** Configuring `kubectl` to manage resources via `update-kubeconfig`.
* **Kubernetes Orchestration:** (Upcoming) Deploying applications using Helm and kubectl.
* **Observability:** (Upcoming) Monitoring clusters with CloudWatch container insights.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)
* [`kubectl`](https://kubernetes.io/docs/tasks/tools/) (optional, for interacting with the cluster)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving Kubernetes infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$VPC_ID`, `$CLUSTER_ROLE_ARN`, `$OIDC_URL`, etc.). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Network Foundation & Control Plane](https://github.com/returnvalue/aws-eks/blob/main/labs/lab1-eks-foundation/README.md)
2. [Lab 2: Data Plane (Managed Node Groups)](https://github.com/returnvalue/aws-eks/blob/main/labs/lab2-eks-nodegroups/README.md)
3. [Lab 3: Serverless Data Plane (Fargate Profiles)](https://github.com/returnvalue/aws-eks/blob/main/labs/lab3-eks-fargate-profiles/README.md)
4. [Lab 4: Security Identity (OIDC & IRSA)](https://github.com/returnvalue/aws-eks/blob/main/labs/lab4-eks-irsa/README.md)
5. [Lab 5: Cluster Add-ons Management (VPC CNI)](https://github.com/returnvalue/aws-eks/blob/main/labs/lab5-eks-addons/README.md)
6. [Lab 6: Modern Access Management (Access Entries)](https://github.com/returnvalue/aws-eks/blob/main/labs/lab6-eks-access-management/README.md)
7. [Lab 7: Connecting to the Cluster (kubeconfig)](https://github.com/returnvalue/aws-eks/blob/main/labs/lab7-eks-kubeconfig/README.md)


---

# AWS API Gateway Serverless Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Amazon API Gateway concepts, from RESTful API design and Lambda integrations to asynchronous patterns, security, and deployment stages. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS API management environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Synchronous REST APIs:** Connecting HTTP endpoints to Lambda functions via Proxy Integrations.
* **Asynchronous Processing:** Implementing the Storage-First pattern using direct SQS integrations.
* **Fan-Out Webhooks:** Integrating directly with SNS to broadcast messages to multiple subscribers.
* **Event Routing:** Directly ingesting webhooks onto an EventBridge Custom Bus.
* **Request Validation:** Enforcing parameter and schema validation at the edge to reduce backend load.
* **Deployment Management:** Managing immutable snapshots and Stages (dev/prod) for CI/CD.
* **API Security:** Implementing API Keys and Usage Plans for throttling and monetization.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving API infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$API_ID`, `$LAMBDA_ARN`, `$VALIDATOR_ID`, `$PLAN_ID`, etc.). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Foundational API & Synchronous Lambda](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab1-api-lambda-sync/README.md)
2. [Lab 2: Storage-First Pattern (Direct SQS Integration)](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab2-api-sqs-async/README.md)
3. [Lab 3: Fan-Out Webhooks (Direct SNS Integration)](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab3-api-sns-fanout/README.md)
4. [Lab 4: Event Routing (Direct EventBridge Integration)](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab4-api-eventbridge/README.md)
5. [Lab 5: Payload Edge Validation](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab5-api-validation/README.md)
6. [Lab 6: API Deployments & Stages](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab6-api-deployments/README.md)
7. [Lab 7: Monetization & Security (API Keys & Throttling)](https://github.com/returnvalue/aws-apigateway/blob/main/labs/lab7-api-keys-throttling/README.md)


---

# AWS CI/CD Pipeline Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core AWS DevOps concepts, from source control and automated builds to continuous deployment and orchestration. Using [LocalStack Pro](https://localstack.cloud/), we simulate a complete AWS CI/CD environment locally.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Source Control:** Managing private Git repositories with Amazon CodeCommit.
* **Pipeline Infrastructure:** Provisioning S3 artifact storage and IAM service roles.
* **Continuous Integration:** Automating builds and tests with AWS CodeBuild.
* **Deployment Targets:** Provisioning and tagging EC2 instances for automated deployments.
* **Continuous Deployment:** Automating application updates with AWS CodeDeploy.
* **Pipeline Orchestration:** Linking stages together with AWS CodePipeline for full automation.
* **Monitoring & Execution:** Triggering and tracking real-time pipeline status.
* **Infrastructure as Code:** (Upcoming) Automating resource provisioning within the pipeline.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [`awslocal` CLI](https://github.com/localstack/awscli-local) (a wrapper around the AWS CLI for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving CI/CD infrastructure.
>
> **Session Persistence:** These labs rely on bash variables (like `$BUILD_ROLE`, `$PIPELINE_ROLE`, `$DEPLOY_ROLE`, etc.). Run all commands in the same terminal session to maintain context.

## 📚 Labs Index
1. [Lab 1: Source Control (AWS CodeCommit)](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab1-codecommit-repo/README.md)
2. [Lab 2: Artifact Storage & IAM Foundations](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab2-artifacts-iam/README.md)
3. [Lab 3: Continuous Integration (AWS CodeBuild)](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab3-codebuild-project/README.md)
4. [Lab 4: Provisioning Deployment Targets (EC2)](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab4-ec2-deployment-target/README.md)
5. [Lab 5: Continuous Deployment (AWS CodeDeploy)](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab5-codedeploy-setup/README.md)
6. [Lab 6: Pipeline Orchestration (AWS CodePipeline)](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab6-codepipeline-orchestration/README.md)
7. [Lab 7: Pipeline Execution & Monitoring](https://github.com/returnvalue/aws-cicd/blob/main/labs/lab7-pipeline-monitoring/README.md)


---

# AWS Infrastructure as Code (Terraform) Labs (LocalStack Pro)


This repository contains hands-on labs demonstrating core Infrastructure as Code (IaC) concepts using HashiCorp Terraform. Using [LocalStack Pro](https://localstack.cloud/) and the `tflocal` wrapper, we simulate a complete AWS environment to practice declarative resource provisioning, state management, and modular design.

## 🎯 Architecture Goals & Use Cases Covered
Based on AWS best practices (SAA-C03), these labs cover:
* **Declarative Provisioning:** Defining infrastructure as code to ensure consistency and repeatability.
* **Dynamic Lookups:** Using Data Sources to fetch AMIs and other external information.
* **Variables & Outputs:** Making configurations dynamic, reusable, and extractable.
* **Security as Code:** Managing IAM roles and policies via version-controlled HCL.
* **Compute Management:** Provisioning and modifying EC2 instances via code.
* **Advanced Networking:** Deploying Application Load Balancers and Target Groups.
* **Modular Design:** Organizing resources into reusable, standardized modules.
* **Networking Foundation:** Designing VPCs and Subnets via code.
* **State Management:** Implementing remote state storage and locking via S3 and DynamoDB.

## ⚙️ Prerequisites

* [Docker](https://docs.docker.com/get-docker/) & Docker Compose
* [LocalStack Pro](https://app.localstack.cloud/) account and Auth Token
* [Terraform](https://developer.hashicorp.com/terraform/downloads) installed locally
* [`tflocal` CLI](https://github.com/localstack/terraform-local) (a wrapper around Terraform for LocalStack)

## 🚀 Environment Setup

1. Configure your LocalStack Auth Token in `.env`:
   ```bash
   echo "YOUR_TOKEN=your_auth_token_here" > .env
   ```

2. Start LocalStack Pro:
   ```bash
   docker-compose up -d
   ```

> [!IMPORTANT]
> **Cumulative Architecture:** These labs are designed as a cumulative scenario. You are building an evolving infrastructure stack.

## 📚 Labs Index
1. [Lab 1: Provider Setup & Foundational Networking](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab1-terraform-foundation/README.md)
2. [Lab 2: Dynamic Data Sources & Compute](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab2-terraform-compute/README.md)
3. [Lab 3: Variables, Tfvars, and Outputs](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab3-terraform-variables/README.md)
4. [Lab 4: IAM & Security as Code](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab4-terraform-iam/README.md)
5. [Lab 5: Advanced Networking (Load Balancers)](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab5-terraform-alb/README.md)
6. [Lab 6: Modularity & Advanced State Routing (Native Terraform)](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab6-terraform-modularity/README.md)
7. [Lab 7: Remote State Architecture](https://github.com/returnvalue/aws-terraform/blob/main/labs/lab7-terraform-state/README.md)


---


---

💡 **Pro Tip: Using `aws` instead of `awslocal`**

If you prefer using the standard `aws` CLI without the `awslocal` wrapper or repeating the `--endpoint-url` flag, you can configure a dedicated profile in your AWS config files.

### 1. Configure your Profile
Add the following to your `~/.aws/config` file:
```ini
[profile localstack]
region = us-east-1
output = json
# This line redirects all commands for this profile to LocalStack
endpoint_url = http://localhost:4566
```

Add matching dummy credentials to your `~/.aws/credentials` file:
```ini
[localstack]
aws_access_key_id = test
aws_secret_access_key = test
```

### 2. Use it in your Terminal
You can now run commands in two ways:

**Option A: Pass the profile flag**
```bash
aws iam create-user --user-name DevUser --profile localstack
```

**Option B: Set an environment variable (Recommended)**
Set your profile once in your session, and all subsequent `aws` commands will automatically target LocalStack:
```bash
export AWS_PROFILE=localstack
aws iam create-user --user-name DevUser
```

### Why this works
- **Precedence**: The AWS CLI (v2) supports a global `endpoint_url` setting within a profile. When this is set, the CLI automatically redirects all API calls for that profile to your local container instead of the real AWS cloud.
- **Convenience**: This allows you to use the standard documentation commands exactly as written, which is helpful if you are copy-pasting examples from AWS labs or tutorials.
