# 💼 IAM Policy – Interview Questions (With Explanations & Scenarios)

This document helps you prepare for AWS DevOps & Solution Architect interviews by covering **theoretical**, **scenario-based**, and **hands-on** IAM Policy questions.

---

## 📌 1. What are IAM Policies?

**Answer**:  
IAM Policies are JSON documents that define what actions are allowed or denied for which resources in AWS. They follow the structure of `Effect`, `Action`, `Resource`, and optionally `Condition`.

---

## 📌 2. What are the different types of IAM Policies?

**Answer**:  
- **Managed Policies**: AWS-managed or customer-managed policies that can be attached to multiple users, groups, or roles.  
- **Inline Policies**: Embedded directly into a single user, group, or role. Not reusable.

---

## 📌 3. What’s the difference between AWS Managed and Customer Managed Policies?

**Answer**:  
- **AWS Managed**: Prebuilt by AWS, cannot be edited.  
- **Customer Managed**: Created and managed by you. Recommended for custom permission control.

---

## 📌 4. What is an IAM Permissions Boundary?

**Answer**:  
A permissions boundary is an advanced feature that defines the maximum permissions a user or role can have, acting as a guardrail. It’s often used with programmatic IAM role creation.

---

## 📌 5. How does AWS evaluate IAM Policies when multiple are attached?

**Answer**:  
- All **Allow** policies are evaluated together.
- An **explicit Deny** always overrides any Allow.
- If no policy explicitly allows an action, it is **implicitly denied**.

---

## 📌 6. What is the difference between Identity-based and Resource-based policies?

**Answer**:
- **Identity-based**: Attached to IAM Users, Groups, or Roles.
- **Resource-based**: Attached directly to resources (e.g., S3 Bucket Policy, Lambda Function Policy).

---

## 📌 7. Can you give a scenario where a user is getting “Access Denied” even with correct IAM permissions?

**Answer**:  
Yes. Even if the identity policy allows access, a **resource policy (like an S3 bucket policy)** might explicitly deny access to that user, causing "Access Denied".

---

## 📌 8. What is the best way to debug IAM policy issues?

**Answer**:  
- Use the **IAM Policy Simulator**.  
- Check **CloudTrail logs** for denied actions.  
- Validate resource-level permissions and conditions.

---

## 📌 9. What is the difference between Inline vs Managed Policies in terms of lifecycle?

**Answer**:  
- **Inline**: Deleted when the attached identity is deleted. Harder to manage.  
- **Managed**: Exists independently and can be reused across multiple identities.

---

## 📌 10. Hands-On: Attach a policy to allow `s3:PutObject` on a specific bucket.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

---

## 📌 11. What are IAM Policy Conditions?

**Answer**:  
Conditions let you control access based on context such as IP address, time, MFA status, tag values, or AWS Org ID. For example, restrict access to a service only from corporate IPs.

---

## 📌 12. What is the limit on number of policies?

**Answer**:  
- A single IAM role can have up to **10 managed policies** attached.
- Policy size limit is 6,144 characters for inline and 2,048 characters for managed.

---
