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
- **Terraform (Optional):** For infrastructure as code, consider using Terraform to define and provision AWS resources. [Learn more about Terraform](https://www.terraform.io/).

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
     -
::contentReference[oaicite:0]{index=0}
 
