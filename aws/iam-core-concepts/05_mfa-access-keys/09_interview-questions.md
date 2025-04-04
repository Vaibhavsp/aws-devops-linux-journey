## 💼 09_interview-questions.md – **IAM MFA & Access Keys Interview Q&A**

These are real-world **interview-style** questions — deep, scenario-based, and focused on security best practices with **Multi-Factor Authentication (MFA)** and **Access Keys** in AWS IAM.

---

### 🔐 MFA (Multi-Factor Authentication)

---

### 🧠 Q1: **What is MFA in AWS, and why is it important?**  
**Answer**:  
MFA adds an extra layer of security to your AWS account. It requires users to present two forms of authentication:  
- Something you know (password)  
- Something you have (MFA device)

This helps prevent unauthorized access even if credentials are compromised.

---

### 🧠 Q2: **Which MFA device types are supported by AWS IAM?**  
**Answer**:  
1. Virtual MFA (e.g., Google Authenticator, Authy)  
2. U2F security keys (e.g., Yubikey)  
3. Hardware MFA devices (Gemalto tokens)

---

### 🧠 Q3: **How do you enforce MFA for all IAM users?**  
**Answer**:  
By creating an IAM policy with a condition:  
```json
"Condition": {
  "BoolIfExists": {
    "aws:MultiFactorAuthPresent": "true"
  }
}
```
Attach this policy to a group or user. This blocks access until MFA is used.

---

### 🧠 Q4: **What if a user hasn't configured MFA and gets denied access?**  
**Answer**:  
AWS denies access based on policy. To fix:
1. Temporarily attach an exception policy to allow MFA device registration.
2. Once configured, remove that policy and enforce MFA again.

---

### 🧠 Q5: **How do you use the CLI with MFA?**  
**Answer**:
You must use the `aws sts get-session-token` command:
```bash
aws sts get-session-token \
  --serial-number arn:aws:iam::123456789012:mfa/username \
  --token-code 123456
```
Then, use the temporary credentials it returns to authenticate.

---

### 🔑 Access Keys

---

### 🧠 Q6: **How do you securely manage access keys in AWS?**  
**Answer**:
- Never hard-code or commit them in code
- Rotate every 90 days
- Use environment variables or AWS Secrets Manager
- Monitor usage via CloudTrail

---

### 🧠 Q7: **What are best practices for IAM access keys?**  
**Answer**:
- Use roles wherever possible instead of users with access keys  
- Avoid long-term credentials  
- Audit using credential reports  
- Disable unused keys  
- Rotate regularly

---

### 🧠 Q8: **How many access keys can an IAM user have? Why?**  
**Answer**:
Two. This supports key rotation: deactivate one, activate the new one, test, then delete the old.

---

### 🧠 Q9: **What happens when an access key is inactive?**  
**Answer**:
The key is disabled and cannot be used for authentication or API calls. You can reactivate or delete it.

---

### 🧠 Q10: **How can you audit or monitor access key usage?**  
**Answer**:
Use **AWS CloudTrail** to view API calls made using access keys.  
Additionally, generate **IAM Credential Reports** to see last-used info and security status.

---

### 🧠 Q11: **What should you do if a secret access key is lost?**  
**Answer**:
Delete the key and create a new one. AWS doesn’t allow you to retrieve the secret key again for security reasons.

---

### 🧠 Q12: **Can you use MFA with access keys?**  
**Answer**:
Yes, but only with temporary credentials using `sts:GetSessionToken`. Permanent access keys do not inherently require MFA.

---
