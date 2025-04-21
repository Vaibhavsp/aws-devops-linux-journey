# 📦 EC2 Reserved Instance – Hands-on Guide

### 📝 Objective:
Purchase a Reserved Instance to reduce long-term EC2 costs without changing your existing infrastructure.

---

## ✅ Steps:

### 1. Go to EC2 Dashboard
- Navigate to **EC2 > Reserved Instances**

![1](https://github.com/user-attachments/assets/5612be55-e90b-482d-965c-0be101a1f81f)

### 2. Click on “Purchase Reserved Instances”

![2](https://github.com/user-attachments/assets/2371bdbd-36f3-4da0-b258-df2c6861b7f0)

### 3. Define Your Purchase:
- Platform: **Linux/UNIX**
- Instance Type: e.g., **t3.micro**
- Tenancy: **Shared**
- Term: **1 Year or 3 Years**
- Offering Class: **Standard** (higher discount) or **Convertible** (flexible)

![3](https://github.com/user-attachments/assets/27fc5fae-30f0-49ae-8a18-1b513adf0197)

### 4. Select Availability Zone
- Choose the same AZ as your existing instances (optional but better utilization)

### 5. Payment Option
- All Upfront / Partial Upfront / No Upfront

### 6. Review & Purchase
- Confirm the selection
- Purchase Reserved Instance

![4](https://github.com/user-attachments/assets/3ec7733b-38c5-479f-b7cc-a233b650ea7c)

---

## 🧪 Test/Validate:
- Match running EC2 instance to RI configuration
- Go to **EC2 > Instances**, see if **“Reserved” pricing applied** under billing column

---

## 📌 Notes:
- You don’t need to launch a new EC2 instance
- It applies automatically to any matching instance you launch
- Best for steady state workloads

---

## 🎯 Real-World Use Case:
Ideal for:
- Web servers with predictable load
- Database instances with constant uptime
- Long-term dev/staging servers
