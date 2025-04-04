# 🚧 IAM Policy Troubleshooting Guide

When working with IAM Policies, it's common to encounter **access issues**, **unexpected denials**, or **permissions not working** as expected. This guide will walk you through common IAM policy troubleshooting tips and solutions.

---

## 🔍 Common Issues & Fixes

---

### 1️⃣ ❌ Access Denied Errors

**Cause:**  
- Missing permissions
- Implicit denial (no allow statement)
- Explicit deny overrides allow

**Fix:**
- Use **IAM Policy Simulator** to test permission combinations
- Check for **explicit deny** statements
- Ensure the **action** and **resource** are correctly defined

---

### 2️⃣ 🔐 No Effect After Attaching Policy

**Cause:**  
- Policy was attached to the wrong user/role/group
- Policy has conditions that aren't being met
- The IAM entity is not being used in the current session (e.g., EC2 role not attached properly)

**Fix:**
- Double-check which entity the policy is attached to
- Verify **conditions (`Condition` block)** in the policy
- If using roles, make sure they are being assumed correctly

---

### 3️⃣ ⛔️ Conflicting Permissions

**Cause:**  
- Multiple policies attached (some allowing, some denying)
- Explicit deny takes priority

**Fix:**
- Review all attached policies to the entity (user/group/role)
- Remove or update conflicting policies

---

### 4️⃣ 🤯 Confused Between Resource and Action

**Cause:**  
- Mismatch in policy's `Action` or `Resource`
- For example, using an EC2 action on an S3 resource

**Fix:**
- Refer to the [AWS IAM Actions Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_actions-resources-contextkeys.html)
- Ensure the correct **service namespace**, **action**, and **ARN format** are used

---

### 5️⃣ 🌀 Wildcard (*) Misuse

**Cause:**  
- Using `*` without understanding scope

**Fix:**
- Use `*` cautiously (especially in `Resource`)
- Best practice: restrict permissions using specific resource ARNs whenever possible

---

### 6️⃣ 🛑 Policy Not Working with MFA

**Cause:**  
- Policy requires MFA but user has not authenticated with MFA

**Fix:**
- Make sure MFA is **enabled** and **used** while testing
- Verify policy's `Condition` block has `"aws:MultiFactorAuthPresent": "true"`

---

### 7️⃣ 🔄 Role Not Being Assumed

**Cause:**  
- Using IAM Role without assuming it (in CLI or programmatically)
- Trust relationship missing or incorrect

**Fix:**
- Use `aws sts assume-role` or IAM console to assume the role
- Ensure trust relationship in target role includes the source principal

---

## 🛠️ Tools for Troubleshooting

| Tool | Purpose |
|------|---------|
| ✅ **IAM Policy Simulator** | Test and simulate policies attached to IAM entities |
| ✅ **CloudTrail** | Check who made what request and whether it was allowed/denied |
| ✅ **Access Advisor** | Shows what services are being used by the entity |
| ✅ **IAM Access Analyzer** | Detects overly permissive policies and access paths |

---

## ✅ Tips to Debug Faster

1. Start with **Policy Simulator**.
2. Look into **CloudTrail** for denied actions.
3. Use **AWS CLI** with `--debug` for deep troubleshooting.
4. Keep policies **modular** and **simple**.
5. Prefer **Customer Managed Policies** over inline for better visibility.

---
