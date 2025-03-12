# AWS 3-Tier Architecture Web App

This repository demonstrates the setup of a **3-tier architecture** for a **web application** on **AWS**. The architecture includes the **Web Tier**, **Application Tier**, and **Database Tier**, following best practices for scalability, security, and performance.

## Key Features

- **End-to-End Deployment**: A fully functional example of a 3-tier web application setup with AWS services like **EC2**, **RDS**, **VPC**, **Auto Scaling**, **Load Balancing**, and more.
- **Scalable**: The setup is designed to be scalable for both small and large traffic loads.
- **Secure**: Follows security best practices, including private subnets, secure EC2 instances, and IAM roles.
- **Highly Available**: Designed for availability with features such as multiple subnets, load balancing, and fault tolerance.
- **Infrastructure Setup**: Uses AWS native services for the setup, without the need for tools like Terraform or Docker.

## Platforms

- **AWS** (EC2, RDS, VPC, Load Balancer, Auto Scaling, Security Groups, Subnets, NAT Gateway)

## Architecture Overview

### Web Tier

The **Web Tier** consists of the **EC2 instances** running the web server (Apache/Nginx) and hosting the frontend of the application. This tier communicates with the **Application Tier** via HTTP and serves static and dynamic content to the client.

### Application Tier

The **Application Tier** is where the business logic resides, typically running on EC2 instances or AWS Lambda (for serverless applications). It interacts with the **Database Tier** and processes client requests.

### Database Tier

The **Database Tier** utilizes **Amazon RDS** for relational databases. It handles data storage, retrieval, and manipulation and communicates directly with the Application Tier.

---

## Setup Guide

### Prerequisites

- **AWS Account**: Ensure you have an active AWS account with appropriate permissions to create and manage VPCs, EC2 instances, RDS databases, etc.
- **AWS CLI**: Install and configure the AWS Command Line Interface (CLI) for managing AWS services.

### Setting Up Infrastructure

1. **Provision Resources:**

   Follow the AWS console or CLI to manually provision the following resources:
   
   - **VPC**: Create a custom VPC with appropriate CIDR blocks.
   - **Subnets**: Create public and private subnets for each tier.
   - **Internet Gateway**: Attach the internet gateway to the VPC for external communication.
   - **NAT Gateway**: Set up NAT Gateway for private subnets to access the internet.
   - **Route Tables**: Configure route tables to control traffic flow.
   - **Security Groups**: Set up security groups to allow specific traffic (HTTP, SSH, etc.).
   - **EC2 Instances**: Launch EC2 instances in the appropriate subnets for Web and Application Tiers.
   - **RDS Instance**: Set up an RDS instance for the Database Tier.

2. **Configure Load Balancer:**

   Set up an **Elastic Load Balancer (ELB)** to distribute traffic to your EC2 instances in the Web Tier.

3. **Auto Scaling:**

   Configure **Auto Scaling** for EC2 instances to automatically scale based on traffic load.

4. **Access the Web App:**

   Once the resources are provisioned, you can access your web app via the public IP or the load balancer's DNS name.

---

## Detailed AWS Service Usage

### **VPC (Virtual Private Cloud)**

The VPC provides the network infrastructure for your application, and is divided into public and private subnets. 

- **Public Subnets**: Used for resources that need to be accessible from the internet (e.g., Web Tier EC2 instances, Load Balancer).
- **Private Subnets**: Used for backend resources that should not be directly accessible from the internet (e.g., Application Tier EC2 instances, RDS databases).
  
### **Security Groups**

Security Groups are configured to control access to EC2 instances:

- **Web Tier**: Allow HTTP (port 80) and HTTPS (port 443) traffic.
- **Application Tier**: Allow only internal traffic from the Web Tier on specific ports.
- **Database Tier**: Allow access only from the Application Tier.

### **Elastic Load Balancer (ELB)**

The ELB balances incoming traffic to EC2 instances in the **Web Tier**. This ensures high availability and fault tolerance for the front-end application. The Load Balancer is set up in the public subnet and routes traffic to the EC2 instances in private subnets for security.

### **Auto Scaling**

The EC2 Auto Scaling group ensures that the number of EC2 instances in the Web and Application tiers can automatically scale up or down based on traffic patterns. The Auto Scaling policy is set up to maintain a minimum, maximum, and desired number of instances.

### **RDS (Relational Database Service)**

The RDS instance is provisioned in the private subnet to manage relational data for the app. It communicates with the **Application Tier** to store and retrieve data. RDS provides features such as automatic backups, patch management, and scaling.

### **Route Tables and NAT Gateway**

- **Route Tables**: Control the flow of traffic within the VPC and between subnets.
- **NAT Gateway**: Ensures that instances in private subnets can access the internet for necessary updates and downloads while keeping the instances secure.

---

## Additional Features

- **Auto Scaling**: The architecture is designed to handle auto-scaling for EC2 instances based on traffic load.
- **Load Balancer**: Using **Elastic Load Balancing (ELB)** to distribute traffic between multiple EC2 instances.
- **High Availability**: The infrastructure is designed across multiple availability zones for redundancy.
- **NAT Gateway**: Provides secure internet access for instances in private subnets.
