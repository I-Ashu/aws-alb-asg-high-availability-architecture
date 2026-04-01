# 🚀 AWS Highly Available Architecture (ALB + Auto Scaling + Multi-AZ)

<img width="1536" height="1024" alt="ASG+ALB+VPC Arch" src="https://github.com/user-attachments/assets/8b3a5b75-0532-48a3-8fee-fbe3bfee1e71" />

---

## 📌 Overview

Built a highly available and scalable AWS architecture using **Application Load Balancer (ALB)** and **Auto Scaling Group (ASG)** across multiple Availability Zones.

The system is designed to:
- Eliminate single point of failure  
- Automatically scale and self-heal  
- Secure backend infrastructure using private subnets  

---

## 🏗️ Architecture

- VPC (Multi-AZ)
- 2 Public Subnets (ALB + NAT Gateway)
- 2 Private Subnets (EC2 via ASG)
- Internet Gateway (IGW)
- 2 NAT Gateways (one per AZ)
- Application Load Balancer (ALB)
- Target Group
- Auto Scaling Group (ASG)
- Launch Template
- AWS Systems Manager (SSM)

---

## 🔄 Traffic Flow


---

## ⚙️ Key Components

### ⚖️ Application Load Balancer (ALB)
- Internet-facing
- Deployed across public subnets
- Routes traffic only to healthy instances

---

### 🔁 Auto Scaling Group (ASG)
- Launch Template based
- Min: 2 | Desired: 2 | Max: 4
- Automatically replaces unhealthy instances
- Distributes instances across multiple AZs

---

### 🖥️ EC2 Instances (Private)
- No public IP
- Receives traffic only from ALB
- Accessed via AWS Systems Manager (SSM)

---

### 🌐 NAT Gateway
- One per AZ for high availability
- Enables outbound internet for private instances

---

### 🔐 Security
- No direct SSH access
- Security Groups:
  - ALB → EC2 (HTTP 80 only)
- Private subnet isolation

---

## ⚙️ Deployment Flow (How I Built It)

1. Created VPC with CIDR `10.0.0.0/16`  
2. Designed 4 subnets across 2 AZs (public + private)  
3. Attached Internet Gateway and configured public route table  
4. Created 2 NAT Gateways (one per AZ)  
5. Configured private route tables pointing to NAT Gateways  
6. Created Application Load Balancer in public subnets  
7. Configured Target Group with health checks (HTTP:80)  
8. Created Launch Template with user-data script  
9. Created Auto Scaling Group across private subnets  
10. Validated traffic flow and failover behavior  

---

## 🧠 Design Decisions

- Used private subnets for EC2 to avoid direct internet exposure  
- Implemented ALB for load distribution and fault tolerance  
- Used NAT Gateway per AZ to avoid single point of failure  
- Used ASG for automatic scaling and recovery  
- Used SSM instead of SSH for secure access  

---

## 🧪 Validation

- Verified ALB routing traffic correctly  
- Simulated instance failure → ASG auto replaced instance  
- Confirmed zero downtime  
- Validated multi-AZ traffic distribution  

---

aws-alb-asg-high-availability-architecture/
├── architecture.png
├── README.md
├── user-data.sh


## 👤 Author

**Ashutosh Chaudhary**  
Cloud Operations Engineer | AWS | Terraform | Linux | 
