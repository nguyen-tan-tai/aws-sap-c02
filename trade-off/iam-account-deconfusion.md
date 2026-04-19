# 🧠 AWS SAP Question Deconfusion Guide (How to Stop Getting Tricked)

---

## 🔑 1. Always use the 4-step parsing checklist

Before looking at answers, extract ONLY facts:

### Step 1 — Identity
- Who are the users?
- Is there a requirement for single credentials?

👉 If YES:
- Think central identity (IAM Identity Center)

---

### Step 2 — Accounts
- How many AWS accounts exist?
- Which account owns the resources?

👉 Rule:
> Resources always belong to their own account

---

### Step 3 — Permission split
- Who can access what?

Example:
- Dev → dev only
- Ops → dev + prod

👉 This signals:
- Role-based or cross-account access

---

### Step 4 — Access type
Ask:
- Do users access another account?

👉 If YES:
- Use AssumeRole pattern
- NOT duplicated users

---

## ⚡ 2. Ignore story wording (very important)

AWS uses distracting labels:
- “development team”
- “operations team”

👉 Replace mentally with:

User A → limited access  
User B → extended access  

👉 Focus on permissions, not job titles

---

## 🚫 3. Instant elimination rules (high value)

### If question says:
“single set of credentials”
❌ Eliminate:
- Users in multiple accounts
- Duplicated IAM users

---

### If question says:
“access another AWS account”
✔️ Choose:
- AssumeRole (cross-account access)

---

### If question says:
“centralized management across accounts”
Think:
- AWS Organizations
- AWS Control Tower

---

## 🧩 4. Convert question into pattern

| Pattern | Correct AWS Solution |
|--------|----------------------|
| Single login + multi account | IAM Identity Center |
| Cross-account access | IAM Role (AssumeRole) |
| Org-wide restriction | SCP (Organizations) |
| Fine-grained access | IAM policies |
| Multi-account setup | Control Tower |

---

## 🧠 5. One-line simplification trick

Rewrite every question as:

> Who needs access to what across which accounts?

Then ignore everything else.

---

## ⚡ 6. Mental model (very important)

Users → Roles → Target Account Resources

NOT:

Users duplicated across accounts ❌

---

## 🔥 7. Final exam survival rule

If you see:
- multiple accounts
- single credentials

👉 Always assume:
- central identity
- cross-account roles

---

## 🧭 8. Golden AWS principle

- Users belong to identity system  
- Resources belong to accounts  
- Access happens via roles