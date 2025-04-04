# 🛠️ IAM Roles – Hands-On Practice (GUI + CLI)

---

## 📌 Goal:
Create an IAM Role for an **EC2 Instance** that allows it to access **S3**.

---

## ✅ PART 1: IAM ROLE CREATION USING GUI

### 🎯 Objective:
Create a role named `EC2S3AccessRole` that grants S3 read access to EC2 instances.

---

### 🔸 Step-by-Step (AWS Console):

1. **Login to AWS Console** → Go to **IAM** → **Roles**
2. Click **Create role**
3. **Select trusted entity**:
   - Choose **AWS service**
   - Use case: Select **EC2**
   - Click **Next**
4. **Attach policies**:
   - Search and select **AmazonS3ReadOnlyAccess**
   - Click **Next**
5. **Role name**: `EC2S3AccessRole`
   - (Optional) Add a description: “Allows EC2 instances to read from S3”
6. **Review and Create Role**
   - Click **Create role**

---

### 🔍 Attach Role to EC2 Instance:

1. Go to **EC2 Console**
2. Select an EC2 instance → **Actions** → **Security** → **Modify IAM Role**
3. Choose `EC2S3AccessRole` and click **Update IAM role**

---

## ✅ PART 2: IAM ROLE CREATION USING CLI

### 🔧 Prerequisites:
- AWS CLI installed and configured with proper IAM access
- Use RedHat/CentOS/Ubuntu terminal

---
