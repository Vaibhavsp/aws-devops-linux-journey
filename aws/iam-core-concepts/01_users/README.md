# IAM Users – AWS Identity and Access Management (IAM)

## 📘 What is an IAM User?
An **IAM User** is an entity created in AWS to represent a single person or application that interacts with AWS resources.

Each user:
- Has a unique name within the AWS account
- Can be given **permissions via policies**
- Can have **programmatic access** (CLI, SDKs) and/or **console access** (Web UI)

---

## ❓ Why Use IAM Users?
- To follow the **principle of least privilege**  
- Avoid using the **root user** for everyday tasks  
- Assign access **per user** and **track activity individually**

---

## ⚙️ How IAM Users Work:
- Each IAM user is part of **one AWS account**
- They are assigned:
  - **Policies** to control access
  - **Groups** (optional) for permissions inheritance
  - **Access keys** for CLI/API access
  - **MFA** for extra security

---

## 🧠 Key Points:
- You cannot assign a user to multiple AWS accounts.
- A user can have **password** and/or **access keys**.
- You can assign custom permissions using **JSON policies**.

---

## 📁 Related Files in This Folder:
- `cli-commands.md` – Full CLI hands-on
- `gui-steps.md` – AWS Console step-by-step
- `json-policies/` – Sample custom policies
- `interview.md` – Interview and certification Q&A
