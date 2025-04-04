 # **💼 AWS IAM Cross-Account Access – Interview Questions & Answers**

These questions are designed to cover theory, hands-on understanding, real-world scenarios, and edge cases.

---

### ✅ **1. What is IAM Cross-Account Access?**
**Answer:**  
Cross-account access in AWS allows an IAM user or role in one AWS account (Account A) to access resources in another AWS account (Account B) without creating separate IAM users in the target account. This is achieved by creating an **IAM Role** in the target account with a **trust policy** that allows the source account to assume that role.

---

### ✅ **2. How does IAM Role facilitate cross-account access?**
**Answer:**  
You create a role in **Account A** with a **trust relationship** allowing an IAM user or role in **Account B** to **assume** it. Then, the entity in Account B can use `sts:AssumeRole` to obtain **temporary security credentials** to act as that role.

---

### ✅ **3. What are the steps to implement cross-account IAM role access?**
**Answer:**

1. **Create IAM Role in Account A** with:
   - Trust policy allowing Account B (with principal as Account B’s IAM user/role ARN).
   - Permission policy for the AWS services/resources it can access.
2. **Grant `sts:AssumeRole` permission in Account B** to the IAM user or role.
3. **Use AWS CLI in Account B** to assume the role using:
   ```bash
   aws sts assume-role \
     --role-arn "arn:aws:iam::AccountA_ID:role/CrossAccountAccessRole" \
     --role-session-name "test-session"
   ```

---

### ✅ **4. What is a trust policy in the context of IAM roles?**
**Answer:**  
A **trust policy** defines *who is allowed to assume* the IAM role. It specifies the **trusted entities** (e.g., specific users, roles, accounts, federated users, services) that can request to assume the role using `sts:AssumeRole`.

---

### ✅ **5. What is the use of `sts:AssumeRole`?**
**Answer:**  
`sts:AssumeRole` is an action that allows a user or role to take on the permissions of another IAM role. This is essential for **cross-account access** and for **delegating access** with temporary security credentials.

---

### ✅ **6. What are common issues when setting up cross-account roles?**
**Answer:**

| 🔍 Issue | 🛠️ Solution |
|---------|--------------|
| `AccessDenied` during AssumeRole | Ensure `sts:AssumeRole` is allowed in the source account |
| Incorrect Role ARN | Double-check the full ARN of the target role |
| Trust policy is misconfigured | Validate that the trust relationship includes the correct source account/user/role ARN |
| Expired temporary credentials | Make sure you're using them before they expire |
| CLI not using temporary credentials | Export the credentials from `sts:AssumeRole` properly |

---

### ✅ **7. How can you track cross-account access activities?**
**Answer:**  
By using **AWS CloudTrail**. It logs all `sts:AssumeRole` API calls, including who assumed the role, when, and from where. You can filter logs by `eventName = AssumeRole`.

---

### ✅ **8. What is the best practice for IAM role naming in a cross-account setup?**
**Answer:**  
Use clear, descriptive role names like `cross-account-s3-access-from-account-B`, and tag them appropriately. This improves visibility, logging, and auditing.

---

### ✅ **9. Can an IAM user directly access another account’s resources?**
**Answer:**  
No. IAM users are account-scoped. They need to assume a role in the target account that grants the required access.

---

### ✅ **10. What is role chaining in cross-account access?**
**Answer:**  
Role chaining is the practice of assuming one role, then using the temporary credentials to assume another role. AWS limits the maximum role chaining depth to one role (i.e., you can't chain multiple role assumptions).

---

### ✅ **11. Can you attach an IAM policy directly to an AWS account?**
**Answer:**  
No. IAM policies can only be attached to users, groups, or roles, not to accounts. For cross-account access, roles and trust policies are used.

---

### ✅ **12. What are federated users and can they use cross-account roles?**
**Answer:**  
Federated users are external identities (like SAML, OIDC, Cognito) who access AWS temporarily. Yes, they can assume cross-account roles if included in the trust policy as `Federated` principals.

---
