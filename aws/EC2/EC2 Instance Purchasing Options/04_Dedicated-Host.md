# 🏢 EC2 Dedicated Host – Hands-on Guide

### 📝 Objective:
Allocate a dedicated host in AWS and launch an EC2 instance tied specifically to that physical host.

---

## ✅ Steps:

### 1. Go to EC2 Dashboard
- Navigate to **EC2 > Dedicated Hosts**

![1](https://github.com/user-attachments/assets/b4845365-c843-483d-b9ba-84387df5b847)

### 2. Allocate Dedicated Host
- Click **Allocate Host**
- Select:
  - Instance Family: e.g., **t3**
  - Availability Zone (e.g., `ap-south-1a`)
  - Quantity: 1
  - Auto Placement: Optional (Off by default)
- Click **Allocate**

![2](https://github.com/user-attachments/assets/0248bd83-319c-44c9-9c91-2422bf1b4db9)

### 3. Launch EC2 Instance on Host
- Go to **Launch Instance** wizard
- AMI: Amazon Linux 2023
- Instance Type: e.g., **t3.medium** (match host family)
- Under **Tenancy**, choose:
  - **Dedicated Host**
- Select the allocated host ID (from earlier)
- Add key pair, storage, and launch

![3](https://github.com/user-attachments/assets/e74dd169-6274-4a40-8065-b7c422e19c87)

![4](https://github.com/user-attachments/assets/dc29aa64-3b88-493f-96d5-f0f346bd8ba4)

---

## 🧪 Test/Validate:
- Go to **EC2 > Instances > Details**
- Confirm Host ID is showing
- Cross-check in Dedicated Hosts tab — instance should be listed

---

## 📌 Notes:
- Dedicated Host = Physical server exclusively yours
- Enables licensing for Windows/Oracle
- Costlier, but for regulatory/security needs

---

## 🎯 Real-World Use Case:
Ideal for:
- Regulated industries (banking, healthcare)
- BYOL licensing for MS SQL/Oracle
- Physical server placement control
