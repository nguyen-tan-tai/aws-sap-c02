# 🌳 AWS Master Decision Tree (Security + Advisory + Governance)

## 1. What is your goal?

---

### 🔴 Prevent an attack (BLOCK traffic)
- HTTP/HTTPS attack (SQLi, XSS, bots)?
  → AWS WAF
- Large-scale DDoS (L3/L4)?
  → AWS Shield / Shield Advanced
- Network filtering inside VPC (east-west, deep inspection)?
  → AWS Network Firewall
- Enforce WAF/Shield rules across accounts?
  → AWS Firewall Manager

---

### 🟡 Detect threats / risks (FIND issues)
- Suspicious activity (API abuse, crypto mining)?
  → Amazon GuardDuty
- Vulnerabilities (CVE, outdated packages)?
  → Amazon Inspector
- Sensitive data exposure (PII in S3)?
  → Amazon Macie

---

### 🔵 Monitor / Audit (SEE what happened)
- Who did what (API calls)?
  → AWS CloudTrail
- Resource configuration / compliance drift?
  → AWS Config
- Metrics / logs / alarms?
  → Amazon CloudWatch

---

### 🟣 Investigate / Aggregate (UNDERSTAND incidents)
- Central security dashboard (multi-service findings)?
  → AWS Security Hub
- Deep investigation / root cause analysis?
  → Amazon Detective

---

### 🟢 Identity & Governance (CONTROL access & accounts)
- Fine-grained permissions (users, roles)?
  → AWS IAM
- Multi-account governance (SCPs)?
  → AWS Organizations
- Secure multi-account setup (landing zone)?
  → AWS Control Tower
- Enforce security policies across accounts?
  → AWS Firewall Manager

---

### ⚫ Data protection (PROTECT data)
- Encryption keys?
  → AWS KMS
- Secrets with automatic rotation?
  → AWS Secrets Manager
- Simple config / secrets (low cost)?
  → SSM Parameter Store

---

### ⚪ Compliance / Audit (PROVE compliance)
- Need compliance reports (SOC, ISO)?
  → AWS Artifact
- Automate audit evidence collection?
  → AWS Audit Manager

---

### 🟠 Advisory / Optimization (⚠️ RECOMMEND only)
- General best practice checks (cost, security, fault tolerance)?
  → AWS Trusted Advisor
- Architecture review (Well-Architected pillars)?
  → AWS Well-Architected Tool
- Resource right-sizing (EC2, Lambda)?
  → AWS Compute Optimizer
- Cost analysis and trends?
  → AWS Cost Explorer

---

## ⚡ 10-Second Elimination Rules

- BLOCK traffic → WAF / Shield / Network Firewall  
- DETECT threats → GuardDuty  
- SCAN vulnerabilities → Inspector  
- FIND sensitive data → Macie  
- WHO did what → CloudTrail  
- CONFIG drift → Config  
- CENTRAL dashboard → Security Hub  
- INVESTIGATE → Detective  
- PERMISSIONS → IAM  
- MULTI-account → Organizations / Control Tower  
- ENFORCE org-wide → Firewall Manager  
- ENCRYPT → KMS  
- SECRETS → Secrets Manager / Parameter Store  
- COMPLIANCE docs → Artifact  
- AUDIT automation → Audit Manager  
- RECOMMEND only → Trusted Advisor / Well-Architected  