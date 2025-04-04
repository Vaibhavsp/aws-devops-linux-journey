### 🔐 **What is Cross-Account Access in IAM?**

Cross-account access allows **resources in one AWS account to be accessed securely** from another AWS account, **without sharing long-term credentials**.

---

### ✅ **Why is Cross-Account Access Needed?**

- **Separation of accounts** for security (Dev, QA, Prod)
- **Centralized access** for admin users or tools
- **Shared services** architecture (e.g., central logging, monitoring, billing)
- Avoids using Access Keys across accounts (security risk)

---

### 🧠 Key Concepts:

| Concept | Description |
|--------|-------------|
| **Account A** | The account that has the users who want to access a resource. (Requester Account) |
| **Account B** | The account that owns the resource (like S3, Lambda, EC2, etc.). (Resource Owner Account) |
| **Role** | IAM Role created in Account B that grants access to its resources. |
| **Trust Policy** | A JSON document in the IAM Role which allows users from Account A to "assume" this role. |
| **AssumeRole** | An action used to switch to the IAM Role in Account B from Account A. |

---

### 🔁 How Does Cross-Account Access Work?

#### 📌 Step-by-step Concept Flow:

1. **Create a Role in Account B**
   - This role gives access to a resource (e.g., S3, DynamoDB).
   - It contains a **trust policy** allowing users from Account A to assume it.

2. **Add Permission Policy to Role**
   - Grants permission to access specific AWS resources.

3. **In Account A**, user runs `sts:AssumeRole`
   - This switches the current identity to the role in Account B using temporary credentials.

4. **User can now access resources in Account B securely.**

---

### 🔒 Trust Policy – Key to Cross-Account Access

This is the JSON block that goes into the IAM Role in Account B:

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

📌 Replace `111111111111` with Account A's AWS Account ID.

---

### 🎯 Use Cases of Cross-Account Access:

- Centralized CI/CD (e.g., Jenkins or GitLab from one account deploys to others)
- Monitoring via CloudWatch from a central account
- Billing & usage tracking in an Org structure
- Security auditing from a master account

---
