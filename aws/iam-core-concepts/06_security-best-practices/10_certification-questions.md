# 📝 AWS SAA-C03 Certification Questions: MFA & Access Keys

---

### ✅ Q1. A user lost access to the MFA device and cannot log in. What’s the best solution?

**A.** Disable MFA in the CLI  
**B.** Delete the IAM user  
**C.** As an admin, deactivate MFA and allow reset  
**D.** Wait for AWS to reset the account

✔️ **Answer**: C

---

### ✅ Q2. Which IAM policy enforces MFA for all actions?

```json
{
  "Effect": "Deny",
  "Action": "*",
  "Resource": "*",
  "Condition": {
    "BoolIfExists": {
      "aws:MultiFactorAuthPresent": "false"
    }
  }
}
```

What is the purpose of the above policy?

**A.** Deny actions if MFA is not used  
**B.** Allow actions only if MFA used  
**C.** Enforce root key use  
**D.** Force console login only

✔️ **Answer**: A

---

### ✅ Q3. Which tool is used to audit unused access keys?

**A.** AWS Config  
**B.** CloudTrail  
**C.** IAM Analyzer  
**D.** Credential Report

✔️ **Answer**: D

---

### ✅ Q4. How can you secure access keys for EC2 instances?

**A.** Store keys in environment variable  
**B.** Use IAM Roles with temporary credentials  
**C.** Use root user keys  
**D.** Save keys in AMI

✔️ **Answer**: B

---

### ✅ Q5. What’s the limit of access keys per IAM user?

**A.** 1  
**B.** 2  
**C.** 5  
**D.** Unlimited

✔️ **Answer**: B

---
