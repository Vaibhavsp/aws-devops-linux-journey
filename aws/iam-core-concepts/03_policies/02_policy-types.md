# 📂 Types of IAM Policies in AWS

AWS offers different types of policies to manage access and permissions in your cloud environment. Each policy serves a different use case depending on where and how it's applied.

---

## 🧩 1. Identity-Based Policies

These are **attached to IAM users, groups, or roles** to control what actions they can perform.

### 🔸 Managed Policies
- **AWS Managed Policies**: Created and maintained by AWS.
  - Example: `AmazonEC2ReadOnlyAccess`
- **Customer Managed Policies**: Created and managed by you.
  - Fully customizable and reusable across multiple identities.

### 🔹 Inline Policies
- Embedded **directly into a single IAM user, group, or role**.
- One-to-one relationship — **not reusable**.
- Use only for fine-grained control.

---

## 🧩 2. Resource-Based Policies

These are **attached directly to AWS resources**, like:

- S3 Buckets (`bucket policy`)
- SNS Topics
- SQS Queues
- Secrets Manager, etc.

### 🔹 Key Feature:
They **support cross-account access** without needing to create roles in the target account.

---

## 🧩 3. Permissions Boundaries

- **Limit** the maximum permissions an IAM user or role can have.
- Think of them as **"permission ceilings."**

📌 Example Use Case:
Let a user create EC2 instances, but only within a certain region or size, even if their identity policy says otherwise.

---

## 🧩 4. Service Control Policies (SCPs)

- Used **only with AWS Organizations**.
- Set permission **guardrails** at the account or OU (organizational unit) level.
- They don’t grant permissions but **restrict** them.

📌 Example:
Block the use of certain regions across all accounts.

---

## 🧩 5. Session Policies

- **Temporary policies** used during session-based authentication.
- Common in **Federated Access** and **STS AssumeRole** situations.

📌 Example:
Limit what a federated user can do during a single session.

---

## 🔍 Summary Table

| Policy Type             | Attached To                  | Use Case                               | Reusable |
|-------------------------|------------------------------|----------------------------------------|----------|
| Identity-Based Policy   | IAM Users, Groups, Roles     | Standard permission management         | ✅       |
| Resource-Based Policy   | AWS Resources                | Cross-account, specific resource access| ❌       |
| Permissions Boundaries  | IAM Users, Roles             | Limit max permissions                  | ✅       |
| SCPs                    | AWS Accounts/OUs             | Org-wide control                       | ✅       |
| Session Policies        | Temporary sessions           | Short-lived permissions                | ❌       |

---

