# 🌐 Elastic IP (EIP) – Hands-on Tutorial

### 📝 Objective:
Allocate and associate an Elastic IP to an EC2 instance, and understand its reassociation and static nature.

---

## ✅ What is Elastic IP?
Elastic IP is a **static, public IPv4 address** that you can allocate and associate with your EC2 instance. Unlike a default public IP (which changes on stop/start), an EIP remains the same until released.

---

## ✅ Use Case:
- Required when you want a **permanent public IP**
- Useful for **DNS mapping** or **application endpoints**
- Ensures consistent access even if the instance is restarted

---

## 🚀 Steps to Allocate & Associate Elastic IP
### Prerequisite:
- Run an **EC2 instance**

![image](https://github.com/user-attachments/assets/8b15c1ea-7c73-497d-b0bd-8bcf325a475f)

### 1. Allocate a New Elastic IP
- Go to **EC2 Dashboard → Network & Security → Elastic IPs**

![image](https://github.com/user-attachments/assets/77e716ba-c238-4d78-9151-e7df8aabcade)

- Click **“Allocate Elastic IP address”**

![image](https://github.com/user-attachments/assets/1844ce8f-81ad-4e86-b3f9-56d71821351e)

- Choose **Amazon’s pool of IPv4 addresses**

![image](https://github.com/user-attachments/assets/ec81de75-0ccb-4d33-8b26-2239fe3c88a1)

- Click **Allocate**

![image](https://github.com/user-attachments/assets/819e35b0-3cd0-41cb-ad0e-c1acd4545055)

---

### 2. Associate Elastic IP with EC2 Instance
- Select the EIP you just created
- Click **Actions → Associate Elastic IP address**

![image](https://github.com/user-attachments/assets/48b3f97d-331e-4a9d-ad4d-61b7f8969742)

- Set the following:
  - **Instance**: Select your running EC2
  - **Private IP**: Keep default (auto-selected)
  - ✅ Check **“Allow this Elastic IP address to be reassociated”**
- Click **Associate**

![image](https://github.com/user-attachments/assets/e80f6da6-c982-47a2-a6c8-4d20e4eda2d9)

![image](https://github.com/user-attachments/assets/aaa3c238-5893-49ed-8fd5-3e317d06e199)

---

### 3. Validate the Setup
- Go to EC2 > Instances > Public IPv4 → confirm EIP is attached
- Use SSH to connect via EIP:
```bash
ssh -i your-key.pem ec2-user@<your-elastic-ip>
```
- Or access hosted service (e.g., web server)

![image](https://github.com/user-attachments/assets/e3e55e4d-9d1a-4294-a585-c7bbabb2367a)

---

## 🔁 Optional: Reassociate EIP to Another Instance
- Stop current instance (optional)

![image](https://github.com/user-attachments/assets/dddf3370-eeff-4052-8c6e-43066c76e3ed)

- Go back to EIP → **Disassociate** from current instance

![image](https://github.com/user-attachments/assets/92b16f4a-6176-4afe-bf19-a488997550ad)

![image](https://github.com/user-attachments/assets/79d0680e-9b78-4d06-addf-9cca18c9f05e)

- Use **Associate** to attach it to another instance

![image](https://github.com/user-attachments/assets/35cd8e3b-b33b-4ebe-8cb5-59ff3e337955)

![image](https://github.com/user-attachments/assets/034f4973-89e8-4ac3-bb03-7758f4080c2d)

![image](https://github.com/user-attachments/assets/0ef1b75c-8872-4941-9993-4f7f06176a16)

![image](https://github.com/user-attachments/assets/7f2cd4e7-82cb-4bed-a007-a2e07b46286f)


---

## 🔍 Notes:
- AWS allows **1 free EIP per region** if associated with a running instance
- Charges apply for unused or multiple EIPs
- Helps in **high availability setup** when IP needs to stay the same across failovers

---

## 🧪 Real-World Validation
- Launch EC2 with public IP and compare behavior with/without EIP
- Try restarting instance and observe IP change (only in non-EIP case)

---

## 🎯 Real-World Use Cases:
- Hosting apps on static IPs (mapped via DNS)
- Backend API endpoints needing consistent public reach
- Failover scenarios where you can switch EIP between servers quickly

---

Now you're ready to build on top of static public access with confidence using Elastic IPs! 💪

*Happy building in the cloud!* ☁️

Medium Blog: [medium.com/@vaibhavparekh097](https://medium.com/@vaibhavparekh097)
LinkedIn: [linkedin.com/in/vaibhav-parekh08/](https://www.linkedin.com/in/vaibhav-parekh08/)
