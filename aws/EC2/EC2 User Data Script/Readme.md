# 🚀 Automate EC2 Setup with User Data – Hands-On + Troubleshooting Guide

Setting up an EC2 instance manually every time?  
There’s a better way — automate everything using **User Data scripts** at launch time!

In this blog, let’s dive into how to:
- Write and attach a working **User Data script**
- Set up a **web server on EC2**
- **Troubleshoot** common issues like: *“This site can’t be reached”*

---

## 🔍 What is EC2 User Data?

**User Data** is a special script you provide while launching an EC2 instance.  
It runs automatically the **first time the instance boots** and is usually used for:
- Installing packages (e.g., Apache)
- Setting up files, configurations
- Launching services

---

## 🧸 Step-by-Step Setup Guide

### ✅ Step 1: Create Your Script

Use this simple script to install Apache and deploy a basic HTML page.

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello from EC2 User Data!</h1>" > /var/www/html/index.html
```

This script is for **Amazon Linux 2**. If you're using **Ubuntu**, modify it like this:

```bash
#!/bin/bash
apt update -y
apt install apache2 -y
systemctl start apache2
systemctl enable apache2
echo "<h1>Hello from Ubuntu EC2!</h1>" > /var/www/html/index.html
```

---

### ✅ Step 2: Launch EC2 Instance with User Data

1. Go to **EC2 > Launch Instance**
![1](https://github.com/user-attachments/assets/f4e2b6cb-4849-443f-b1f6-b396a164ea75)

![2](https://github.com/user-attachments/assets/d3daa5ef-0ea3-448e-89ab-dd455f689d55)

2. Choose **Amazon Linux 2 AMI**
![3 1](https://github.com/user-attachments/assets/ee2523be-9be8-4016-bf95-9deddfe0ebb2)

3. Choose instance type: `t2.micro` (free tier)
![3 2](https://github.com/user-attachments/assets/1c7d6872-5816-4177-839c-e15cc86a6160)

4. Under **Advanced Details**, paste your **User Data** script
![3 6](https://github.com/user-attachments/assets/f4a27111-cf77-40ec-8148-2fbaf76ca3ab)

![3 7](https://github.com/user-attachments/assets/777f79ca-b4ff-41df-bd41-445f59d0f61b)


5. Configure Security Group:
   - Allow **HTTP (port 80)**
   - Optional: allow SSH (port 22)
![3 4](https://github.com/user-attachments/assets/30ca8473-64aa-4f87-918c-ba60964ecb6c)

6. Launch with your existing or new key pair
![4](https://github.com/user-attachments/assets/f7483e42-f2c7-49ab-b188-0a60ccc4217b)

![6](https://github.com/user-attachments/assets/ddd16a14-2bc5-46fd-8862-0669abd9aa65)

---

### ✅ Step 3: Access Your Site

After the instance is running:

- Go to **Instance Details**
- Copy **Public IPv4 address**
- Open browser and visit:  
  `http://<your-public-ip>`
![8](https://github.com/user-attachments/assets/39e60154-e0a0-4067-a8a5-17479dfddbba)

You should see the **HTML page from your script!**

---

## 🛠 Troubleshooting Guide

Got the dreaded error?  
**“This site can’t be reached”**  
Let’s fix it. Here are the most common issues:

---

### 1. Apache Service Didn’t Start

SSH into your instance and run:

```bash
sudo systemctl status httpd    # Amazon Linux
sudo systemctl status apache2  # Ubuntu
```

If it's not running:

```bash
sudo systemctl start httpd
```

---

### 2. Port 80 Not Allowed in Security Group

Check your **Inbound Rules**:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| HTTP | TCP | 80 | 0.0.0.0/0 |
| SSH  | TCP | 22 | Your IP |

Update if needed via **EC2 > Security Groups**

---

### 3. User Data Didn’t Run

Connect via SSH and check logs:

```bash
sudo cat /var/log/cloud-init-output.log
sudo cat /var/log/cloud-init.log
```

You should see your script's output here.  
If it failed, fix the script and re-launch a new instance.

---

### ↺ Re-run User Data (Optional)

By default, User Data runs only once.  
To re-run on reboot:

```bash
sudo rm -rf /var/lib/cloud/instances/*
sudo cloud-init clean
sudo reboot
```

---

## 📆 Summary Table

| Task | Command |
|------|---------|
| Check Apache | `sudo systemctl status httpd` |
| View Logs | `cat /var/log/cloud-init-output.log` |
| Check Port 80 | Inbound Rules → HTTP → Port 80 |
| Test Web | `http://<Public-IP>` |

---

## 🧠 Final Thoughts

This hands-on may look simple, but it’s a **core DevOps skill**.  
Using EC2 + User Data helps you build **repeatable, automated infrastructure**.

This is the same method used to:
- Auto-deploy web servers
- Pre-install agents/software
- Run bootstrap automation at scale

---

## 🔗 Resources

- [My GitHub Repo](https://github.com/Vaibhavsp/aws-devops-linux-journey)
- [My Medium Blog](https://medium.com/@vaibhavparekh097)
- [AWS Docs – EC2 User Data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)
