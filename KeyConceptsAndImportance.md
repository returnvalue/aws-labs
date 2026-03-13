# Key Concepts & Importance

IAM
* **IAM Fundamentals:** Creating Users, Groups, and attaching Identity-Based Managed Policies.
* **Service Roles & Trust Policies:** Instead of embedding access keys, we use IAM Roles (Trust Policies + Permissions Policies) to securely grant compute services (like Lambda or EC2) access to other AWS resources.
* **Policy Evaluation Logic:** Proving that an `Explicit Deny` always overrides an `Allow`.
* **Policy Conditions:** Restricting the exact types of EC2 instances a user can provision using the `Condition` block (e.g., `ec2:InstanceType`).
* **Permissions Boundaries:** Defining the absolute maximum permissions an IAM entity can have, mitigating the risk of privilege escalation.
* **Cross-Account Access & STS:** Generating temporary security credentials using `AssumeRole` while preventing the "Confused Deputy" problem via the `ExternalId` condition.

---

VPC
* **Foundational Networking:** Amazon VPC provides an isolated network environment. You have complete control over networking, including IP ranges, subnets, route tables, and gateways. A /24 subnet provides 256 total IP addresses, but AWS reserves 5 IP addresses, leaving 251 available.
* **Routing & Internet Access:** Internet Gateways provide access to the internet, while a NAT Gateway enables outbound internet access for private subnets. Instances in the private subnet remain private with no inbound access from the internet. 
* **Private Connectivity:** VPC Endpoints provide private connectivity to AWS services like S3 and DynamoDB without traversing the internet. 
* **Layered Security:** Security Groups are stateful, meaning if inbound is allowed, return traffic is automatically allowed. Network ACLs are stateless, support Deny rules, and evaluate traffic at the subnet level. Network ACLs do not support rate limiting.
* **Multi-VPC Topologies:** VPC Peering connects two VPCs privately but is not transitive. AWS Transit Gateway acts as a central hub for VPCs and is highly scalable. 
* **Shared Services:** AWS PrivateLink provides private connectivity to services exposed via VPC Endpoint Services without requiring VPC peering or an Internet Gateway.

---

EC2
* **Network Foundation:** Provisioning custom VPCs, public/private subnets, and internet gateways.
* **EC2 Provisioning:** Launching On-Demand instances with optimized AMI selection.
* **Security & Access:** Implementing stateful Security Groups and instance-level bootstrapping via User Data.
* **High Availability:** Designing for fault tolerance using Multi-AZ deployments.
* **Scaling & Load Balancing:** Exploring Launch Templates, Auto Scaling Groups, and Elastic Load Balancers.
* **Cost Optimization:** Leveraging Spot Instances and Savings Plans logic.

---

S3
* **Data Protection:** Implementing Versioning to protect against accidental deletes and overwrites.
* **Security & Access Control:** Securing access via Pre-signed URLs for third parties.
* **Lifecycle Management:** Automating data transitions and expiration.
* **Event-Driven Architectures:** Decoupling systems with S3 Event Notifications and SQS.
* **Server-Side Encryption:** Securing data at rest with SSE-S3 and SSE-KMS.
* **Compliance:** Enforcing WORM models with S3 Object Lock.
* **Content Delivery:** Global distribution with Amazon CloudFront.
* **Disaster Recovery:** Cross-Region Replication for mission-critical data.

---

RDS
* **Networking Foundation:** Designing DB Subnet Groups for multi-AZ reliability.
* **RDS Provisioning:** Launching managed relational databases (PostgreSQL).
* **High Availability:** Implementing Multi-AZ deployments for failover.
* **Serverless Databases:** Deploying Amazon Aurora Serverless for unpredictable workloads.
* **Connection Pooling:** Implementing RDS Proxy for serverless scalability and resiliency.
* **Security & Encryption:** Securing data at rest with SSE-KMS and IAM Database Auth.
* **Disaster Recovery:** Managing snapshots and automated backups.

---

LAMBDA
* **Function Provisioning:** Deploying serverless compute with specific runtimes and execution roles.
* **Synchronous Web Access:** Exposing functions via built-in Lambda Function URLs.
* **Asynchronous Polling:** Decoupling systems with SQS Event Source Mappings.
* **Safe Deployments:** Implementing function Versions and Aliases for lifecycle management.
* **Code Reusability:** Leveraging Lambda Layers for shared libraries and logic.
* **Scalability & Resiliency:** Using Reserved Concurrency to guarantee compute availability.
* **IAM Execution Roles:** Implementing the principle of least privilege for Lambda functions.

---

CLOUDWATCH
* **Log Management:** Creating log groups and streams to centralize application logs.
* **Metric Filters:** Automatically extracting numerical data from text logs for monitoring.
* **CloudWatch Alarms:** Setting thresholds to trigger notifications or automated actions via SNS.
* **Custom Metrics:** Publishing application-specific data points for monitoring.
* **API Auditing:** Implementing CloudTrail to track account activity for security and compliance.
* **Continuous Compliance:** Using AWS Config to automate resource evaluation and reporting.
* **Secure Operations:** Managing secrets and configuration with SSM Parameter Store.

---

ECS
* **Networking Foundation:** Designing multi-AZ VPCs for container reliability.
* **IAM Security:** Implementing strict separation between Execution and Task roles.
* **Cluster Management:** Provisioning serverless ECS Fargate clusters.
* **Task Definitions:** Defining blueprints using the `awsvpc` network mode.
* **Batch & One-off Jobs:** Running standalone Fargate tasks for migrations and processing.
* **Image Management:** Using Amazon ECR to securely store and version Docker images.
* **Load Balancing:** Distributing traffic to containers via ALB with IP-based targets.
* **Service Orchestration:** Deploying long-running ECS Services with self-healing and ALB integration.
* **Service Auto Scaling:** Implementing dynamic target-tracking scaling based on demand.

---

EKS
* **Control Plane Management:** Provisioning managed EKS clusters with IAM service roles.
* **Networking Foundation:** Designing multi-AZ VPCs required for Kubernetes reliability.
* **Worker Nodes:** Deploying and scaling EC2 Managed Node Groups.
* **Serverless Kubernetes:** Using Fargate Profiles to run pods without managing nodes.
* **EKS Security:** Implementing IRSA (IAM Roles for Service Accounts) and modern Access Entries.
* **Cluster Add-ons:** Managing operational software like VPC CNI natively via the EKS API.
* **Cluster Connectivity:** Configuring `kubectl` to manage resources via `update-kubeconfig`.
* **Kubernetes Orchestration:** (Upcoming) Deploying applications using Helm and kubectl.
* **Observability:** (Upcoming) Monitoring clusters with CloudWatch container insights.

---

APIGATEWAY
* **Synchronous REST APIs:** Connecting HTTP endpoints to Lambda functions via Proxy Integrations.
* **Asynchronous Processing:** Implementing the Storage-First pattern using direct SQS integrations.
* **Fan-Out Webhooks:** Integrating directly with SNS to broadcast messages to multiple subscribers.
* **Event Routing:** Directly ingesting webhooks onto an EventBridge Custom Bus.
* **Request Validation:** Enforcing parameter and schema validation at the edge to reduce backend load.
* **Deployment Management:** Managing immutable snapshots and Stages (dev/prod) for CI/CD.
* **API Security:** Implementing API Keys and Usage Plans for throttling and monetization.

---

CICD
* **Source Control:** Managing private Git repositories with Amazon CodeCommit.
* **Pipeline Infrastructure:** Provisioning S3 artifact storage and IAM service roles.
* **Continuous Integration:** Automating builds and tests with AWS CodeBuild.
* **Deployment Targets:** Provisioning and tagging EC2 instances for automated deployments.
* **Continuous Deployment:** Automating application updates with AWS CodeDeploy.
* **Pipeline Orchestration:** Linking stages together with AWS CodePipeline for full automation.
* **Monitoring & Execution:** Triggering and tracking real-time pipeline status.
* **Infrastructure as Code:** (Upcoming) Automating resource provisioning within the pipeline.

---

TERRAFORM
* **Declarative Provisioning:** Defining infrastructure as code to ensure consistency and repeatability.
* **Dynamic Lookups:** Using Data Sources to fetch AMIs and other external information.
* **Variables & Outputs:** Making configurations dynamic, reusable, and extractable.
* **Security as Code:** Managing IAM roles and policies via version-controlled HCL.
* **Compute Management:** Provisioning and modifying EC2 instances via code.
* **Advanced Networking:** Deploying Application Load Balancers and Target Groups.
* **Modular Design:** Organizing resources into reusable, standardized modules.
* **Networking Foundation:** Designing VPCs and Subnets via code.
* **State Management:** Implementing remote state storage and locking via S3 and DynamoDB.
