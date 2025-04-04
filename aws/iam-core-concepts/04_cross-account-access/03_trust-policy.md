### 🎯 What is a **Trust Policy** in IAM?

A **Trust Policy** defines **who (which principal)** is allowed to **assume a role**. It is different from a permissions policy. Instead of saying *"what actions are allowed"*, it says *"who can assume this role."*

This is **attached to a Role**, not to a User.

---

### 📘 Trust Policy JSON Structure (Breakdown)

Let’s look at this example again:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111111111111:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

### 🧠 Line-by-Line Explanation

| Element | Meaning |
|--------|--------|
| `"Version": "2012-10-17"` | AWS policy language version |
| `"Effect": "Allow"` | Allow the defined action |
| `"Principal"` | The **entity** that is allowed to assume the role |
| `"AWS": "arn:aws:iam::111111111111:root"` | This allows *all IAM users and roles* in Account A (ID: 111111111111) to assume the role |
| `"Action": "sts:AssumeRole"` | The action that is allowed (required for assuming a role) |

---

### 🔐 What is `sts:AssumeRole`?

It tells AWS:  
➡️ *"Allow this principal to use Security Token Service (STS) to assume this role."*

---

### 💡 What is the `"root"` in `"arn:aws:iam::111111111111:root"`?

It means *the whole account*.  
So **any IAM user or role** in Account A (1111...) can assume this role.

You can restrict this by replacing `root` with a specific **IAM user** or **role ARN**.

Example:
```json
"AWS": "arn:aws:iam::111111111111:user/crossaccount-user"
```

---

### 🔒 Optional Condition (Best Practice)

To restrict access to specific services or users, you can add **conditions** like MFA, IP, or Tags.

Example – Require MFA:
```json
"Condition": {
  "Bool": {
    "aws:MultiFactorAuthPresent": "true"
  }
}
```

---

### ✅ Summary

| Concept | Meaning |
|--------|---------|
| **Trust Policy** | Defines *who can assume the role* |
| **Principal** | Entity allowed to assume the role |
| **Action** | Always `sts:AssumeRole` |
| **Attached To** | IAM Role only |
| **Usage** | Used in Cross-Account, Federated Users, EC2 Assume Role, etc. |

---
