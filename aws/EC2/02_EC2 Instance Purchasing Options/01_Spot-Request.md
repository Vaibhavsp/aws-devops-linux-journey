# ☁️ EC2 Spot Instance Request – Hands-on Guide

### 📝 Objective:
Launch a Spot EC2 instance using AWS Console and test its behavior.

---

## ✅ Steps:

### 1. Go to EC2 Dashboard
- Navigate to **EC2 > Instances > Launch Instance**

![1](https://github.com/user-attachments/assets/e6f0189e-c75a-4c87-a040-d02c5122964b)

![2](https://github.com/user-attachments/assets/87e3bc1b-2b5c-4fa6-9a7d-35be92678108)

### 2. Choose AMI & Instance Type
- AMI: **Amazon Linux 2023**
- Instance Type: **t3.micro** (or any free tier)

![3](https://github.com/user-attachments/assets/23671142-be79-4d75-a0bb-4baba63fd4b1)

![4](https://github.com/user-attachments/assets/a4aab0cf-24a9-43f5-b703-d701b11ed049)


### 3. Configure Purchase Options
- Expand **Advanced Details**
- Under **Purchase Options**:
  - ✅ Tick **Request Spot Instances**
  - Choose **Interruption Behavior**: Stop / Terminate

![5](https://github.com/user-attachments/assets/ddc86d72-40f7-4a65-a15c-d927ef728ca1)

### 4. Configure Storage & Networking
- Keep default or add storage
- Add to existing VPC / subnet

![6](https://github.com/user-attachments/assets/d8ccce07-5c62-4171-97c8-31b4a4eee401)

![7](https://github.com/user-attachments/assets/75cd7916-229d-4ad3-9284-f32c2eb6b594)

### 5. Configure Security Group
- Add rules:
  - SSH (port 22) – My IP
  - HTTP (port 80) – Anywhere (optional)

### 6. Review and Launch
- Select existing key pair or create a new one
- Launch the instance

![8](https://github.com/user-attachments/assets/63f6d4bf-d832-4336-b253-d7586519bd94)

![10](https://github.com/user-attachments/assets/4dcbd553-e676-4f49-8395-9df2240f686f)

![9](https://github.com/user-attachments/assets/bf823234-73d8-418d-b1df-0a2c0431e3ba)


---

## 📸 Screenshots to Capture:
- ✅ Spot Instance checkbox enabled
- ✅ Interruption Behavior option
- ✅ Instance launched with **"Lifecycle: spot"**

---

## 🧪 Test:
1. SSH into the instance
2. Try manually stopping the instance → See if it's stopped or terminated
3. Monitor EC2 dashboard for pricing, state

---

## 📌 Notes:
- Spot instances may be terminated by AWS anytime
- Cheapest compute option for fault-tolerant or flexible tasks

---

## 🎯 Real-World Use Case:
Ideal for:
- Batch jobs
- Image processing
- Auto-scaling fleets where cost is critical
