### 🔸 Step-by-Step (AWS CLI):

#### 📝 Step 1: Create the Trust Policy (trust-policy.json)
```bash
cat > trust-policy.json <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

### 📝 Step 2: Create the IAM Role
```bash
aws iam create-role \
  --role-name EC2S3AccessRole \
  --assume-role-policy-document file://trust-policy.json
```

### 📝 Step 3: Attach S3 ReadOnlyAccess Policy
```bash
aws iam attach-role-policy \
  --role-name EC2S3AccessRole \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

### 🔍 Step 4: Attach the Role to an EC2 Instance
Get your instance ID:
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name]" --output table
```
Then attach the IAM role:
```bash
aws ec2 associate-iam-instance-profile \
  --instance-id i-xxxxxxxxxxxxxxx \
  --iam-instance-profile Name="EC2S3AccessRole"
```

## 🔐 Validation
### Verify on EC2:
### SSH into EC2 and run:
```bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/
```
You’ll see the role name and temporary credentials!

## 🚨 Cleanup (Optional)
```bash
aws iam detach-role-policy --role-name EC2S3AccessRole --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
aws iam delete-role --role-name EC2S3AccessRole
```
