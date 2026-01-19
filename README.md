# 🚀 AWS Application Load Balancer with Auto Scaling (Real-World Project)

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![EC2](https://img.shields.io/badge/EC2-Compute-yellow)
![VPC](https://img.shields.io/badge/VPC-Network-blue)
![ALB](https://img.shields.io/badge/LoadBalancer-ALB-green)
![ASG](https://img.shields.io/badge/AutoScaling-Enabled-success)

---

## 📌 Project Overview

This project demonstrates a **real-world, production-style AWS architecture** where a web application runs securely on **private EC2 instances** behind an **Application Load Balancer (ALB)** with **Auto Scaling Group (ASG)**.

The infrastructure is designed following **AWS best practices** for:
- 🔐 Security
- 📈 Scalability
- 🌍 High Availability

---

## 🏗️ Architecture Diagram (Logical Flow)

```
User
 ↓
Application Load Balancer (Public Subnet)
 ↓
Target Group
 ↓
Auto Scaling Group
 ↓
Private EC2 Instances (Apache Web Server)
 ↓
NAT Gateway → Internet (Outbound Only)
```

---

## 🧰 AWS Services Used

- Amazon VPC  
- Amazon EC2 (Ubuntu)  
- Application Load Balancer (ALB)  
- Auto Scaling Group (ASG)  
- Target Groups  
- NAT Gateway  
- Internet Gateway  
- Security Groups  

---

## ⚙️ Key Features

✅ EC2 instances run in **private subnets (no public IP)**  
✅ Internet access only through **ALB**  
✅ Outbound internet via **NAT Gateway**  
✅ Auto Scaling based on demand  
✅ Highly available across multiple AZs  

---

## 🪜 Step-by-Step Implementation

### 1️⃣ VPC Creation
- Custom VPC with CIDR: `10.0.0.0/16`

### 2️⃣ Subnets
- **Public Subnets** → ALB & NAT Gateway  
- **Private Subnets** → EC2 instances  

### 3️⃣ Internet Gateway
- Attached to VPC for inbound internet traffic

### 4️⃣ NAT Gateway
- Created in public subnet
- Enables outbound internet for private EC2

### 5️⃣ Security Groups
**ALB Security Group**
- Allow HTTP (80) from `0.0.0.0/0`

**EC2 Security Group**
- Allow HTTP (80) only from ALB SG

### 6️⃣ Launch Template
- Ubuntu AMI
- Apache installed using User Data script

### 7️⃣ Target Group
- Target type: Instance
- Protocol: HTTP (80)
- Health check path: `/`

### 8️⃣ Application Load Balancer
- Internet-facing
- Listener on port 80
- Attached to target group

### 9️⃣ Auto Scaling Group
- Min: 1
- Desired: 2
- Max: 3
- Integrated with ALB

---

## 📜 User Data Script (Ubuntu EC2)

```bash
#!/bin/bash
apt update -y
apt install -y apache2
systemctl start apache2
systemctl enable apache2

echo "<h1>AWS ALB + Auto Scaling Web Server</h1><h2>Hostname: $(hostname)</h2>" > /var/www/html/index.html
```

---

## 🧪 Verification Steps

1. Copy **ALB DNS name**
2. Open browser:
```
http://<ALB-DNS-NAME>
```
3. Refresh page multiple times
4. Observe **different hostnames** (load balancing working)

---

## ✅ Final Outcome

✔ Secure architecture with no public EC2 IPs  
✔ Load balancing across multiple instances  
✔ Auto scaling handles traffic automatically  
✔ Production-grade AWS setup  

---

## 🧠 Key Learnings

- Designing secure AWS VPC architecture  
- Load balancing & auto scaling concepts  
- Real-world cloud networking  
- Hands-on AWS infrastructure deployment  

---

## 📌 Use Cases

- Enterprise web applications  
- Microservices backend  
- Scalable production workloads  

---

## 👨‍💻 Author

**Irfan Pasha**  
Cloud Engineer | AWS Enthusiast  

🔗 GitHub:[https://github.com/yourusername](https://github.com/IrfanPasha05/aws-alb-autoscaling-project/edit/main/README.md)  
🔗 DEV: https://dev.to/yourusername  

---

⭐ If you found this project helpful, please give it a star!
