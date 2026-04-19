# 🔐 AWS Security Services Comparison (More Complete + Usage Guidance)

| Service | Category | Primary Use Case | What It Protects | How It Works | Typical Scenario | When to Use | When NOT to Use |
|--------|----------|------------------|------------------|--------------|------------------|-------------|------------------|
| AWS WAF | Prevent | Block malicious HTTP requests | Web apps (L7) | Rule-based filtering | Stop SQL injection / bots | When you need HTTP filtering, bot control, rate limiting | Not for L3/L4 DDoS or non-HTTP traffic |
| AWS Shield | Prevent | DDoS protection | Network (L3/4) | Traffic absorption | Handle SYN flood | Default protection for all AWS apps | Not for application-layer filtering |
| AWS Shield Advanced | Prevent | Advanced DDoS | Critical apps | DRT + cost protection | Enterprise workloads | High-value apps needing SLA + cost protection | Not needed for small/simple apps |
| AWS Network Firewall | Prevent | Network-level filtering | VPC traffic | Stateful firewall rules | Control east-west traffic | Need deep packet inspection inside VPC | Not for HTTP-specific filtering (use WAF) |
| AWS Firewall Manager | Control | Central policy enforcement | Multi-account | Apply WAF/Shield rules | Org-wide firewall control | Enforce security across accounts | Not needed for single account setups |
| Amazon GuardDuty | Detect | Threat detection | Account/VPC | ML on logs | Detect compromised IAM | Detect anomalies without manual rules | Not for prevention or blocking |
| Amazon Inspector | Detect | Vulnerability scan | EC2/ECR/Lambda | CVE scanning | Find outdated packages | Scan workloads for vulnerabilities | Not for runtime threat detection |
| Amazon Macie | Detect | Sensitive data discovery | S3 | ML classification | Detect PII exposure | Protect sensitive data in S3 | Not for non-S3 data |
| AWS Detective | Investigate | Analyze incidents | Security logs | Graph correlation | Investigate GuardDuty findings | Deep investigation of alerts | Not for real-time detection |
| AWS Security Hub | Aggregate | Central findings | Whole environment | Aggregates alerts | Single dashboard | Centralize security posture | Not a detection or prevention tool |
| AWS Config | Monitor | Config tracking | Resources | Rules + snapshots | Detect public S3 | Compliance & drift detection | Not for real-time logging |
| AWS CloudTrail | Monitor | API audit | Account | Logs API calls | Track user actions | Audit “who did what” | Not for config state tracking |
| Amazon CloudWatch | Monitor | Metrics/logs | Infra/apps | Alerts + logs | Detect anomalies | Monitor system health | Not for security-specific detection |
| AWS IAM | Control | Access control | Users/roles | Policies | Least privilege | Manage permissions | Not for org-wide restriction (use SCP) |
| AWS Organizations | Control | Multi-account governance | Accounts | SCPs | Restrict services | Control accounts centrally | Not for resource-level permissions |
| AWS Control Tower | Control | Landing zone setup | Accounts | Guardrails + automation | Secure multi-account setup | Quick secure multi-account setup | Not for fine-grained policy control |
| AWS KMS | Protect | Encryption keys | Data | Manage CMKs | Encrypt storage | Manage encryption centrally | Not for storing secrets directly |
| AWS Secrets Manager | Protect | Secret management | Credentials | Rotation | Store DB passwords | Need automatic rotation | Overkill for simple configs |
| AWS Systems Manager Parameter Store | Protect | Config & secrets | App configs | Secure storage | Store API keys | Simple, low-cost secret storage | Not for automatic rotation |
| Amazon Cognito | Identity | App authentication | Users | User pools | Login system | User authentication for apps | Not for IAM-based access |
| AWS Directory Service | Identity | AD integration | Enterprise users | Managed AD | Windows auth | Need AD integration | Not for simple app auth |
| AWS Artifact | Compliance | Audit reports | Docs | Provides certs | SOC/ISO download | Need compliance documents | Not for enforcing compliance |
| AWS Audit Manager | Compliance | Automate audits | Compliance data | Evidence collection | Prepare audits faster | Automate audit workflows | Not for real-time monitoring |


# 🌳 AWS Security Services Decision Tree

## 1. What is the goal?

### 🔴 Prevent an attack
- Is it HTTP/HTTPS (Layer 7)?
  → Use **AWS WAF**
- Is it large-scale DDoS (Layer 3/4)?
  → Use **AWS Shield** (or Shield Advanced)
- Need network filtering inside VPC?
  → Use **AWS Network Firewall**
- Need to enforce rules across multiple accounts?
  → Use **AWS Firewall Manager**

---

### 🟡 Detect threats or vulnerabilities
- Suspicious activity / anomaly (API abuse, crypto mining)?
  → Use **Amazon GuardDuty**
- Vulnerabilities (CVE, outdated packages)?
  → Use **Amazon Inspector**
- Sensitive data exposure (PII in S3)?
  → Use **Amazon Macie**

---

### 🔵 Monitor / Audit
- Who did what (API activity)?
  → Use **AWS CloudTrail**
- Resource configuration / compliance drift?
  → Use **AWS Config**
- Metrics, logs, alarms?
  → Use **Amazon CloudWatch**

---

### 🟣 Investigate / Aggregate
- Central security dashboard?
  → Use **AWS Security Hub**
- Investigate incidents deeply?
  → Use **Amazon Detective**

---

### 🟢 Identity & Access Control
- Fine-grained permissions?
  → Use **AWS IAM**
- Multi-account governance?
  → Use **AWS Organizations**
- Quick secure multi-account setup?
  → Use **AWS Control Tower**

---

### ⚫ Data Protection
- Encryption keys?
  → Use **AWS KMS**
- Secrets with rotation?
  → Use **AWS Secrets Manager**
- Simple config/secret storage?
  → Use **SSM Parameter Store**

---

### ⚪ Compliance / Audit Support
- Download compliance reports?
  → Use **AWS Artifact**
- Automate audit evidence collection?
  → Use **AWS Audit Manager**

---

## ⚡ Fast Elimination Rules (SAP Exam)

- DDoS → **Shield**, NOT WAF  
- HTTP attack → **WAF**, NOT Shield  
- Threat detection → **GuardDuty**, NOT Inspector  
- Vulnerability scan → **Inspector**, NOT GuardDuty  
- API logging → **CloudTrail**, NOT Config  
- Config drift → **Config**, NOT CloudTrail  
- Multi-account setup → **Control Tower**, NOT IAM  
- Cross-account enforcement → **Firewall Manager**

---

## 🧠 Memory Trick

- **Prevent** → WAF, Shield  
- **Detect** → GuardDuty, Inspector, Macie  
- **Monitor** → CloudTrail, Config, CloudWatch  
- **Control** → IAM, Organizations, Control Tower  
- **Protect Data** → KMS, Secrets Manager  
- **Govern** → Firewall Manager, Security Hub  