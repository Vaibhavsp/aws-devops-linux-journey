# 🔐 IAM Roles – Deep Dive

## What is an IAM Role?
An IAM Role is an AWS identity with specific permissions that a trusted entity can assume. Unlike users, roles are *not* associated with a specific person or group—they are *assumed* by trusted entities like users, services, or applications.

---

## Why Use IAM Roles?
- Grant temporary access to AWS resources.
- Avoid hardcoding credentials.
- Enable secure cross-account access.
- Allow services (like EC2 or Lambda) to perform actions on your behalf.

---

## Key Elements:
- **Trust Policy**: Defines who can assume the role.
- **Permissions Policy**: Defines what actions the role can perform.
- **Session Duration**: Temporary credentials last between 15 mins to 12 hours.

---

## When to Use IAM Roles?
- EC2 Instances needing S3 access.
- Cross-account access between AWS accounts.
- Delegating access between AWS services.
- Federated identity (SSO) via an Identity Provider.

---

## Real-time Example:
Give EC2 instance access to upload files to S3 without storing access keys.

