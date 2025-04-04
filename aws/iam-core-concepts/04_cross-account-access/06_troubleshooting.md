## 📄 *IAM Cross-Account Access Troubleshooting Guide*

When setting up cross-account IAM access, you might run into a few frustrating issues. Let’s tackle them one by one with **causes**, **solutions**, and **debugging steps** 🔍

---

### 🛠️ 1. **Error: `AccessDenied` when assuming role**

**❓ Cause:**  
The trust policy is missing or misconfigured in the trusting account (Account A), or permissions are missing in the calling account (Account B).

**✅ Solution:**

- Verify the trust relationship in the **IAM Role** of Account A:
   - Make sure it allows the correct user/role from Account B.
- Verify the user/role in Account B has `sts:AssumeRole` permission.
  
---

### 🛠️ 2. **Error: `The role cannot be assumed`**

**❓ Cause:**  
You’re trying to assume a role with a misconfigured or overly strict trust policy.

**✅ Solution:**

- Confirm the `Principal` is defined correctly in the trust policy.
- Ensure you are using the **correct ARN** of the IAM user or role.

Example:
```json
"Principal": {
  "AWS": "arn:aws:iam::<Account-B-ID>:user/cross-user"
}
```

---

### 🛠️ 3. **MFA requirement not fulfilled**

**❓ Cause:**  
Trust policy includes MFA, but your `assume-role` command does not pass MFA session.

**✅ Solution:**

Use the following CLI with `--serial-number` and `--token-code`:

```bash
aws sts assume-role \
  --role-arn arn:aws:iam::<Account-A-ID>:role/CrossAccountAccessRole \
  --role-session-name crosssession \
  --serial-number arn:aws:iam::<Account-B-ID>:mfa/your-user-name \
  --token-code 123456
```

---

### 🛠️ 4. **Role assumed successfully, but access denied for AWS resources**

**❓ Cause:**  
Role has been assumed, but the **permissions policy** attached to the role doesn’t allow access to target services like S3, EC2, etc.

**✅ Solution:**

- Attach a policy to the role with the necessary permissions.
- Test using CLI:
  ```bash
  aws s3 ls
  ```

---

### 🛠️ 5. **Can’t find the Role when trying to assume it**

**❓ Cause:**  
Role might not exist in the trusted account, or the ARN is incorrect.

**✅ Solution:**

- Double-check the role ARN.
- Verify the role is created in Account A.
- Use:
  ```bash
  aws iam list-roles
  ```

---

### 🛠️ 6. **Trust Policy says 'Invalid Principal'**

**❓ Cause:**  
You deleted the user/role from Account B, but it’s still referenced in the trust policy of Account A.

**✅ Solution:**

- Update trust policy with the correct active user/role ARN.
- Use **IAM Access Analyzer** to validate.

---

### 🛠️ 7. **No CloudTrail logging for AssumeRole**

**❓ Cause:**  
CloudTrail not enabled, or you’re not filtering the `AssumeRole` API calls.

**✅ Solution:**

- Enable CloudTrail.
- Search for the event name `AssumeRole`.
- Use CloudTrail Insights to detect abnormal assume role behavior.

---

### 🛠️ 8. **CLI role switch working, but Management Console not allowing login**

**❓ Cause:**  
You're missing the correct session duration or not generating a temporary link/token for console login.

**✅ Solution:**

Use the federation endpoint:
```bash
https://signin.aws.amazon.com/switchrole
```

Or use STS federation URL after generating temporary credentials.

---
