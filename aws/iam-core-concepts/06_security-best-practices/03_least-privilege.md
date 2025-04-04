# 🔐 Enforcing Least Privilege in AWS IAM

## 📘 What is Least Privilege?
The **Principle of Least Privilege** means:
> Give users only the permissions they need to perform their job—and nothing more.

---

## 🤔 Why is Least Privilege Important?

| Reason | Explanation |
|--------|-------------|
| 🔒 Security | Limits potential damage if credentials are compromised |
| 📉 Reduces Risk | Prevents accidental deletion, changes, or misuse |
| 📜 Audit & Compliance | Easier to track and justify permission assignments |

---

## ✅ How to Implement Least Privilege

### 🧱 1. Start With Zero Permissions
- When creating a new user or role, **don’t attach any policies initially**.
- Grant permissions gradually as needed.

### 🧪 2. Use IAM Access Advisor
- Shows what services a user has accessed in the last 365 days.
- Navigate to **IAM → Users → UserName → Access Advisor** to audit usage.

### 🎯 3. Attach Specific Managed Policies
Instead of AdministratorAccess, use AWS-managed policies like:
- `AmazonS3ReadOnlyAccess`
- `AmazonEC2FullAccess`

### 🛠️ 4. Use Custom Policies for Granular Control
Example: Grant only S3 list access
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["s3:ListBucket"],
    "Resource": ["arn:aws:s3:::my-bucket"]
  }]
}
```

### 🔄 5. Review and Rotate Permissions
- Perform regular reviews every quarter.
- Remove unused permissions or roles.

---

## 🧠 Pro Tips
- Always test policies using the **IAM Policy Simulator**.
- Combine IAM + SCP (Service Control Policies) in AWS Organizations for multi-account control.

---

## 🧪 Hands-On CLI Example

Create a custom policy for EC2 start/stop only:
```bash
aws iam create-policy \
  --policy-name EC2StartStopOnly \
  --policy-document file://ec2-start-stop-policy.json
```

---

## 🧠 Summary

| Do’s ✅ | Don’ts ❌ |
|--------|----------|
| Start with no permissions | Give full Admin access to everyone |
| Apply granular policies | Use root user for daily tasks |
| Review permissions often | Forget to remove unused access |

---

