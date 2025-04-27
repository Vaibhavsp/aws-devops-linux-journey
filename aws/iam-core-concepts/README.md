# 🌟 AWS Identity and Access Management (IAM)

## Overview
AWS Identity and Access Management (IAM) is a service that helps securely control access to AWS resources. Using IAM, you can create and manage AWS users and groups, and use permissions to allow or deny their access to AWS services.

---

## Key Concepts
- **User:** An individual identity with credentials.
- **Group:** A collection of users managed together.
- **Role:** A set of permissions that can be assumed temporarily.
- **Policy:** A JSON document that defines permissions.
- **Authentication vs Authorization:** IAM handles both who is allowed and what actions are permitted.

---

## Hands-On Covered
- ✅ Creating IAM Users and Groups  
- ✅ Setting up IAM Roles for EC2  
- ✅ Implementing Custom Policies  
- ✅ Using IAM Policy Simulator  
- ✅ Enabling MFA (Multi-Factor Authentication)  
- ✅ Understanding IAM Best Practices  

---

## Best Practices
- 🔒 Enable MFA for root and all users.  
- 📜 Follow the Principle of Least Privilege (only grant necessary permissions).  
- 🔄 Rotate credentials regularly.  
- 🧹 Clean up unused roles, users, and policies.  
- 🔥 Never use root user for daily tasks.

---

## Common Use Cases
- Granting a developer access to a specific S3 bucket.
- Allowing EC2 instances to interact with S3 without keys (using IAM Roles).
- Managing access for third-party applications.
- Controlling API access with IAM policies.

---

## Diagrams
                          +-------------------+
                          |    AWS Account     |
                          +-------------------+
                                   |
           +-----------------------+-----------------------+
           |                                               |
   +---------------+                              +----------------+
   |     Users     |                              |    Groups       |
   +---------------+                              +----------------+
           |                                               |
           +----------------+           +----------------+
                            |             |
                      +-----------------------+
                      |      Policies (JSON)   |
                      +-----------------------+
                                   |
                          +-------------------+
                          |      Permissions    |
                          +-------------------+
                                   |
                          +-------------------+
                          |    AWS Services    |
                          | (EC2, S3, Lambda)   |
                          +-------------------+

  

---

## References
- [AWS IAM Official Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- [AWS Security Best Practices](https://docs.aws.amazon.com/general/latest/gr/aws-security-best-practices.html)

---

## Author
**Vaibhav Parekh**  
### Medium: [medium.com/@vaibhavparekh097](https://medium.com/@vaibhavparekh097)
### LinkedIn: [linkedin.com/in/vaibhav-parekh08](https://www.linkedin.com/in/vaibhav-parekh08/)
