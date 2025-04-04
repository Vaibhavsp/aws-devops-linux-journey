## ⚙️ Hands-on CLI Commands for Access Keys & MFA Setup

---

### 🔑 Access Key Management

#### ✅ 1. Create Access Key

```bash
aws iam create-access-key --user-name <your-username>
```

#### ✅ 2. List Access Keys

```bash
aws iam list-access-keys --user-name <your-username>
```

#### ✅ 3. Delete Access Key

```bash
aws iam delete-access-key \
  --user-name <your-username> \
  --access-key-id <access-key-id>
```

#### ✅ 4. Update Access Key Status (Activate/Inactive)

```bash
aws iam update-access-key \
  --user-name <your-username> \
  --access-key-id <access-key-id> \
  --status Inactive
```

---

### 🔐 MFA (Multi-Factor Authentication)

#### ✅ 5. List MFA Devices

```bash
aws iam list-mfa-devices --user-name <your-username>
```

#### ✅ 6. Enable Virtual MFA Device

```bash
# Step 1: Create virtual MFA device
aws iam create-virtual-mfa-device \
  --virtual-mfa-device-name <device-name> \
  --outfile QR.png \
  --bootstrap-method QRCodePNG

# Step 2: Associate it with user
aws iam enable-mfa-device \
  --user-name <your-username> \
  --serial-number arn:aws:iam::<account-id>:mfa/<device-name> \
  --authentication-code1 123456 \
  --authentication-code2 654321
```

💡 You can scan the generated QR with the **Google Authenticator** app.

#### ✅ 7. Deactivate MFA

```bash
aws iam deactivate-mfa-device \
  --user-name <your-username> \
  --serial-number arn:aws:iam::<account-id>:mfa/<device-name>
```

#### ✅ 8. Delete Virtual MFA Device

```bash
aws iam delete-virtual-mfa-device \
  --serial-number arn:aws:iam::<account-id>:mfa/<device-name>
```

---

### ✅ Setup CLI Profile with MFA Auth

```bash
aws configure --profile mfa-user
```

Then:

```bash
aws sts get-session-token \
  --serial-number arn:aws:iam::<account-id>:mfa/<device-name> \
  --token-code <mfa-token>
```

Store the credentials returned to a **named profile** for secure use!

---

📌 CLI is super useful for automation, scripting, and remote access tasks.  
