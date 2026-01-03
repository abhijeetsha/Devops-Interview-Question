## ✅ DEVOPS Interview Questions And Answer ✅

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
