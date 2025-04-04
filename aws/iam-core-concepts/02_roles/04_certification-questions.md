# 🎓 Scenario-Based Certification Questions – IAM Roles

### ✅ Question 1:
**Scenario:**  
You need to allow an EC2 instance in your VPC to access objects in an S3 bucket without storing credentials on the instance. What should you do?

A. Attach a bucket policy to the S3 bucket granting public access  
B. Use access keys and store them in the instance  
C. Create an IAM Role with S3 read-only policy and assign it to the EC2 instance  
D. Create a new IAM user and assign S3 full access  

**Correct Answer:** ✅ C  
**Explanation:** IAM roles are designed to grant permissions to AWS services like EC2 without embedding credentials.

---

### ✅ Question 2:
**Scenario:**  
A Lambda function in Account A needs to access a DynamoDB table in Account B. What’s the recommended approach?

A. Create an IAM user in Account B and share credentials with Account A  
B. Use STS to generate temporary credentials  
C. Create an IAM role in Account B with trust policy for Account A  
D. Enable cross-region replication on DynamoDB  

**Correct Answer:** ✅ C  
**Explanation:** Use **Cross-Account IAM Role** with a trust relationship so the Lambda function can assume the role.

---

### ✅ Question 3:
**Scenario:**  
Your EC2 instance uses an IAM Role to access S3. You rotated your S3 bucket policy, and now access fails. What’s the FIRST thing you should check?

A. If the EC2 instance has a public IP  
B. If the IAM role still has S3 permissions  
C. If the bucket policy allows access to the IAM Role  
D. If the role trust policy includes the EC2 instance profile  

**Correct Answer:** ✅ C  
**Explanation:** Bucket policies must explicitly allow access from the IAM role used by the EC2 instance.

---

### ✅ Question 4:
**Scenario:**  
Your security team wants all AWS services to use temporary credentials. Which AWS feature helps enforce this?

A. IAM Groups  
B. IAM Roles  
C. IAM Users  
D. Access Analyzer  

**Correct Answer:** ✅ B  
**Explanation:** IAM Roles are designed to issue temporary security credentials.

---

### ✅ Question 5:
**Scenario:**  
You created an IAM Role with `AmazonS3FullAccess` and attached it to an EC2 instance, but still get "Access Denied" when accessing a bucket. What could be the issue?

A. Role not attached to the instance  
B. S3 bucket policy does not allow the role's access  
C. Role has incorrect trust policy  
D. All of the above  

**Correct Answer:** ✅ D  
**Explanation:** All options could prevent access — especially the bucket policy and trust relationship.

---

## 🧠 Pro Tip for the Exam:
- Focus on **who can assume the role** (trust policy) and **what the role can do** (permissions policy).
- Look out for **temporary credentials** and **best practices** questions.

---
