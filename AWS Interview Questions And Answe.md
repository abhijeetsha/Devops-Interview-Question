# Devops Interview Questions And Answer
# ✅ AWS Interview Questions And Answer ✅
## ✅ EC2
## 1. What is EC2 and what are its instance types?
### Ans: Amazon EC2 (Elastic Compute Cloud) is an AWS service that provides resizable virtual servers in the cloud to run applications.
### EC2 Instance Types:
### AWS offers different instance families based on workload:
### 1) General Purpose – Balanced CPU, memory, networking
👉 t2, t3, t4g, m5, m6
* Used for web apps, dev/test, small databases

### 2) Compute Optimized – High CPU performance
👉 c5, c6
* Used for batch processing, gaming servers

### 3) Memory Optimized – High RAM
👉 r5, x1
* Used for databases, in-memory caching

### 4) Storage Optimized – High IOPS and throughput
👉 i3, d2
* Used for data warehousing, log processing

### 5) Accelerated Computing – GPU/FPGA
👉 p, g, f1
* Used for ML, AI, video rendering

## 2. Difference between On-Demand, Reserved, and Spot instances?
| Type          | Description                                  | Use Case                               |
| ------------- | -------------------------------------------- | -------------------------------------- |
| **On-Demand** | Pay per hour/second, no commitment           | Short-term, unpredictable workloads    |
| **Reserved**  | Commit for 1 or 3 years (up to 72% cheaper)  | Long-running apps, databases           |
| **Spot**      | Uses unused AWS capacity (up to 90% cheaper) | Batch jobs, CI/CD, fault-tolerant apps |

## 3. How do you secure EC2 instances?
### Ans: EC2 security is implemented at multiple layers:
  * Security Groups – Allow only required ports (e.g., 22, 80, 443)
  * IAM Roles – Avoid hardcoded credentials
  * Key Pairs – Secure SSH access
  * OS-level firewall – iptables / ufw
  * Disable root login & password login
  * Use VPC private subnets
  * Encrypt EBS volumes
  * Patch OS regularly

## 4. What is a Security Group and how is it different from NACL?
### Ans:
### Security Group:
* Acts as a virtual firewall for EC2
* Stateful
* Works at instance level
* Only ALLOW rules
* Default: deny all inbound, allow all outbound

### NACL (Network ACL):
* Works at subnet level
* Stateless
* Supports ALLOW & DENY rules
* Need explicit inbound & outbound rules

### Key Differences:
| Feature  | Security Group | NACL              |
| -------- | -------------- | ----------------- |
| Level    | Instance       | Subnet            |
| Stateful | Yes            | No                |
| Rules    | Allow only     | Allow & Deny      |
| Order    | No order       | Rule number based |

## 5. How do you attach additional EBS volumes to an EC2 instance?
### Ans: Steps:
  * Create an EBS volume in the same AZ as EC2
  * Attach it to the instance
  * Login to EC2
  * Format the disk (if new)
  * Mount the volume
### Code:
  * lsblk
  * mkfs -t ext4 /dev/xvdf
  * mkdir /data
  * mount /dev/xvdf /data

## 6. How do you take backup of EC2?
### Ans: Main methods:

1️⃣ EBS Snapshots (Most common)
  * Point-in-time backup
  * Stored in S3
  * Can restore full instance or individual volumes

2️⃣ AMI (Amazon Machine Image)
  * Backup of:
  * Root volume
  * OS
  * Applications
  * Used to launch new instances

3️⃣ AWS Backup
  * Centralized backup
  * Supports automation and retention policies

## 7. What happens when an EC2 instance is stopped vs terminated?
| Action     | Stopped         | Terminated              |
| ---------- | --------------- | ----------------------- |
| Instance   | Kept            | Deleted                 |
| Root EBS   | Preserved       | Deleted (by default)    |
| IP Address | Lost (public)   | Lost                    |
| Charges    | No compute cost | No cost                 |
| Data       | Safe            | Lost (unless backed up) |

## ✅ VPC
## 1. What is a VPC?
### Ans: VPC (Virtual Private Cloud) is a logically isolated virtual network in AWS where you can launch AWS resources like EC2, RDS, and ELB.
### You control:
  * IP address range (CIDR)
  * Subnets
  * Route tables
  * Internet & NAT gateways
  * Security (SG, NACL)

## 2. Difference between Public and Private Subnet?
### Ans:
| Feature         | Public Subnet             | Private Subnet          |
| --------------- | ------------------------- | ----------------------- |
| Internet access | Yes                       | No (directly)           |
| Route to IGW    | Yes                       | No                      |
| Public IP       | Yes                       | No                      |
| Use case        | Web servers, ALB, Bastion | DB servers, App servers |

## 3. What is an Internet Gateway (IGW)?
### Ans: An Internet Gateway is a VPC component that allows communication between instances in a public subnet and the internet.
### Functions:
  * Enables incoming and outgoing internet traffic
  * Supports IPv4 and IPv6
  * Required for public EC2 instances

## 4. What is a NAT Gateway and why is it used?
### Ans: A NAT Gateway allows instances in a private subnet to:
  * Access the internet outbound only
  * Prevent inbound traffic from the internet

### Why used?
  * OS updates
  * Download packages
  * Access AWS services

## 5. Difference between Security Group and NACL?
| Feature    | Security Group | NACL              |
| ---------- | -------------- | ----------------- |
| Level      | Instance       | Subnet            |
| Stateful   | Yes            | No                |
| Rules      | Allow only     | Allow & Deny      |
| Rule order | Not applicable | Rule number based |
| Default    | Deny inbound   | Allow all         |

## 6. What is a Route Table?
### Ans: A Route Table defines how network traffic is directed within a VPC.
### Example routes:
  * 0.0.0.0/0 → IGW (public subnet)
  * 0.0.0.0/0 → NAT Gateway (private subnet)
  * VPC CIDR → local (internal traffic)
  * 📌 Every subnet must be associated with a route table.

## 7. How do instances in a private subnet access the internet?
### Ans: Through a NAT Gateway (or NAT Instance).
### Flow:
* Private EC2 → Route Table → NAT Gateway → Internet Gateway → Internet
### Steps:
  * NAT Gateway in public subnet
  * Private subnet route table points 0.0.0.0/0 to NAT Gateway
  * NAT Gateway routes traffic via IGW

## ✅ S3
## 1. What is Amazon S3?
### ANs: Amazon S3 (Simple Storage Service) is an object storage service used to store and retrieve any amount of data from anywhere.
### Key features:
  * Highly durable (99.999999999%)
  * Scalable and cost-effective
  * Stores data as objects (bucket + object)
  * Used for backups, logs, media, static websites

## 2. Difference between S3 and EBS?
## Ans: 
| Feature      | S3                     | EBS                 |
| ------------ | ---------------------- | ------------------- |
| Storage type | Object storage         | Block storage       |
| Attachment   | Not attached to EC2    | Attached to one EC2 |
| Use case     | Backup, static content | OS, databases       |
| Durability   | Very high              | High                |
| Access       | HTTP/HTTPS             | OS filesystem       |
| AZ scope     | Regional               | Single AZ           |

## 3. What are S3 storage classes?
### Ans: Amazon S3 offers different storage classes based on access pattern:
  * S3 Standard – Frequently accessed data
  * S3 Intelligent-Tiering – Auto cost optimization
  * S3 Standard-IA – Infrequent access
  * S3 One Zone-IA – Single AZ storage
  * S3 Glacier Instant Retrieval – Archive, fast access
  * S3 Glacier Flexible Retrieval – Archive, minutes–hours
  * S3 Glacier Deep Archive – Lowest cost, long-term archive

## 4. How do you secure an S3 bucket?
### Ans: S3 security is managed at multiple levels:
  * Block Public Access (default)
  * Bucket policies (resource-based)
  * IAM policies (user/role-based)
  * Encryption
    * SSE-S3
    * SSE-KMS
  * Enable versioning
  * Enable access logging
  * Use VPC Endpoint for S3
  * MFA Delete (optional)

## 5. What is S3 versioning?
### Ans: S3 Versioning keeps multiple versions of an object in the same bucket.
### Benefits:
  * Protects against accidental deletion
  * Easy rollback
  * Supports data recovery
  * 📌 Once enabled, it cannot be disabled, only suspended.

## 6. What is S3 lifecycle policy?
## Ans: An S3 Lifecycle Policy automatically manages object lifecycle.
## Examples:
  * Move data to IA or Glacier
  * Delete old versions
  * Clean incomplete uploads
* After 30 days → Standard-IA  
* After 90 days → Glacier  
* After 365 days → Delete

## 7. Can S3 be used for hosting a static website?
### Ans: S3 can host static websites like:
  * HTML
  * CSS
  * JavaScript
  * Images

## Steps:
  * Enable Static Website Hosting
  * Upload website files
  * Configure bucket policy for public read
  * (Optional) Use CloudFront for HTTPS & performance
* ⚠ S3 cannot host dynamic content (no backend code).

## ✅ IAM
### 1. What is IAM?
### Ans: AWS IAM (Identity and Access Management) is a service used to manage access to AWS resources securely.

### With IAM, you can:
  * Create users, groups, and roles
  * Assign permissions using policies
  * Control who can access what in AWS
  * 👉 IAM is a global service (not region-specific).

## 2. Difference between IAM User, Group, and Role?
| Feature | IAM User | IAM Group | IAM Role |
|----|----|----|
| Represents | Individual person/app | Collection of users | AWS service or external identity |
| Credentials | Yes (password, access keys) | No | No permanent credentials |
| Use case | Human access | Permission management | Temporary access |
| Best practice | Avoid long-term keys | Assign policies to group | Preferred for services |

## 3. What is an IAM Role and where is it used?
### Ans: An IAM Role is an AWS identity with temporary security credentials.
### Where used:
  * EC2 → S3 access
  * Lambda → DynamoDB
  * EKS service accounts
  * Cross-account access
  * Federated users (SSO)
  * 📌 Roles eliminate the need to store access keys in code.

## 4. What is the principle of least privilege?
### Ans: The principle of least privilege means:
  * Grant only the minimum permissions required to perform a task.
### Example:
  * Allow s3:GetObject instead of s3:*
  * Restrict access to specific buckets or resources
### Benefits:
  * Reduced security risk
  * Better compliance
  * Limits blast radius

## 5. Difference between inline and managed policies?
| Feature       | Inline Policy       | Managed Policy    |
| ------------- | ------------------- | ----------------- |
| Scope         | One user/role/group | Multiple entities |
| Reusable      | No                  | Yes               |
| Management    | Embedded directly   | Centrally managed |
| Best practice | Rare use            | Recommended       |
* 📌 Managed policies can be AWS-managed or Customer-managed.

## 6. How do EC2 instances access S3 securely without credentials?
### Ans: Using an IAM Role attached to the EC2 instance.
### How it works:
  * Create IAM role with S3 permissions
  * Attach role to EC2
  * EC2 automatically gets temporary credentials
  * Applications access S3 via AWS SDK/CLI

## ✅ RDS
## 1. What is Amazon RDS?
### Ans: Amazon RDS (Relational Database Service) is a managed database service that makes it easy to set up, operate, and scale relational databases in AWS.
### Supported engines:
  * MySQL
  * PostgreSQL
  * MariaDB
  * Oracle
  * SQL Server
  * Amazon Aurora

### AWS manages:
  * OS patching
  * Backups
  * High availability
  * Monitoring

## 2. Difference between RDS and EC2-hosted Database?
### Ans: 
| Feature           | RDS                 | Database on EC2 |
| ----------------- | ------------------- | --------------- |
| Management        | Fully managed       | Self-managed    |
| Backups           | Automatic           | Manual          |
| Patching          | Automatic           | Manual          |
| High availability | Built-in (Multi-AZ) | User configured |
| Scaling           | Easy                | Complex         |
| OS access         | No                  | Yes             |

## 3. What is Multi-AZ deployment?
### Ans: Multi-AZ is a high-availability feature where RDS automatically:
  * Creates a standby replica in another AZ
  * Synchronously replicates data
  * Performs automatic failover during failure
* ✔ Improves availability
* ❌ Does not improve read performance

## 4. What is a Read Replica?
### Ans: A Read Replica is a read-only copy of the primary database.
### Used for:
  * Scaling read traffic
  * Reporting & analytics
  * Disaster recovery

### Key points:
  * Asynchronous replication
  * Can be promoted to standalone DB
  * Improves read performance

## 5. How do you take RDS backups?
### 1️⃣ Automated Backups
* Enabled by default
* Daily snapshots + transaction logs
* Point-in-time recovery
* Retention: 1–35 days

### 2️⃣ Manual Snapshots
* User-initiated
* Retained until deleted
* Used for long-term backups

## 6. How do you secure RDS?
### Ans: RDS security is implemented at multiple levels:
  * VPC & private subnet
  * Security Groups (allow DB port only)
  * IAM authentication
  * Encrypt at rest (KMS)
  * Encrypt in transit (SSL/TLS)
  * Strong DB credentials
  * Enable auditing & monitoring
  * Restrict public access

## ✅ EKS
## 1. What is Amazon EKS?
### Ans: Amazon EKS (Elastic Kubernetes Service) is a fully managed Kubernetes service by AWS that makes it easy to run Kubernetes clusters without managing the control plane.
### AWS manages:
  * Kubernetes control plane
  * API server
  * etcd
  * High availability across AZs

### You manage:
  * Worker nodes
  * Applications
  * Kubernetes resources

## 2. Difference between EKS and self-managed Kubernetes?
### Ans: 
| Feature            | Amazon EKS         | Self-Managed Kubernetes |
| ------------------ | ------------------ | ----------------------- |
| Control plane      | AWS managed        | You manage              |
| High availability  | Built-in           | Manual setup            |
| Upgrades           | Managed by AWS     | Manual                  |
| Security           | IAM integrated     | Manual                  |
| Operational effort | Low                | High                    |
| Cost               | Control plane cost | Infra + ops cost        |
* 📌 EKS reduces operational overhead and improves reliability.

## 3. What are node groups?
### Ans: Node Groups are a collection of EC2 instances that run Kubernetes worker nodes.
### Types:
  * Managed Node Groups – AWS manages lifecycle
  * Self-Managed Node Groups – You manage
  * Fargate – Serverless pods (no EC2)

### Node groups:
  * Auto Scaling enabled
  * Can be On-Demand or Spot
  * Can be GPU based

## 4. How does EKS authentication work?
### Ans: EKS uses AWS IAM for authentication and RBAC for authorization.
### Flow:
  * User authenticates with IAM
  * IAM identity mapped in aws-auth ConfigMap
  * Kubernetes RBAC controls permissions

### Tools:
  * aws eks get-token
  * IAM roles/users
  * Kubernetes roles & rolebindings

## 5. How do you upgrade an EKS cluster?
### Ans: Upgrade process:
  * Upgrade control plane (AWS managed)
  * Upgrade worker nodes
  * Managed node groups
  * Self-managed nodes
  * Upgrade add-ons (CoreDNS, kube-proxy, VPC CNI)
  * Validate workloads
* 📌 Always upgrade one minor version at a time.

## 6. What is IRSA (IAM Roles for Service Accounts)?
### Ans: IRSA allows Kubernetes pods to securely access AWS services using IAM roles.
### Benefits:
  * No hardcoded credentials
  * Fine-grained permissions
  * Better security

###How it works:
  * IAM role linked to Kubernetes service account
  * Uses OIDC provider
  * Pods assume role dynamically

### Use cases:
  * Pod accessing S3
  * Pod accessing DynamoDB
  * Pod accessing Secrets Manager

# ✅ DEVOPS Interview Questions And Answer ✅

## 🔹 Docker Interview Questions
## 1) What is Docker?
### Ans: Docker is a containerization platform that allows developers to package an application along with its dependencies into a container.
Containers run consistently across different environments like development, testing, and production.

## 2) Difference between Docker Image and Docker Container?
### Ans:
| Docker Image              | Docker Container              |
| ------------------------- | ----------------------------- |
| Read-only template        | Running instance of an image  |
| Used to create containers | Executes the application      |
| Stored in Docker registry | Runs in memory                |
| Example: `nginx:latest`   | Example: Running nginx server |

## 3) What is a Dockerfile?
### A Dockerfile is a text file containing instructions to build a Docker image.
### It defines:
* Base image
* Application code
* Dependencies
* Commands to run the app

## 4) Difference between CMD and ENTRYPOINT?
### Ans: Use ENTRYPOINT for the main command and CMD for default arguments.
| CMD                          | ENTRYPOINT              |
| ---------------------------- | ----------------------- |
| Provides default command     | Defines main executable |
| Can be overridden easily     | Harder to override      |
| Used for optional parameters | Used for fixed commands |

## 5) What is a Docker Volume?
### Ans: Docker volume is a persistent storage mechanism used to store data outside the container lifecycle. Even if a container is deleted, the data remains.
### Use cases:
  * Database storage
  * Logs
  * Shared data between containers

## 6) Difference between COPY and ADD?
### Ans: Recommendation: Use COPY unless ADD features are required.
| COPY                         | ADD                     |
| ---------------------------- | ----------------------- |
| Copies files/directories     | Copies + extra features |
| Simple and predictable       | Can extract tar files   |
| Preferred for most use cases | Supports URLs           |
| Best practice                | Use only if needed      |

## 7) How do you reduce Docker image size?
### Ans: 
  * Use lightweight base images (e.g., alpine)
  * Use multi-stage builds
  * Remove unnecessary packages
  * Combine RUN commands
  * Clean cache (apt-get clean)
  * Use .dockerignore

## 8) What is Docker Networking?
### Ans: Docker networking enables communication between containers, the host, and external systems.
### Types of Docker networks:
  * Bridge (default)
  * Host
  * None
  * Overlay (Swarm/Kubernetes)
### Containers in the same network can communicate using container names.

## 9) What is Docker Compose?
### Ans: Docker Compose is a tool used to define and run multi-container applications using a docker-compose.yml file.
### Benefits:
  * Easy multi-container setup
  * Single command to start services
  * Ideal for microservices

## 🔹 Kubernetes Interview Questions (EKS Preferred)
## 1) What is Kubernetes and why is it used?
### Ans: Kubernetes is an open-source container orchestration platform used to deploy, manage, scale, and operate containerized applications.
### It is used for:
  * Automatic scaling
  * High availability
  * Self-healing
  * Rolling updates & rollbacks
  * Managing microservices
  👉 EKS (Elastic Kubernetes Service) is AWS’s managed Kubernetes service where AWS manages the control plane.

## 2) What is a Pod?
### Ans: A Pod is the smallest deployable unit in Kubernetes.
  * Contains one or more containers
  * Containers in a Pod share:
    * Same network (IP & port space)
    * Same storage volumes
  * Pods are ephemeral (not permanent)

## 3) Difference between Deployment, StatefulSet, and DaemonSet?
### Ans: 
| Feature      | Deployment     | StatefulSet        | DaemonSet               |
| ------------ | -------------- | ------------------ | ----------------------- |
| Use case     | Stateless apps | Stateful apps      | Node-level services     |
| Pod identity | Random         | Stable & unique    | One pod per node        |
| Storage      | Shared         | Persistent per pod | Optional                |
| Examples     | Web apps       | DB, Kafka          | Logs, monitoring agents |

## 4) What is Deployment Stategies And Tyoes..?
### Ans: Four Tyoes of Deployment Strategy given below
| Strategy       | Downtime | Risk     | Complexity |
| -------------- | -------- | -------- | ---------- |
| Rolling Update | ❌ No     | Low      | Low        |
| Recreate       | ✅ Yes    | Medium   | Very Low   |
| Blue-Green     | ❌ No     | Very Low | Medium     |
| Canary         | ❌ No     | Very Low | High       |
| A/B Testing    | ❌ No     | Low      | High       |

## 5) What is a Service and its types?
### Ans: A Service provides a stable network endpoint to access Pods.
### Types of Services:
  * ClusterIP – Internal access (default)
  * NodePort – Exposes app on node IP & port
  * LoadBalancer – Uses cloud load balancer (AWS ELB/NLB)
  * ExternalName – Maps to external DNS

## 6) Difference between ConfigMap and Secret?
### Ans: In EKS, Secrets can be integrated with AWS Secrets Manager.
| ConfigMap                 | Secret                   |
| ------------------------- | ------------------------ |
| Stores non-sensitive data | Stores sensitive data    |
| Plain text                | Base64 encoded           |
| App configs               | Passwords, tokens        |
| No encryption by default  | Can be encrypted at rest |

## 7) What is Ingress?
### Ans: Ingress manages external HTTP/HTTPS access to Kubernetes services.
  * Works with an Ingress Controller
  * Supports:
    * Path-based routing
    * Host-based routing
    * SSL/TLS termination
    * 👉 In EKS, commonly used:
    * AWS Load Balancer Controller (ALB Ingress)

## 8) What is HPA (Horizontal Pod Autoscaler)?
### Ans: HPA automatically scales the number of Pods based on:
  * CPU utilization
  * Memory utilization
  * Custom metrics
### Example:
  * Scale pods from 2 → 10 when CPU > 70%

## 9) How does Kubernetes handle pod failure?
### Ans: Kubernetes provides self-healing:
* If a Pod crashes → recreated automatically
* If a node fails → Pods are rescheduled on other nodes
* Uses:
  * Liveness & Readiness probes
  * ReplicaSets

## 10) How does Kubernetes perform rolling updates?
### Ans: Rolling updates update Pods gradually without downtime.
### Process:
  * Create new Pods with updated version
  * Terminate old Pods slowly
  * Controlled using:
  * maxSurge
  * maxUnavailable
### Supports rollback if deployment fails.

## 11) How do you expose applications running in EKS?
### Ans: You can expose apps using:

1️⃣ Service type LoadBalancer
→ Creates AWS ELB/NLB

2️⃣ Ingress (ALB)
→ Recommended for production

3️⃣ NodePort
→ Mostly for testing

4️⃣ Port Forwarding
→ Debugging only

## 🔹 Terraform (Infrastructure as Code)
## 1) What is Terraform?
### Ans: Terraform is an Infrastructure as Code (IaC) tool by HashiCorp used to provision, manage, and version infrastructure using declarative configuration files.
### It supports:
  * Cloud providers (AWS, Azure, GCP)
  * On-prem infrastructure
  * SaaS tools

## 2) What is Infrastructure as Code?
### Ans: Infrastructure as Code is the practice of managing infrastructure using code instead of manual processes.
### Benefits:
  * Automation
  * Consistency
  * Version control
  * Faster deployments
  * Easy rollback 

## 3) What are Terraform providers?
### Ans: Providers are plugins that allow Terraform to interact with APIs of cloud providers and services.
### Examples:
* aws
* kubernetes
* helm
* github
### Each provider defines the resources and data sources it supports.

## 4) Difference between resource and data source?
### Ans:
| Resource                          | Data Source                   |
| --------------------------------- | ----------------------------- |
| Creates or manages infrastructure | Reads existing infrastructure |
| Changes state                     | Does not modify state         |
| Example: `aws_instance`           | Example: `data.aws_ami`       |


## 5) What is Terraform state?
### Ans: Terraform state is a file (terraform.tfstate) that maps Terraform resources to real infrastructure.
### It helps Terraform:
  * Track resource changes
  * Perform updates & deletes
  * Avoid duplication

## 6) Where do you store Terraform state in production?
### Ans: In production, Terraform state should be stored in a remote backend like:
  * AWS S3 (with DynamoDB for locking)
  * Terraform Cloud
  * Azure Blob Storage
  * 👉 Never store state locally in production.

## 7) What is remote backend?
### Ans: A remote backend stores Terraform state remotely and enables:
* Team collaboration
* State locking
* Secure storage
### Example:
* S3 + DynamoDB (lock & consistency)

## 8) Difference between terraform plan and apply?
### Ans: 
| terraform plan       | terraform apply           |
| -------------------- | ------------------------- |
| Shows execution plan | Applies changes           |
| No infra changes     | Creates/updates resources |
| Used for review      | Used for deployment       |


## 9) What is a Terraform module?
### Ans: A module is a reusable collection of Terraform configurations.
### Benefits:
* Code reusability
* Standardization
* Easier maintenance
### Tyes:
* Root module
* Child module
* Registry modules

## 10) What are workspaces?
### Ans: Workspaces allow multiple state files from the same configuration.
### Use cases:
* dev / staging / prod environments
* Command:
  * terraform workspace new dev
  * terraform workspace select prod
 
## 11) How do you manage secrets in Terraform?
### Ans: Best practices:
  * Use environment variables
  * Use AWS Secrets Manager / Parameter Store 
  * Use terraform.tfvars (not committed)
  * Encrypt state files
  * Avoid hardcoding secrets

## 12) What happens if Terraform state is deleted?
### Ans: If state is deleted:
* Terraform loses track of existing infrastructure
* Next apply may try to recreate resources
* Can cause duplication or conflicts
### 👉 Recovery:
* Restore state from backup
* Use terraform import

## 🔹 CI/CD Interview Questions
## 1) What is CI/CD?
### Ans: CI/CD stands for Continuous Integration and Continuous Deployment/Delivery.
* CI: Automatically build & test code
* CD: Automatically deploy application

## 2) What are the benefits of CI/CD?
### Ans: 
* Faster releases
* Early bug detection
* Automation
* Consistent deployments
* Reduced manual errors

## 3) What are common CI/CD tools?
### Ans: 
* Jenkins
* GitHub Actions
* GitLab CI/CD
* AWS CodePipeline
* Azure DevOps

## 4) What is a CI/CD pipeline?
### Ans: A pipeline is an automated workflow that includes:
* Code checkout
* Build
* Test
* Security scan
* Deploy

## 5) Difference between Continuous Delivery and Continuous Deployment?
### Ans: 
| Continuous Delivery | Continuous Deployment |
| ------------------- | --------------------- |
| Manual approval     | Fully automated       |
| Safer               | Faster                |
| Production optional | Always to production  |

## 6) How do you secure CI/CD pipelines?
### Ans: 
* Use secrets managers
* Least-privilege IAM roles
* Secure credentials
* Code scanning
* Pipeline approvals

## 7) How does CI/CD integrate with Docker & Kubernetes?
### Ans: 
* CI builds Docker images
* Pushes to container registry
* CD deploys to Kubernetes using:
  * Helm
  * kubectl
  * ArgoCD

## ✅ Jenkins Interview Questions
## 1) What is Jenkins?
### Ans: Jenkins is an open-source CI/CD automation tool used to build, test, and deploy applications.
### It helps automate:
* Code build
* Unit testing
* Docker image creation
* Deployment to servers or Kubernetes
### Jenkins supports 1000+ plugins and integrates easily with Git, Docker, AWS, and Kubernetes. 

## 2) What is a Jenkins pipeline?
### Ans: A Jenkins Pipeline is a set of automated steps written as code to define the CI/CD process.
### It includes stages such as:
* Checkout
* Build
* Test
* Deploy
### Pipelines are version-controlled and stored in Git.

## 3) Difference between Declarative and Scripted pipeline?
### Ans: Best practice: Use Declarative pipelines for standard CI/CD.
| Declarative Pipeline         | Scripted Pipeline       |
| ---------------------------- | ----------------------- |
| Simple & structured          | Flexible & powerful     |
| Uses predefined syntax       | Uses Groovy scripting   |
| Easier to maintain           | Complex logic supported |
| Preferred for most use cases | Used for advanced logic |

## 4) What is a Jenkinsfile?
### Ans: A Jenkinsfile is a text file that defines the Jenkins pipeline.
* Stored in source code repository
* Written in Groovy
* Enables Pipeline as Code

## 5) How do you secure Jenkins?
### Ans: Security best practices:
* Enable role-based access control
* Use Jenkins credentials store
* Integrate with LDAP / Active Directory
* Use HTTPS (SSL)
* Restrict agent permissions
* Regular plugin updates

## 6) How do you integrate Jenkins with Git?
### Ans: Steps:
* Install Git plugin
* Configure Git repository URL
* Add SSH key or access token
* Configure webhook for auto-trigger
* Jenkins pulls code on commit
### Supported Git platforms:
* GitHub
* GitLab
* Bitbucket

## 7) How do you deploy applications using Jenkins?
### Ans: Jenkins deploys apps by:
* Building artifacts (JAR/Docker image)
* Pushing image to registry
### Deploying using:
* SSH
* Ansible
* Docker
* Kubernetes (kubectl/Helm)
* AWS services
### Example:
* Jenkins → Docker → ECR → EKS

## ✅ GitHub Actions / GitLab CI Interview Questions
## 1) What is CI/CD?
### Ans: CI/CD stands for Continuous Integration and Continuous Deployment/Delivery.
* CI: Automatically build and test code on every commit
* CD: Automatically deploy applications to staging/production
### Goal: faster, reliable, and automated software delivery.

## 2) Difference between GitHub Actions and Jenkins?
### Ans: Jenkins is more flexible; GitHub Actions is easier to manage.
| GitHub Actions         | Jenkins                    |
| ---------------------- | -------------------------- |
| Cloud-native           | Self-hosted                |
| YAML-based workflows   | Groovy pipelines           |
| Integrated with GitHub | Plugin-based               |
| Less maintenance       | Requires server management |


## 3) What is a workflow in GitHub Actions?
### Ans: A workflow is an automated process defined in a YAML file under:
### Command: .github/workflows/
### It contains:
* Triggers (push, PR, schedule)
* Jobs
* Steps
* Runners

## 3) What are runners?
### Ans: Runners are servers that execute CI/CD jobs.
### Types:
* GitHub-hosted runners
* Self-hosted runners
* They run tasks like build, test, and deploy.

## 4) What is a pipeline in GitLab CI?
### Ans: A pipeline is a set of jobs defined in .gitlab-ci.yml.
### It runs in stages, such as:
* build
* test
* deploy
### Triggered on commits, merge requests, or schedules.

## 5) How do you store secrets in CI/CD?
### Ans: Best practices:
* Use GitHub Secrets / GitLab CI Variables
* Use cloud secret managers (AWS Secrets Manager)
* Never hardcode credentials
* Restrict access & rotate secrets
* Encrypt secrets at rest

## 6) How do you implement rollback in CI/CD?
### Ans: Rollback methods:
* Kubernetes rolling rollback (kubectl rollout undo)
* Blue-Green deployment
* Canary deployment
* Versioned artifacts/images
* Rollback is triggered when health checks fail.

## 7) How do you deploy to AWS using CI/CD?
### Ans: Typical flow:
* CI builds application
* Create Docker image
* Push image to ECR
* Deploy to EKS / EC2 / ECS
* Validate using health checks
### Tools:
* GitHub Actions / Jenkins
* Terraform
* kubectl / Helm

## ⭐ Scenario-Based DevOps Questions (Very Important)
## 1) How would you deploy a Java application on AWS using Docker & Kubernetes?
### Ans: Steps:
* Build Java app using Maven
* Create Docker image
* Push image to Amazon ECR
* Create Kubernetes manifests
* Deploy to EKS using kubectl/Helm
* Expose using ALB Ingress

## 2) How do you design high availability architecture in AWS?
### Ans: 
* Use Multi-AZ
* Application Load Balancer
* Auto Scaling Groups
* RDS Multi-AZ
* EKS with multiple nodes
* Route 53 health checks

## 3) How do you automate infrastructure creation using Terraform?
### Ans: 
* Write Terraform code for AWS resources
* Use remote backend (S3 + DynamoDB)
* Use modules for reusability
* Apply via CI/CD pipeline
* Version control in Git 

## 4) How do you implement zero-downtime deployment?
### Ans: Methods:
* Rolling updates
* Blue-Green deployment
* Canary deployment
* Load balancer health checks
* Kubernetes readiness probes
* How do you troubleshoot a pod not starting?

## 5) How do you secure CI/CD pipelines?
### Ans: Security practices:
* Least-privilege IAM roles
* Secure secrets management
* Code scanning & SAST
* Image vulnerability scanning
* Approval gates
* Audit logging

## 6) How do you troubleshoot a pod not starting?
### Ans: Steps:
* kubectl get pods
* kubectl describe pod
* Check events & logs
* Validate image & resources
* Check ConfigMaps/Secrets
* Verify node health
