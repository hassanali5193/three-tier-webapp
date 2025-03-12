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


## Diagram

![AWS 3-Tier Architecture] data:image/jpeg;base64,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

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
