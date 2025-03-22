## **Bonus Task 2: Multi-Tier Architecture with Nested Stacks**

## **📌 Objective**
Use **Nested Stacks** to break down large CloudFormation templates into modular, reusable components.

---

## **🔹 Why Use Nested Stacks?**
✅ **Modularity** – Break complex infrastructure into smaller, manageable stacks.
✅ **Reusability** – Define templates that can be reused across projects.
✅ **Scalability** – Update individual components without redeploying the entire infrastructure.

---

## **🔹 How Nested Stacks Work**
1️⃣ **Parent Stack** – The main CloudFormation template that references other stacks.
2️⃣ **Child Stacks** – Independent stacks deployed by the parent stack.
3️⃣ **Nested Stack Calls** – The parent stack invokes child stacks using the `AWS::CloudFormation::Stack` resource.

---

## **🛠 Steps to Implement Nested Stacks**
### **1️⃣ Write a Parent Stack Template**
Modify `exercises/08-bonus-nestedstacks/parent-stack.yaml` to define the main application stack.

### **2️⃣ Define Child Stack Templates**
Inside `exercises/08-bonus-nestedstacks/`, create:
- `network-stack.yaml` – Defines VPC, Subnets, and Route Tables.
- `compute-stack.yaml` – Deploys EC2, ECS, or Lambda.
- `database-stack.yaml` – Provisions RDS or DynamoDB.

### **3️⃣ Link Nested Stacks in the Parent Stack**
In `parent-stack.yaml`, reference the child stacks:
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

### **4️⃣ Deploy the Parent Stack**
Run the following AWS CLI command:
```sh
aws cloudformation create-stack --stack-name MultiTierArchitecture \
  --template-body file://parent-stack.yaml \
  --capabilities CAPABILITY_NAMED_IAM
```

### **5️⃣ Validate Nested Stack Deployment**
Check stack creation logs:
```sh
aws cloudformation describe-stacks --stack-name MultiTierArchitecture
```

---