# **📚 AWS IAM Cross-Account Access – Certification Style Questions (SAA-C03)**

These questions follow the scenario-based style of the **AWS Solutions Architect Associate (SAA-C03)** exam and cover the *IAM Cross Account Access* topic in-depth.

---

### ✅ **Question 1: Cross-Account Role Access**

A developer in **Account B** needs to access an S3 bucket in **Account A**. What must be set up for this to work securely?

**A.** Attach an inline policy in Account A to allow access from Account B  
**B.** Create a role in Account A with trust policy allowing Account B and attach an S3 policy  
**C.** Create a user in Account A and share credentials with developer  
**D.** Use an access key from Account A in Account B directly

> **Answer:** ✅ **B**  
> **Explanation:** You need to create an IAM role in Account A with a trust policy that allows access from the user or role in Account B, and attach appropriate permission policies to access S3.

---

### ✅ **Question 2: Permission Denied during AssumeRole**

You set up cross-account access but users in Account B get an `AccessDenied` error when calling `AssumeRole`. What could be the reason?

**A.** IAM Role ARN is incorrect in the trust policy  
**B.** The permissions boundary is missing  
**C.** Users in Account B don’t have `sts:AssumeRole` permissions  
**D.** MFA is not enabled

> **Answer:** ✅ **C**  
> **Explanation:** The calling user in Account B needs an IAM policy that explicitly allows `sts:AssumeRole` on the target role ARN.

---

### ✅ **Question 3: Trust Relationship Scope**

What component defines who can assume a role in a cross-account setup?

**A.** Permission policy  
**B.** Access keys  
**C.** Trust policy  
**D.** Role path

> **Answer:** ✅ **C**  
> **Explanation:** The trust policy specifies which IAM users or roles can assume the role.

---

### ✅ **Question 4: CloudTrail Auditing**

Which of the following is useful to track which user assumed a role via cross-account access?

**A.** IAM Access Analyzer  
**B.** AWS Trusted Advisor  
**C.** CloudTrail  
**D.** CloudWatch

> **Answer:** ✅ **C**  
> **Explanation:** CloudTrail logs all `AssumeRole` events and provides identity, time, and source information.

---

### ✅ **Question 5: Role Access Not Working**

You assumed a role using `sts:assume-role`, but still can’t access EC2 instances in the trusted account. What might be the problem?

**A.** The CLI session expired  
**B.** You didn’t attach an EC2 policy to the assumed role  
**C.** MFA wasn’t used  
**D.** Region mismatch

> **Answer:** ✅ **B**  
> **Explanation:** Assuming the role only works if the attached policy allows required actions (e.g., EC2:DescribeInstances).

---

### ✅ **Question 6: Least Privilege Enforcement**

What is the best practice for granting cross-account access?

**A.** Use broad permissions to avoid friction  
**B.** Always use resource-based policies  
**C.** Use roles with narrowly scoped policies and trust relationships  
**D.** Create temporary users in the target account

> **Answer:** ✅ **C**  
> **Explanation:** AWS recommends using IAM roles with least-privilege permissions and a properly scoped trust relationship.

---

### ✅ **Question 7: Inline vs Managed Policy in Cross Account Setup**

Which type of policy is better for reuse when assigning permissions to a cross-account role?

**A.** Inline Policy  
**B.** Managed Policy  
**C.** SCP  
**D.** None of the above

> **Answer:** ✅ **B**  
> **Explanation:** Managed policies are reusable across multiple identities and recommended for standardization.

---
