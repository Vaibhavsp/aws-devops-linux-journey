# 📚 AWS VPC + EC2 + SG + NACL Full Practical Hands-on (Detailed)

---

## 🚀 What We Did:

A fully practical AWS Networking exercise covering VPC creation, EC2 launch, configuring Security Groups, modifying NACLs, and observing real-time impact on web server access.

---

## 🧠 Hands-on Detailed Steps:

---

## 1. Create a Custom VPC

### • Navigate to AWS Console → Search for **VPC** → Open **VPC Dashboard**.

![AWS Console](https://github.com/user-attachments/assets/d5831ced-a5dc-47fd-b263-34e11daabadb)
  
![VPC Dashboard](https://github.com/user-attachments/assets/25ef50b7-a3ac-4ab9-888d-c32419c2bc33)

### • Click **Create VPC**.

![Create VPC](https://github.com/user-attachments/assets/19f7ed9a-d457-4a7c-863e-64ab22a5408b)

### • Choose "**VPC and more**" option.

![VPC and more](https://github.com/user-attachments/assets/b8ca4b96-dbea-40ee-ab0b-df2b68db5646)

### • Set:
  - **Name Tag**: `demo`
  - **IPv4 CIDR block**: `10.0.0.0/16`
### • Preview flowchart (optional but helps visualization).

![flowchart](https://github.com/user-attachments/assets/747e5120-0fa9-497e-bc52-fda6ef93b4d0)

### • Click **Create VPC**.
### • VPC creation confirmation received.

![VPC Created](https://github.com/user-attachments/assets/e0456170-3a45-4ff0-b944-1aeb457cf8d6)


### ✅ *Custom VPC created successfully.*

---

## 2. Launch an EC2 Instance inside the VPC

### • Open **EC2 Console**.
### • Click **Launch Instance**.
### • **OS Image Selected**: Ubuntu (Free tier eligible).

![8](https://github.com/user-attachments/assets/e9bb1eeb-1de1-462d-aab3-a9ee93b075aa)

### • Under **Network Settings**:
  - Choose the VPC created above (`demo`).
  - Choose an available **Public Subnet** inside VPC.

![9](https://github.com/user-attachments/assets/3e96d548-d224-44b2-a4d5-2b1de59dcc17)

### • **Launch** the instance.

![Launch Instance](https://github.com/user-attachments/assets/4454cbad-7123-4038-9ce3-033841c7fccb)

### ✅ *EC2 instance created inside custom VPC and public subnet.*

---

## 3. Connect to EC2 via SSH

### • Connect to the EC2 instance using SSH:
  ```bash
  ssh -i your-key.pem ubuntu@<Public-IP>
  ```
  
![Connect via SSH](https://github.com/user-attachments/assets/3f5da6d9-f762-49ee-9257-3869b15a49af)

### ✅ *SSH connection established.*

---

## 4. Setup Python Web Server on EC2

### • Update packages inside EC2:
  ```bash
  sudo apt update -y
  ```

![Update packages](https://github.com/user-attachments/assets/d298a908-6c56-4e2f-bcce-6deeecf6111e)

### • Start a simple HTTP server using Python:
  ```bash
  python3 -m http.server 8000
  ```

![Start HTTP](https://github.com/user-attachments/assets/6fec9dc3-d659-4a3a-b901-47909bcbf1f4)

### • This runs a web server on **port 8000**.

### ✅ *Web server running inside EC2 instance.*

---

## 5. Modify Security Group to Allow Port 8000

### • Go to **EC2 Dashboard** → Select running instance.

![Assign SG](https://github.com/user-attachments/assets/f18ba88e-6340-4fb2-bfcb-f566739fa11d)

### • Under **Security** → Click **Security Groups** → Edit **Inbound Rules**.
### • Add a new inbound rule:
  - **Type**: Custom TCP
  - **Port Range**: 8000
  - **Source**: Anywhere (0.0.0.0/0)
  
![Add a new inbound rule](https://github.com/user-attachments/assets/338a65df-312d-485d-aa9f-67c8a5b13454)

### • Click **Save**.

### ✅ *Port 8000 traffic now allowed at Security Group level.*

---

## 6. Access the Web Server

### • Copy the **Public IP** of the EC2 instance.
### • Open browser and visit:
  ```
  http://<Public-IP>:8000
  ```
  Example:  
  ```
  http://65.0.102.160:8000
  ```

![Access the Web Server](https://github.com/user-attachments/assets/365cfd4d-6cad-4619-badc-fc14cb67d6f7)


### ✅ *Web Page now live and accessible over internet!*

### • Also, observe incoming HTTP requests reflected on SSH console where Python server is running.

![Reflection of HTTP Server in Python](https://github.com/user-attachments/assets/a564fcd1-4b7f-4365-94b6-1f4b8ed0de7f)

---

## 7. Modify Network ACL to Deny and Allow Traffic Dynamically

## 7.1 Deny Access via NACL
### • Go to **VPC Dashboard** → **Network ACLs**.

![NACL](https://github.com/user-attachments/assets/8fe395ed-a557-4306-b520-04396f8cbc78)

### • Find the NACL associated with the Public Subnet.

![19](https://github.com/user-attachments/assets/e2e19e1d-a8aa-419d-b645-998b36a8477e)

### • Edit **Inbound Rules**:

![20](https://github.com/user-attachments/assets/6e02792d-210f-4e44-b139-23b199022b63)

  ### • Remove existing rules if necessary.

![Remove existing rule](https://github.com/user-attachments/assets/681ace8e-864c-4a93-9325-420273b3e348)

 ### Add new **Inbound Rule**:
      - Rule No: `100`
      - Type: Custom TCP
      - Port: `8000`
      - Source: `0.0.0.0/0`
      - Action: **DENY**
  
![Add new Rule](https://github.com/user-attachments/assets/4fcbea4c-14d8-4d39-9ac1-b9e532f49f3e)
    
![Configure the properties](https://github.com/user-attachments/assets/47f46850-396e-4499-afcd-a281e9c12671)

### • Save the NACL.

![NACL Created and Properties Applied](https://github.com/user-attachments/assets/90b7c627-8e31-4cc7-a5b9-c0b0313a348d)


### ✅ *Now the webpage (`http://Public-IP:8000`) will stop working.*  
(Error: *This site can’t be reached*)

![Web Page with no output](https://github.com/user-attachments/assets/ebf614e0-e291-4773-bea3-a18ca2ca8d78)

---

### 7.2 Allow Access Again via New NACL Rule

### • Edit Inbound Rules again:

  ![Edit Inbound Rules again](https://github.com/user-attachments/assets/239904c0-4a9f-44e6-a37e-6ec01775af0c)

### • Add another new rule:
  - Rule No: `100 & 200`
  - Type: Custom TCP
  - Port: `8000` for Rule no `200`
  - Source: `0.0.0.0/0`
  - Action: **ALLOW for Rule no `100`** **Deny for for Rule no `200`**
### • Save changes.

![27](https://github.com/user-attachments/assets/e46cb1cc-f63c-4ef8-acb0-8ad04150fb43)

### ✅ *Now the webpage starts working again!*  
(NACL processes rules in ascending rule number order.)

![Webpage starts working](https://github.com/user-attachments/assets/ce1e460e-5086-4b6a-824d-68813f3a87b9)

---

### 7.3 Play with Rule Priority
### • Change rule numbers:
  • Make the DENY rule number smaller (e.g., 50).

![Reverse the Permission](https://github.com/user-attachments/assets/803e0a40-5f72-40b2-8df4-8dec7858fd1c)

![31](https://github.com/user-attachments/assets/25a9d009-459b-43d5-b8b7-fc5f6600fb0a)

### • Result:
  • Web access blocked again — because first matching rule (DENY) gets applied.

![31](https://github.com/user-attachments/assets/da838626-bc66-4fd3-8bf9-6ba341b7cbfd)

### ✅ *Demonstrated NACL working based on ascending rule numbers!*

---

## 🔥 Final Observations:

| Layer | Control |
|:-----:|:-------:|
| VPC | Network boundary |
| EC2 | Hosting workload |
| SG (Security Group) | Instance level access control (Stateful) |
| NACL (Network ACL) | Subnet level access control (Stateless) |


---

## 🔗 Useful Links:

- [GitHub Repo - AWS Journey](https://github.com/Vaibhavsp/aws-devops-linux-journey)
- [My Medium Blog](https://medium.com/@vaibhavparekh097)
- [LinkedIn](https://www.linkedin.com/in/vaibhav-parekh08/)
- [X](https://x.com/awswithvibes)

---
