# 📘 IAM Policy – Certification Style Questions (SAA-C03)

These scenario-based questions will help you prepare for AWS Certification exams by testing your understanding of IAM Policies in real-world situations.

---

## 🧠 Question 1: Understanding Policy Evaluation

**Scenario**:  
A developer is trying to access an S3 bucket but receives an "Access Denied" error, even though the IAM policy allows `s3:GetObject`.  

**Which of the following could be the reason?**  
A. The bucket policy explicitly denies access  
B. The user is not authenticated  
C. The IAM role is not attached properly  
D. The user has no MFA device enabled

✅ **Answer**: A  
➡ IAM policy might allow, but **explicit deny in bucket policy** overrides all allows.

---

## 🧠 Question 2: Inline vs Managed Policy

**Which of the following is a disadvantage of using Inline Policies?**  
A. They can be reused across multiple users  
B. They support versioning  
C. They are hard to track and manage  
D. They are global in scope

✅ **Answer**: C  
➡ Inline policies are tied to individual identities and not reusable, hence harder to manage.

---

## 🧠 Question 3: Resource-Specific Permissions

**Scenario**:  
You want a user to access only the objects in one specific S3 bucket.  

**Which of the following IAM policy statements is correct?**

```json
A. {
  "Effect": "Allow",
  "Action": "s3:*",
  "Resource": "*"
}
```

```json
B. {
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::mybucket/*"
}
```

✅ **Answer**: B  
➡ Only grants read access to a specific bucket.

---

## 🧠 Question 4: Policy with Condition

**Scenario**:  
You want to ensure users can only access resources from the corporate IP address.  

**What IAM feature should you use?**  
A. IAM Role  
B. IAM Policy Condition  
C. MFA Enforcement  
D. IAM Group

✅ **Answer**: B  
➡ Use `Condition` block with `IpAddress`.

---

## 🧠 Question 5: Policy Simulation

**When should you use the IAM Policy Simulator?**  
A. When migrating users  
B. To test permissions before deployment  
C. To rename policies  
D. To delete expired users

✅ **Answer**: B  
➡ IAM Policy Simulator is useful to test and debug access before applying permissions.

---

## 🧠 Question 6: Permissions Boundary Use Case

**What is the purpose of Permissions Boundaries in IAM?**  
A. Grant full access to the root user  
B. Define which AWS services can be used by an EC2 instance  
C. Limit the maximum permissions a user or role can have  
D. Restrict IAM users from assuming roles

✅ **Answer**: C  
➡ Permission Boundaries define the maximum permissions a user or role can have.

---
