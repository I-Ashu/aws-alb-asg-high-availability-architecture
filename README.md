# 🚀 AWS Highly Available Architecture (ALB + Auto Scaling + Multi-AZ)

<img width="1536" height="1024" alt="ASG+ALB+VPC Arch" src="https://github.com/user-attachments/assets/8b3a5b75-0532-48a3-8fee-fbe3bfee1e71" />

---

## 📌 Overview

Built a highly available and scalable AWS architecture using **Application Load Balancer and Auto Scaling Group** across multiple Availability Zones.

Designed to ensure:
- No single point of failure  
- Automatic scaling & self-healing  
- Secure private infrastructure  

---

## 🏗️ Architecture

- VPC (Multi-AZ)
- 2 Public Subnets (ALB + NAT Gateway)
- 2 Private Subnets (EC2 via ASG)
- Internet Gateway (IGW)
- 2 NAT Gateways (one per AZ)
- Application Load Balancer (ALB)
- Target Group
- Auto Scaling Group (ASG) with Launch Template
- AWS Systems Manager (SSM) for access

---

## 🔄 Traffic Flow (CORRECT)


---

## ⚙️ Key Components

### ⚖️ ALB
- Internet-facing
- Deployed across public subnets
- Routes traffic to healthy instances only

---

### 🔁 Auto Scaling Group (ASG)
- Launch Template based
- Min: 2 | Desired: 2 | Max: 4
- Automatically replaces unhealthy instances
- Distributes instances across AZs

---

### 🖥️ EC2 (Private)
- No public IP
- Receives traffic only from ALB
- Access via SSM (no SSH)

---

### 🌐 NAT Gateway
- One per AZ (high availability)
- Enables outbound internet for private EC2

---

### 🔐 Security
- No direct SSH access
- Security Groups:
  - ALB → EC2 (HTTP 80 only)
- Private subnet isolation

---

## 🧪 Validation

- Verified ALB routing to healthy instances  
- Tested instance failure → ASG auto replaced  
- Confirmed zero downtime  
- Validated multi-AZ traffic distribution  

---

## 👤 Author

**Ashutosh Chaudhary**  

Cloud Operations Engineer | AWS | Terraform | Linux | 
