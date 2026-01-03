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
