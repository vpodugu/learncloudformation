# AWS CloudFormation Advanced Homework – Week 6

## Overview
This repository contains a comprehensive set of CloudFormation deployment exercises designed for experienced IT professionals. You'll build a complete AWS infrastructure that's scalable, secure, and event-driven.

## What You'll Build
- **Networking**: VPC, Subnets, NAT Gateway, Route Tables
- **Security**: Security Groups, NACLs, IAM roles
- **Compute**: API Gateway, Lambda, ECS Fargate, Auto Scaling
- **Database**: DynamoDB, RDS
- **Messaging**: SQS, SNS for asynchronous processing
- **Monitoring**: CloudWatch Logs, Alarms, Metrics

## Repository Structure
```
cloudformation-homework/
│── exercises/
│   ├── 01-networking/        # Task 1: VPC, Subnets, NAT, Security
│   ├── 02-security/          # Task 2: Security Groups, NACLs, IAM Roles
│   ├── 03-compute/           # Task 3: Fargate, Lambda, Auto Scaling
│   ├── 04-database/          # Task 4: DynamoDB, RDS, IAM policies
│   ├── 05-messaging/         # Task 5: SQS, SNS, Event-driven architecture
│   ├── 06-monitoring/        # Task 6: CloudWatch, Logging, Alarms
│── answers/
│   ├── 01-networking.yaml
│   ├── 02-security.yaml
│   ├── 03-compute.yaml
│   ├── 04-database.yaml
│   ├── 05-messaging.yaml
│   ├── 06-monitoring.yaml
│── README.md                 # Instructions for each exercise
```

## Exercise 1: Networking (VPC, Subnets, NAT)
**Goal:** Set up a VPC with public and private subnets, including a NAT Gateway for secure outbound access.

**Tasks**
1. Create a VPC with CIDR block 10.0.0.0/16
2. Set up 2 public and 2 private subnets across two availability zones
3. Deploy a NAT Gateway in a public subnet
4. Attach an Internet Gateway to the VPC
5. Configure Route Tables:
   - Public subnets route to the Internet Gateway
   - Private subnets route through the NAT Gateway

**Instructions:** Modify `exercises/01-networking/networking.yaml` and deploy it with:
```sh
aws cloudformation create-stack --stack-name networking-stack \
  --template-body file://exercises/01-networking/networking.yaml
```

**Validation:**
Run these commands to verify your setup:
```sh
aws ec2 describe-vpcs
aws ec2 describe-subnets
aws ec2 describe-route-tables
```
Check that your subnets and route tables are configured correctly.

## Exercise 2: Security (Security Groups, NACLs, IAM)
**Goal:** Implement security controls using Security Groups, NACLs, and IAM roles.

**Tasks**
1. Create a Security Group for EC2/Fargate:
   - Allow HTTP (80, 443) from the internet
   - Allow SSH (22) only from your IP
2. Create a Security Group for RDS:
   - Allow connections only from EC2/Fargate instances
3. Set up NACL rules:
   - Allow inbound HTTP, HTTPS from the internet
   - Block unauthorized IPs
4. Create IAM Role & Policy for EC2 and Lambda

**Instructions:** Modify `exercises/02-security/security.yaml` and deploy it:
```sh
aws cloudformation create-stack --stack-name security-stack \
  --template-body file://exercises/02-security/security.yaml
```

**Validation:**
Verify your security setup with:
```sh
aws ec2 describe-security-groups
aws ec2 describe-network-acls
aws iam list-roles
```

## Exercise 3-6: Compute, Database, Messaging, Monitoring
Continue with the remaining exercises:
- Compute (Lambda, Fargate, Auto Scaling)
- Database (DynamoDB, RDS)
- Messaging (SQS, SNS, Event-Driven Processing)
- Monitoring (CloudWatch, Logging, Alarms)

## Bonus Challenges
- Use StackSets to deploy resources across multiple regions
- Deploy a multi-tier architecture using Nested Stacks

By completing these exercises, you'll gain hands-on experience with AWS CloudFormation and learn how to deploy full-stack cloud applications effectively.
