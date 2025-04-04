# 🔍 IAM Roles – Troubleshooting & Common Challenges

This document outlines real-world issues faced while working with IAM Roles and how to solve them.

---

## 🚫 1. Access Denied Even With Role Attached
- **Cause**: Trust relationship not configured correctly.
- **Solution**: Check `Trust Policy` for correct `Principal` and service (like `ec2.amazonaws.com`).

## 🚫 2. EC2 Can't Access S3 (or Other Services)
- **Cause**: Role lacks permissions or S3 bucket policy restricts access.
- **Solution**: 
  - Verify EC2 role permissions.
  - Confirm bucket policy allows access from the role.
  - Check networking or VPC endpoint issues.

## 🚫 3. AssumeRole Fails
- **Cause**: Missing `sts:AssumeRole` permission or bad trust relationship.
- **Solution**: 
  - Ensure user or service has the right permissions.
  - Validate trust relationship on the role.

## 🚫 4. Role Not Showing in EC2 Launch
- **Cause**: Role created without correct trust policy for EC2.
- **Solution**: Trust policy must include `ec2.amazonaws.com` as the service.

## 🚫 5. Confused Deputy Problem
- **Cause**: 3rd-party misuses a role's permissions.
- **Solution**: Use `ExternalId` in the trust policy when allowing third-party access.

## 🚫 6. No Role Usage Logs
- **Cause**: CloudTrail not enabled.
- **Solution**: Enable CloudTrail across all regions and ensure logs are configured.

## 🚫 7. Metadata Service Not Accessible
- **Cause**: IMDS blocked or misconfigured.
- **Solution**: 
  - Enable **IMDSv2**.
  - Ensure no firewall blocks `169.254.169.254`.

## 🚫 8. Multiple Roles Needed on EC2
- **Cause**: One EC2 can't have multiple roles directly.
- **Solution**: Merge permissions into a single policy or use a credentials proxy pattern.

## 🚫 9. Permissions Look Right But Fail
- **Cause**: Other policies (SCPs, Resource Policies) blocking actions.
- **Solution**: Use **IAM Policy Simulator** and check org-wide restrictions.

## 🚫 10. Cross-account AssumeRole Fails
- **Cause**: `sts:AssumeRole` not granted or trust policy missing.
- **Solution**: 
  - Confirm IAM role trust policy in **target** account.
  - Ensure **source** user/role has `sts:AssumeRole` permission.

---

> ✅ Tip: Use AWS IAM Access Analyzer and CloudTrail together for deep troubleshooting of IAM roles.
