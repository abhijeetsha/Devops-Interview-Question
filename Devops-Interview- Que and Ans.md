# Devops Interview Questions And Answer
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

