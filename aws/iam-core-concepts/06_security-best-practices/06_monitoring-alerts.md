# 🚨 IAM Monitoring & Alerts

To maintain a secure AWS environment, it’s crucial to monitor IAM-related activities in real-time and receive alerts for suspicious behavior.

---

## ✅ What to Monitor?

| What | Why |
|------|-----|
| IAM User logins | Detect unauthorized access |
| API calls like `CreateUser`, `DeletePolicy` | Track changes to IAM setup |
| Root account activity | Highly sensitive |
| Usage of access keys | Spot misuse or exposed credentials |
| Failed login attempts | Possible brute force attempts |

---

## 🛠️ Tools Used

- **AWS CloudTrail**: Logs all API calls
- **AWS CloudWatch**: Monitor events & set alarms
- **SNS (Simple Notification Service)**: Send alerts to email or Lambda
- **AWS Config**: Track configuration changes

---

## 🎯 How to Set Up Monitoring

### 1. **Enable CloudTrail**
Logs all IAM activity (like creating roles, attaching policies)

```bash
aws cloudtrail create-trail --name my-trail --s3-bucket-name my-logs-bucket
aws cloudtrail start-logging --name my-trail
```

### 2. **Create Metric Filters in CloudWatch**

Filter for unauthorized attempts:

```bash
aws logs put-metric-filter \
  --log-group-name "/aws/cloudtrail/logs" \
  --filter-name "FailedLogin" \
  --filter-pattern '{($.eventName = ConsoleLogin) && ($.errorMessage = "Failed authentication")}' \
  --metric-transformations \
    metricName=FailedLoginAttempts,metricNamespace=IAMMonitoring,metricValue=1
```

### 3. **Set Alarms and Alerts**

Attach an SNS topic to send email when the metric breaches the threshold:

```bash
aws sns create-topic --name IAMAlerts
aws sns subscribe --topic-arn arn:aws:sns:region:account-id:IAMAlerts --protocol email --notification-endpoint your@email.com
```

---

## 📌 Real-time Project Use

- Notify admin team if a new IAM user is created unexpectedly
- Detect access key usage anomalies
- Monitor S3 bucket permission changes triggered by IAM actions

---

## 🔍 Bonus:

- Use **Athena** to query CloudTrail logs for IAM activity
- Connect with **GuardDuty** for detecting malicious IAM usage

---
