## 🔐 Enable MFA for User (Advanced – done via console mostly)

### ✅ 4. `json-policies/read-only-policy.json`

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:Get*",
        "s3:List*"
      ],
      "Resource": "*"
    }
  ]
}
