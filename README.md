# **AWS CloudFormation Advanced Homework – Week 6**

## **📌 Objective**  
This repository provides an end-to-end **CloudFormation deployment exercise** for experienced IT professionals. 

You will build a **scalable, secure, and event-driven AWS infrastructure** that includes:
✅ **Networking**: VPC, Subnets, NAT Gateway, Route Tables  
✅ **Security**: Security Groups, NACLs, IAM roles  
✅ **Compute**: API Gateway, Lambda, ECS Fargate, Auto Scaling  
✅ **Database**: DynamoDB, RDS  
✅ **Messaging**: SQS, SNS for asynchronous processing  
✅ **Monitoring**: CloudWatch Logs, Alarms, Metrics  

---

## **📂 Repository Structure**
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

---

## **🔹 Exercise 1: Networking (VPC, Subnets, NAT)**
📍 **Goal:** Deploy a **VPC with public/private subnets** and a **NAT Gateway** for secure outbound access.

📌 **Tasks**  
1. Create a **VPC (10.0.0.0/16)**  
2. Create **2 public and 2 private subnets** across **two availability zones**  
3. Deploy a **NAT Gateway** in a **public subnet**  
4. Attach an **Internet Gateway** to the **VPC**  
5. Configure **Route Tables**:
   - Public subnets route to the Internet Gateway
   - Private subnets route through the NAT Gateway  

📄 **Instructions:** Modify `exercises/01-networking/networking.yaml` and deploy it with:  
```sh
aws cloudformation create-stack --stack-name networking-stack \
  --template-body file://exercises/01-networking/networking.yaml
```
✅ **Validation**:  
Run:  
```sh
aws ec2 describe-vpcs
aws ec2 describe-subnets
aws ec2 describe-route-tables
```
Ensure subnets and route tables exist as expected.

---

## **🔹 Exercise 2: Security (Security Groups, NACLs, IAM)**
📍 **Goal:** Implement **Security Groups, NACLs, and IAM roles** for secure access control.

📌 **Tasks**  
1. Create a **Security Group for EC2/Fargate**:
   - Allow **HTTP (80, 443)** from the internet  
   - Allow **SSH (22) only from your IP**  
2. Create a **Security Group for RDS**:
   - Allow **only EC2/Fargate instances** to connect  
3. Create **NACL rules**:
   - Allow inbound **HTTP, HTTPS** from the internet  
   - Block **unauthorized IPs**  
4. Create **IAM Role & Policy** for EC2 and Lambda  

📄 **Instructions:** Modify `exercises/02-security/security.yaml` and deploy it:  
```sh
aws cloudformation create-stack --stack-name security-stack \
  --template-body file://exercises/02-security/security.yaml
```
✅ **Validation**:  
Check:
```sh
aws ec2 describe-security-groups
aws ec2 describe-network-acls
aws iam list-roles
```

---

## **🔹 Exercise 3-6: Compute, Database, Messaging, Monitoring**
Follow similar steps for:
- **Compute (Lambda, Fargate, Auto Scaling)**  
- **Database (DynamoDB, RDS)**  
- **Messaging (SQS, SNS, Event-Driven Processing)**  
- **Monitoring (CloudWatch, Logging, Alarms)**  

---

## **📩 Submission Instructions**
1. **Fork the GitHub repo** and create a branch.  
2. Push your completed CloudFormation templates to `answers/`.  
3. Open a **Pull Request (PR)** with a **README** explaining what you built.  
4. Share the **CloudFormation Stack Names** and **outputs** in the PR description.  

---

## **🚀 Bonus Challenges**
🔹 **Use StackSets to deploy resources across multiple regions**  
🔹 **Integrate AWS CodePipeline to automate CloudFormation deployments**  
🔹 **Deploy a multi-tier architecture using Nested Stacks**  

🎯 **Goal:** By completing this, you will **master AWS CloudFormation** and **deploy full-stack cloud applications like a pro!** 🚀
