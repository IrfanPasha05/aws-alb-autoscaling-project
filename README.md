\# 🚀 AWS ALB + Auto Scaling Group (Real-Time Project)



\## 📌 Project Overview

This project demonstrates a \*\*production-style AWS architecture\*\* where a web application runs on \*\*private EC2 instances\*\* and is exposed to the internet using an \*\*Application Load Balancer (ALB)\*\* with \*\*Auto Scaling Group (ASG)\*\*.



The setup follows AWS best practices for \*\*security, scalability, and high availability\*\*.



---



\## 🏗️ Architecture Components

\- Custom VPC

\- Public \& Private Subnets

\- Internet Gateway

\- NAT Gateway

\- Application Load Balancer (ALB)

\- Target Group

\- Launch Template

\- Auto Scaling Group

\- Ubuntu EC2 with Apache (User Data)



---



\## ⚙️ Services Used

\- Amazon VPC

\- Amazon EC2

\- Application Load Balancer

\- Auto Scaling Group

\- Target Groups

\- NAT Gateway

\- Internet Gateway

\- Security Groups



---



\## 🪜 Step-by-Step Implementation



\### 1️⃣ Created Custom VPC

\- CIDR block: `10.0.0.0/16`



\### 2️⃣ Created Subnets

\- Public Subnets → ALB \& NAT Gateway

\- Private Subnets → EC2 instances



\### 3️⃣ Internet Gateway

\- Attached to VPC for inbound internet traffic



\### 4️⃣ NAT Gateway

\- Created in public subnet

\- Enabled outbound internet access for private EC2



\### 5️⃣ Security Groups

\- \*\*ALB SG\*\*: Allows HTTP (80) from Internet

\- \*\*EC2 SG\*\*: Allows HTTP (80) only from ALB SG



\### 6️⃣ Launch Template

\- Ubuntu AMI

\- Apache installed using User Data script



\### 7️⃣ Target Group

\- Target type: Instance

\- Protocol: HTTP (80)

\- Health check path: `/`



\### 8️⃣ Application Load Balancer

\- Internet-facing ALB

\- Attached to public subnets

\- Listener on port 80



\### 9️⃣ Auto Scaling Group

\- Desired capacity: 2

\- Min: 1 | Max: 3

\- Integrated with ALB target group



---



\## 📜 User Data Script (Ubuntu)



```bash

\#!/bin/bash

apt update -y

apt install -y apache2

systemctl start apache2

systemctl enable apache2

echo "<h1>ALB + Auto Scaling Web Server</h1><h2>Hostname: $(hostname)</h2>" > /var/www/html/index.html



