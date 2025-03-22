# Multi-Tier Architecture with Nested Stacks

## Overview
In this bonus task, we'll explore how to use Nested Stacks to break down large CloudFormation templates into modular, reusable components. This approach helps manage complex infrastructure more effectively.

## Why Nested Stacks Matter
- **Modularity**: Break complex infrastructure into smaller, manageable stacks
- **Reusability**: Create templates that can be reused across different projects
- **Scalability**: Update individual components without redeploying everything

## Understanding Nested Stacks
Nested Stacks work through three main components:
1. A Parent Stack that serves as the main template
2. Child Stacks that are deployed by the parent
3. Stack references that connect everything together

## Implementation Guide

### Step 1: Create the Parent Stack
First, we'll modify `exercises/08-bonus-nestedstacks/parent-stack.yaml` to define our main application stack.

### Step 2: Set Up Child Stacks
In the `exercises/08-bonus-nestedstacks/` directory, we'll create three separate templates:
- `network-stack.yaml` for VPC, Subnets, and Route Tables
- `compute-stack.yaml` for EC2, ECS, or Lambda resources
- `database-stack.yaml` for RDS or DynamoDB

### Step 3: Connect the Stacks
In `parent-stack.yaml`, we'll reference our child stacks like this:
```yaml
Resources:
  NetworkStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: ./network-stack.yaml
      Parameters:
        VpcCIDR: "10.0.0.0/16"

  ComputeStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: ./compute-stack.yaml
      Parameters:
        InstanceType: "t3.micro"

  DatabaseStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: ./database-stack.yaml
      Parameters:
        DBEngine: "mysql"
```

### Step 4: Deploy Your Stack
Run this command to create your multi-tier architecture:
```sh
aws cloudformation create-stack --stack-name MultiTierArchitecture \
  --template-body file://parent-stack.yaml \
  --capabilities CAPABILITY_NAMED_IAM
```

### Step 5: Check the Deployment
Monitor your stack creation with:
```sh
aws cloudformation describe-stacks --stack-name MultiTierArchitecture
```
This will show you the status of both the parent and child stacks.