# 💼 IAM Roles – Interview Questions (Theory + Scenarios)

These questions are crafted to test your conceptual clarity, practical understanding, and real-world problem-solving skills related to IAM Roles.

---

## 📘 Basic to Intermediate:

### 1. What is an IAM Role in AWS, and how is it different from a User?
**Answer:**  
- An IAM Role is an AWS identity with **temporary security credentials** and **no long-term credentials**.
- Unlike a user (meant for people), roles are assumed by **services**, **applications**, or **users from another AWS account**.
- Roles use trust policies to define **who can assume** them and permission policies to define **what they can do**.

---

### 2. When would you use an IAM Role instead of an IAM User?
**Answer:**  
- When AWS services (like EC2, Lambda, etc.) need access to other AWS resources.
- For **cross-account access** without sharing credentials.
- For **federated access** using Identity Providers (IdPs).
- When using **temporary credentials** for better security.

---

### 3. What are the core components of an IAM Role?
**Answer:**
- **Trust Policy** – defines **who** can assume the role.
- **Permissions Policy** – defines **what actions** the role can perform.
- **Role Session Duration** – how long the temporary credentials are valid.
- **Role Assumption Method** – STS, SDK, AWS CLI, service linking, etc.

---

## 🔍 Advanced / Scenario-Based:

### 4. Explain the IAM Role assumption process with EC2.
**Answer:**
1. You create an IAM Role with specific permissions (e.g., S3 read).
2. Attach that Role to an EC2 instance.
3. Inside the instance, applications retrieve temporary credentials via the **EC2 Instance Metadata Service**.
4. These temporary credentials are used to access S3 securely without hardcoding credentials.

---

### 5. What is the EC2 Instance Metadata Service, and how does it help with IAM Roles?
**Answer:**
- The **Instance Metadata Service (IMDS)** provides data about the instance.
- When an IAM role is attached, apps inside the instance can query IMDS to retrieve **temporary access keys, secret keys, and session tokens** for that role.

Command:
```bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

---

### 6. What is the purpose of the `AssumeRole` API?
**Answer:**
- It allows a principal (user/service) to request **temporary security credentials** for a role.
- Used in **cross-account access**, **federated login**, **service-to-service** interactions.

---

### 7. Explain the Trust Policy and its importance.
**Answer:**
- Trust policy defines **who can assume** the IAM role.
- Without a correct trust relationship, even if the role has permissions, it cannot be assumed.
- Example: Allow EC2 service to assume a role.

```json
{
  "Effect": "Allow",
  "Principal": { "Service": "ec2.amazonaws.com" },
  "Action": "sts:AssumeRole"
}
```

---

### 8. What are the common issues you face when IAM Roles don’t work?
**Answer:**
- Role not attached correctly to the service.
- Incorrect or missing **trust policy**.
- Insufficient permissions in the **permissions policy**.
- Missing permissions at the **resource level** (e.g., S3 bucket policy).
- Trying to assume a role from a region where it's not allowed or not supported.

---

### 9. How do you troubleshoot IAM Role-related access denied errors?
**Answer:**
- Confirm if the role has required permissions (policy).
- Verify if the role is attached or assumed.
- Check Trust Policy – is the correct principal defined?
- Use **CloudTrail** to inspect STS AssumeRole events.
- Use **IAM Policy Simulator** to test role permissions.

---

### 10. What are best practices when working with IAM Roles?
**Answer:**
- **Use least privilege** – grant only required permissions.
- **Use roles instead of users** for services.
- Enable **MFA** when roles are assumed via console.
- Rotate policies regularly and monitor with **CloudTrail**.
- **Avoid hardcoding credentials**, always use temporary credentials from roles.
