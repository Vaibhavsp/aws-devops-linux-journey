# 🎯 IAM Users – Interview Questions

---

### Q1. What is the difference between an IAM user and a root user?
- Root user has full unrestricted access.
- IAM users are managed identities with limited permissions.

---

### Q2. How would you manage secure access to AWS services for different users?
- Create individual IAM users.
- Assign policies via groups.
- Enforce MFA and password policy.
- Rotate access keys regularly.

---

### Q3. Explain the principle of least privilege.
- Only give users the exact permissions they need—no more, no less.

---

### Q4. What happens if you delete an IAM user who had access keys?
- The keys become invalid immediately.
- No access to AWS CLI or API using those keys anymore.

---

### Q5. How do you rotate access keys for a user?
1. Create new keys
2. Update application config
3. Test
4. Delete the old keys

---

### Q6. How do you enforce MFA for IAM users?
- Set up MFA under **Security Credentials**
- Use a virtual MFA device like Google Authenticator or Authy

---

### Q7. How do you track IAM user activity?
- Enable **AWS CloudTrail**
- Check **login events, policy evaluation logs, and usage logs**

---

### Q8. Can one IAM user belong to multiple groups?
✅ Yes, and will inherit permissions from all those groups.

---

### Q9. What are IAM Access Keys and when should they be used?
- Programmatic access (CLI, SDK)
- Never hardcode them in source code
- Rotate periodically

---

### Q10. What's the default limit on IAM users?
- 5,000 per account by default (can be increased via AWS support)

---
