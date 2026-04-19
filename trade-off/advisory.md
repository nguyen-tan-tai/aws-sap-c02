# 🔐 AWS Advisory & Related Services Comparison

| Service | Category | Primary Use Case | What It Does | When to Use | When NOT to Use |
|--------|----------|------------------|--------------|-------------|------------------|
| AWS Trusted Advisor | Advisory | Best practice recommendations | Checks for cost, security, performance, fault tolerance issues | Improve overall AWS posture quickly | Not real-time monitoring or enforcement |
| AWS Security Hub | Security Ops | Centralize security findings | Aggregates alerts from GuardDuty, Inspector, etc. | Unified security dashboard | Not for recommendations or architecture advice |
| AWS Config | Compliance | Track & enforce configuration | Evaluates resources against rules | Ensure compliance (e.g., no public S3) | Not recommendation-based |
| AWS Well-Architected Tool | Advisory | Architecture review | Evaluates workloads against best practices (pillars) | Review system design quality | Not continuous monitoring |
| AWS Compute Optimizer | Optimization | Resource right-sizing | Recommends optimal compute resources | Optimize cost/performance | Not security-focused |
| AWS Cost Explorer | Cost | Cost analysis | Visualize and analyze AWS spending | Track cost trends | Not security or compliance |
| AWS Audit Manager | Compliance | Automate audit process | Collects evidence for audits | Prepare compliance reports | Not real-time monitoring |
| AWS Artifact | Compliance | Access audit reports | Provides AWS compliance documents (SOC, ISO) | Download audit certifications | Not for enforcement or detection |


# 🌳 AWS Security + Advisory Decision Tree

## 1. What is your goal?

---

### 🔴 Prevent an attack
- HTTP/HTTPS attack (SQLi, XSS, bots)?
  → AWS WAF
- Large-scale DDoS (L3/L4)?
  → AWS Shield / Shield Advanced
- Need network filtering inside VPC?
  → AWS Network Firewall
- Enforce rules across multiple accounts?
  → AWS Firewall Manager

---

### 🟡 Detect threats / risks
- Suspicious activity (API abuse, crypto mining)?
  → Amazon GuardDuty
- Vulnerabilities (CVE, packages)?
  → Amazon Inspector
- Sensitive data exposure (PII in S3)?
  → Amazon Macie

---

### 🔵 Monitor / Audit
- Who did what (API logs)?
  → AWS CloudTrail
- Resource configuration / compliance drift?
  → AWS Config
- Metrics / logs / alarms?
  → Amazon CloudWatch

---

### 🟣 Investigate / Aggregate
- Central security dashboard?
  → AWS Security Hub
- Investigate incidents deeply?
  → Amazon Detective

---

### 🟢 Governance / Multi-account
- Fine-grained permissions?
  → AWS IAM
- Multi-account governance (SCP)?
  → AWS Organizations
- Quick secure landing zone setup?
  → AWS Control Tower
- Enforce security policies across accounts?
  → AWS Firewall Manager

---

### ⚫ Data protection
- Encryption keys?
  → AWS KMS
- Secrets with rotation?
  → AWS Secrets Manager
- Simple config / secrets?
  → SSM Parameter Store

---

### ⚪ Compliance / Audit support
- Need compliance reports (SOC, ISO)?
  → AWS Artifact
- Automate audit evidence collection?
  → AWS Audit Manager

---

### 🟠 Advisory / Optimization (⚠️ NOT enforcement)
- General best practice recommendations?
  → AWS Trusted Advisor
- Architecture review (Well-Architected pillars)?
  → AWS Well-Architected Tool
- Resource right-sizing (EC2, Lambda)?
  → AWS Compute Optimizer
- Cost analysis and trends?
  → AWS Cost Explorer

---

## ⚡ Fast elimination rules

- “Recommend / suggest improvements” → Trusted Advisor  
- “Review architecture design” → Well-Architected Tool  
- “Enforce compliance” → Config  
- “Centralize security findings” → Security Hub  
- “Detect threats” → GuardDuty  
- “Block traffic” → WAF / Shield  
- “Optimize cost/performance” → Compute Optimizer  