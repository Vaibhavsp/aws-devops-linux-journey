## 🎓 08_certification-questions.md – **AWS Certification Practice (MFA & Access Keys)**

These questions are crafted in the style of **AWS SAA-C03** (Solution Architect Associate) certification — scenario-based, tricky, and focused on **MFA**, **Access Keys**, and **Security**.

---

### 🧠 Question 1:  
**A developer has lost the secret key of their IAM user access key. What should the administrator do?**  
A. Retrieve the secret key from the console  
B. Re-enable the access key  
C. Delete the old access key and create a new one  
D. Use AWS Config to recover the key  

✅ **Answer**: **C**  
> Once a secret key is lost, it cannot be retrieved. You must delete and recreate.

---

### 🧠 Question 2:  
**You have enforced MFA using IAM policy. A user complains that the CLI is not working. What is the likely reason?**  
A. CLI doesn’t support MFA  
B. User didn’t run `aws configure`  
C. User didn’t assume the role  
D. User didn’t provide MFA token via `sts:GetSessionToken`  

✅ **Answer**: **D**  
> MFA-enforced policies require you to get temporary credentials using STS with MFA.

---

### 🧠 Question 3:  
**A security team wants to monitor usage of access keys across the organization. What AWS service should be used?**  
A. AWS Inspector  
B. AWS CloudWatch  
C. AWS CloudTrail  
D. AWS Config  

✅ **Answer**: **C**  
> **AWS CloudTrail** tracks all API usage including access key usage.

---

### 🧠 Question 4:  
**How many access keys can a single IAM user have?**  
A. 1  
B. 2  
C. 3  
D. 5  

✅ **Answer**: **B**  
> Only **2** access keys are allowed per user (active/inactive for rotation).

---

### 🧠 Question 5:  
**Which of the following is a best practice for access keys? (Choose 2)**  
A. Store in code repo  
B. Rotate keys regularly  
C. Enable CloudTrail  
D. Assign AdministratorAccess policy  

✅ **Answer**: **B, C**

---

### 🧠 Question 6:  
**What happens when an access key is marked Inactive?**  
A. It is deleted after 7 days  
B. It cannot be used for API calls  
C. It can only be used with MFA  
D. It gets re-enabled after 24 hours  

✅ **Answer**: **B**

---

### 🧠 Question 7:  
**You want to force IAM users to use MFA. How do you do this?**  
A. Assign MFA to IAM Role  
B. Use SCP  
C. Create a Condition block in IAM Policy  
D. Enable in IAM settings  

✅ **Answer**: **C**  
> IAM policies can enforce MFA using `Condition: {"Bool": {"aws:MultiFactorAuthPresent": "true"}}`

---

### 🧠 Question 8:  
**Which STS API is used to generate temporary credentials with MFA?**  
A. `AssumeRole`  
B. `GetFederationToken`  
C. `GetSessionToken`  
D. `AssumeRoleWithSAML`  

✅ **Answer**: **C**

---
