# 💰 AWS Savings Plan – Hands-on Overview

### 📝 Objective:
Understand how to create a Savings Plan in AWS Billing and how it helps optimize EC2 costs.

---

## ✅ Steps:

### 1. Go to AWS EC2 Console

![1](https://github.com/user-attachments/assets/1c9f44e6-81d8-4a3d-aa8c-06844534a8fd)

### 2. Click on “Purchase Savings Plan”
- You’ll see two types:
  - **Compute Savings Plan** (most flexible)
  - **EC2 Instance Savings Plan** (less flexible but more savings)
  
![2](https://github.com/user-attachments/assets/7e7e04b9-8b94-4df3-a05f-07b73502b7d0)

### 3. Choose a Plan Type
- Select **Compute Savings Plan** for maximum flexibility

![3](https://github.com/user-attachments/assets/10c044bc-c4a1-439f-a9bb-3f86443f4b2e)

### 4. Set Parameters:
- Term: **1 or 3 years**
- Payment Option:
  - All upfront
  - Partial upfront
  - No upfront
- Commitment: Decide how much per hour you want to commit (e.g., $0.01/hr)

![4](https://github.com/user-attachments/assets/08d4a4b4-ac91-4d8d-92da-fed92767ff96)

### 5. Review and Confirm
- Review estimated savings
- Accept terms and complete purchase

---

## 🧪 Test/Validate:
- No deployment or launch required
- Use **Cost Explorer** to track if plan applies to running resources

---

## 📌 Notes:
- Applies **automatically** to matching EC2 instances
- Does **not require launching new instances**
- Works even for Fargate and Lambda (Compute SP)

---

## 🎯 Real-World Use Case:
Ideal for:
- Long-running workloads
- Predictable usage environments
- Startups and businesses looking to reduce EC2 bills
