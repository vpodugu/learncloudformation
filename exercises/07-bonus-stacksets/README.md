# **Bonus Task 1: Using StackSets for Multi-Region Deployment**

## **📌 Objective**
Learn how to deploy AWS resources across multiple regions using **AWS CloudFormation StackSets**. This ensures **scalability, fault tolerance, and disaster recovery** by automatically replicating stacks across AWS regions.

---

## **🔹 Why Use StackSets?**
✅ **Multi-Region Consistency** – Ensures the same infrastructure is available across multiple AWS regions.
✅ **Centralized Management** – Manage all deployments from a single CloudFormation template.
✅ **Automatic Scaling** – If new regions are added, StackSets can automatically provision resources there.
✅ **Disaster Recovery** – Deploying infrastructure in different AWS regions provides resilience against regional failures.

---

## **🔹 How StackSets Work**
1️⃣ **Create a StackSet** – Define your CloudFormation template and specify the AWS accounts and regions to deploy to.
2️⃣ **Deploy to Target Accounts & Regions** – StackSets create stacks in each specified region automatically.
3️⃣ **Manage and Update** – Apply updates centrally and propagate them to all stack instances.

---

## **🛠 Steps to Implement StackSets**
### **1️⃣ Prerequisites**
- **Administrator permissions** to create StackSets.
- AWS CLI or AWS Console access.
- An IAM role with `AWSCloudFormationStackSetAdministrationRole` and `AWSCloudFormationStackSetExecutionRole` permissions.

### **2️⃣ Create an IAM Role for StackSet Execution**
You need an execution role in each target account to allow StackSets to create stacks.

### **3️⃣ Write a StackSet CloudFormation Template**
Modify `exercises/07-bonus-stacksets/stackset-template.yaml` to define the resources.

### **4️⃣ Deploy the StackSet**
Run the following AWS CLI command:
```sh
aws cloudformation create-stack-set --stack-set-name MultiRegionDeployment \
  --template-body file://stackset-template.yaml \
  --capabilities CAPABILITY_NAMED_IAM
```

### **5️⃣ Add Stack Instances to Multiple Regions**
```sh
aws cloudformation create-stack-instances --stack-set-name MultiRegionDeployment \
  --accounts 123456789012 \
  --regions us-east-1 us-west-1 eu-central-1
```

### **6️⃣ Validate Deployment**
Run:
```sh
aws cloudformation describe-stacks --stack-name MultiRegionDeployment
```
Ensure all instances are successfully deployed in the specified regions.

---