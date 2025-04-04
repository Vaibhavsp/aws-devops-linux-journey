## 🧰 07_troubleshooting.md – MFA & Access Keys Issues

---

### 🚨 Common Issues and Fixes with MFA & Access Keys

---

### ❌ 1. **Access Key Not Working (Invalid Access Key ID / Signature Error)**

#### 🔍 Cause:
- Key is inactive
- Key is deleted
- Wrong key used in config
- Clock skew between system and AWS

#### ✅ Fix:
- Run:  
  ```bash
  aws iam list-access-keys --user-name <username>
  ```
- Check key status (`Active/Inactive`)
- Sync system time (`sudo ntpdate pool.ntp.org`)
- Update correct key in credentials file:
  ```bash
  nano ~/.aws/credentials
  ```

---

### ❌ 2. **"MFA token required" Error While Using AWS CLI**

#### 🔍 Cause:
- User has policy that enforces MFA, but MFA token wasn’t provided

#### ✅ Fix:
- Generate a session token with MFA:
  ```bash
  aws sts get-session-token \
    --serial-number arn:aws:iam::<account-id>:mfa/<username> \
    --token-code <6-digit-mfa-code>
  ```

- Use the returned temporary credentials (Access Key, Secret, Session Token)

---

### ❌ 3. **Can’t See “Create Access Key” Option**

#### 🔍 Cause:
- You’re trying to create an access key for yourself but don’t have required permissions.

#### ✅ Fix:
- Attach this policy to your user:
  ```json
  {
    "Effect": "Allow",
    "Action": "iam:CreateAccessKey",
    "Resource": "arn:aws:iam::*:user/${aws:username}"
  }
  ```

---

### ❌ 4. **Too Many Access Keys Created**

#### 🔍 Cause:
- A user can have **max 2 access keys**

#### ✅ Fix:
- Use:
  ```bash
  aws iam list-access-keys --user-name <username>
  ```
- Then delete one:
  ```bash
  aws iam delete-access-key --access-key-id <key-id>
  ```

---

### ❌ 5. **Accidentally Deleted Secret Access Key**

#### 🔍 Cause:
- Secret key is not recoverable once lost

#### ✅ Fix:
- Create a new key:
  ```bash
  aws iam create-access-key --user-name <username>
  ```
- Delete old one if no longer used

---

### ❌ 6. **CLI Still Using Old Credentials After Rotation**

#### 🔍 Cause:
- CLI credentials not updated after key rotation

#### ✅ Fix:
- Update `~/.aws/credentials` file manually  
  OR use:
  ```bash
  aws configure
  ```

---

### ❌ 7. **Access Denied When Calling STS with MFA**

#### 🔍 Cause:
- IAM Policy doesn't allow `sts:GetSessionToken`

#### ✅ Fix:
- Add this policy to user or group:
  ```json
  {
    "Effect": "Allow",
    "Action": "sts:GetSessionToken",
    "Resource": "*"
  }
  ```

---

### 🧠 Pro Tip

Use [IAM Policy Simulator](https://policysim.aws.amazon.com/) to test your policies and access.

---
