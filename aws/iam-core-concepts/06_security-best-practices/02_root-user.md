# 🔐 Securing the Root User in AWS

## 📘 What is the Root User?
- The **root user** is the AWS account's **original identity** created when the account was first set up.
- It has **unrestricted access** to **all resources** and **billing features**.

---

## 🚨 Why You Should Secure It
| Risk | Description |
|------|-------------|
| 🧨 Full Access | Can delete the entire account, disable security tools, or leak data. |
| 🕵️‍♂️ Attack Target | Hackers often go after root for complete control. |
| ❌ Not Auditable | Actions performed by root are harder to delegate or trace. |

---

## 🛡️ How to Secure the Root User (Step-by-Step)

### ✅ Step 1: Enable MFA on Root User
1. Log in to AWS Console using root account.
2. Go to: **IAM → Users → Root user → Enable MFA**
3. Use an MFA app like **Google Authenticator** or **Authy** to scan QR code.
4. Save backup codes in a secure location.

---

### ✅ Step 2: Lock Away the Root Access Keys
1. Go to **IAM → Security Credentials → Access keys**
2. Delete any existing root access keys.
3. Never create new ones unless critically required.

---

### ✅ Step 3: Don’t Use Root for Daily Tasks
- Create **admin IAM user** for daily use.
- Only use root for:
  - MFA enablement
  - Changing account billing information
  - Closing AWS account

---

### ✅ Step 4: Audit Root Usage
Use **AWS CloudTrail** to track any activity from the root user:
```bash
aws cloudtrail lookup-events --lookup-attributes AttributeKey=Username,AttributeValue=root
```

🧠 Key Takeaways
- Root user = 🔑 master key of your AWS kingdom.
- Use it once to configure, then lock it down forever.
- Monitor all future activity using CloudTrail.
