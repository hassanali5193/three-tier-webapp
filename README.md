# three-tier-webapp

# AWS 3-Tier Architecture Setup Guide

This guide provides step-by-step instructions to set up a 3-tier architecture on AWS, comprising the Web Tier, Application Tier, and Database Tier. Each tier is designed to be scalable and secure, following AWS best practices.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up the Infrastructure](#setting-up-the-infrastructure)
   - [Create a Virtual Private Cloud (VPC)](#create-a-virtual-private-cloud-vpc)
   - [Set Up Subnets](#set-up-subnets)
   - [Create an Internet Gateway](#create-an-internet-gateway)
   - [Set Up a NAT Gateway](#set-up-a-nat-gateway)
   - [Configure Route Tables](#configure-route-tables)
3. [Deploying the Tiers](#deploying-the-tiers)
   - [Web Tier](#web-tier)
   - [Application Tier](#application-tier)
   - [Database Tier](#database-tier)
4. [Verifying Connectivity](#verifying-connectivity)

## Prerequisites

- **AWS Account:** Ensure you have an active AWS account with appropriate permissions to create and manage VPCs, subnets, EC2 instances, RDS databases, and other AWS resources.
- **AWS CLI:** Install and configure the AWS Command Line Interface (CLI) for managing AWS services.
- **GitHub Account:** Set up a GitHub account to store and version-control your infrastructure code and configurations.

## Setting Up the Infrastructure

### Create a Virtual Private Cloud (VPC)

1. **Navigate to VPC Dashboard:**
   - Log in to the AWS Management Console.
   - Go to the VPC dashboard.

2. **Create VPC:**
   - Click on "Create VPC."
   - Choose "VPC only."
   - Name your VPC (e.g., `MyVPC`).
   - Set the IPv4 CIDR block to `10.10.0.0/16`.
   - Click "Create VPC."

### Set Up Subnets

1. **Navigate to Subnets:**
   - In the VPC dashboard, click on "Subnets."

2. **Create Subnets:**
   - Click "Create subnet."
   - Select your VPC.
   - Create 2 public subnets for the Web Tier and 4 private subnets (2 each for Application and Database Tiers).
   - Assign appropriate CIDR blocks (e.g., `10.10.1.0/24` for the first public subnet).
   - Enable "Auto-assign public IPv4 address" for public subnets.

### Create an Internet Gateway

1. **Navigate to Internet Gateways:**
   - In the VPC dashboard, click on "Internet Gateways."

2. **Create and Attach Internet Gateway:**
   - Click "Create Internet Gateway."
   - Name it (e.g., `MyInternetGateway`).
   - Click "Create."
   - Select the new Internet Gateway, click "Actions," then "Attach to VPC."
   - Choose your VPC and click "Attach Internet Gateway."

### Set Up a NAT Gateway

1. **Navigate to NAT Gateways:**
   - In the VPC dashboard, click on "NAT Gateways."

2. **Create NAT Gateway:**
   - Click "Create NAT Gateway."
   - Name it (e.g., `MyNATGateway`).
   - Select a public subnet.
   - Allocate an Elastic IP.
   - Click "Create NAT Gateway."

### Configure Route Tables

1. **Public Route Table:**
   - In the VPC dashboard, click on "Route Tables."
   - Create a new route table for public subnets.
   - Associate it with the public subnets.
   - Add a route: Destination `0.0.0.0/0`, Target "Internet Gateway."

2. **Private Route Table:**
   - Create a new route table for private subnets.
   - Associate it with the private subnets.
   - Add a route: Destination `0.0.0.0/0`, Target "NAT Gateway."

## Deploying the Tiers

### Web Tier

1. **Launch Template:**
   - In the EC2 dashboard, go to "Launch Templates."
   - Create a new launch template:
     - Name it (e.g., `WebTierTemplate`).
     - Select Amazon Linux as the AMI.
     - Choose `t2.micro` as the instance type.
     - Create a new key pair or use an existing one.
     - Configure network settings:
       - Create a security group allowing SSH (port 22) and HTTP (port 80) from any IP.
       - Enable "Auto-assign public IP."
     - In "Advanced Details," add user data to install and start the Apache web server.

2. **Launch Web Tier EC2 Instances:**
   - Navigate to the EC2 dashboard and click "Instances" > "Launch Instance."
   - Choose "Launch Instance from Template."
   - Select the previously created `WebTierTemplate`.
   - Choose the public subnets for the Web Tier.
   - Launch two EC2 instances for high availability.
   - Ensure the security group allows HTTP (port 80) and SSH (port 22) access from anywhere.
   - Once the instances are launched, confirm they are accessible by visiting their public IPs in a web browser.

### Application Tier

1. **Launch Template for Application Tier:**
   - In the EC2 dashboard, go to "Launch Templates."
   - Create a new launch template:
     - Name it (e.g., `AppTierTemplate`).
     - Select Amazon Linux or another AMI.
     - Choose `t2.micro` or an appropriate instance type based on your needs.
     - Create a new key pair or use an existing one.
     - Configure network settings:
       - Create a security group allowing only HTTP (port 80) or custom application ports.
       - Associate the template with the private subnets for the Application Tier.
     - Configure advanced settings as needed.
     - Launch instances within the private subnets.

2. **Launch Application Tier EC2 Instances:**
   - Launch at least two EC2 instances in the private subnets for the Application Tier.
   - Verify that these instances are not publicly accessible, and only the Web Tier can communicate with them.

### Database Tier

1. **Launch RDS Instance:**
   - In the RDS dashboard, click "Create Database."
   - Choose a database engine (e.g., MySQL, PostgreSQL).
   - Select the instance type (e.g., `db.t2.micro`).
   - Select your private subnets for the Database Tier.
   - Configure the database settings (e.g., database name, master username, password).
   - Ensure the security group allows inbound access only from the Application Tier.
   - Launch the RDS instance and wait for it to become available.

2. **Configure Security Groups:**
   - For the Web Tier, ensure the security group allows inbound HTTP (port 80) and SSH (port 22).
   - For the Application Tier, configure security groups to allow traffic from the Web Tier (port 80 or custom application port).
   - For the Database Tier, configure security groups to allow traffic from the Application Tier.

## Verifying Connectivity

1. **Test Web Tier:**
   - Once the EC2 instances for the Web Tier are launched, verify that you can access the web application by entering the public IP address in a browser.
   - You should see the Apache web server default page or your custom application.

2. **Test Application Tier:**
   - Use SSH to connect to one of the EC2 instances in the Application Tier (private subnet).
   - Verify that the application is running and can connect to the database.

3. **Test Database Connectivity:**
   - Connect to the RDS instance from one of the Application Tier instances.
   - Ensure the database is accessible and that the application can query the database as needed.

4. **Test Full Connectivity:**
   - Ensure that the Web Tier can communicate with the Application Tier, and the Application Tier can connect to the Database Tier.
   - Test the overall flow of the application from the web interface down to the database.

## Conclusion

You have successfully set up a 3-tier architecture on AWS, with a Web Tier, Application Tier, and Database Tier. This architecture ensures scalability, high availability, and security by isolating each tier in different subnets and utilizing best practices for routing and security. 

For continuous improvement, consider adding features like Auto Scaling, Load Balancers, and Multi-AZ deployments to further enhance the resilience and performance of your infrastructure.

 
