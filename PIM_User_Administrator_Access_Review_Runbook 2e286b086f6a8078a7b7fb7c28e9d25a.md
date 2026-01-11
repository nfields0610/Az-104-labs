# PIM_User_Administrator_Access_Review_Runbook

# 🛡️ Runbook: PIM – User Administrator Access Review (Monthly)

## Lab Purpose

Establish a **recurring access review** for a privileged group to prevent **privilege creep**, enforce **least privilege**, and demonstrate **Identity Governance + PIM integration** in Microsoft Entra ID.

---

## Scope

- **Resource Type:** Entra ID Group
- **Group:** `PIM-User-Administrator-Lab`
- **Review Scope:** Guest users only
- **Review Cadence:** Monthly
- **Reviewers:** Users review their own access
- **Automation:** Enabled (auto-apply results)

---

## Step 1: Create Access Review

**Path:**

`Microsoft Entra Admin Center → Identity Governance → Access reviews → New access review`

**Template Selected:**

- Review access to a resource type

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image.jpeg)

---

## Step 2: Select Resource (Group)

- Resource type: **Groups**
- Selected group: **PIM-User-Administrator-Lab**
- Scope: **Guest users only**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%201.jpeg)

---

## Step 3: Configure Reviewers

**Reviewer Configuration:**
- Users review their own

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%202.jpeg)

**Why this matters:**
- Enables self-attestation
- Reduces administrative overhead
- Common enterprise governance pattern

---

## Step 4: Configure Recurrence

- Review duration: **3 days**
- Frequency: **Monthly**
- Start date: **01/07/2026**
- End: **No end date**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%203.jpeg)

---

## Step 5: Configure Review Settings

### Upon Completion

- Auto-apply results to resource: **Enabled**
- If reviewers don’t respond: **Remove access**
- Action on denied guest users: **Remove group membership**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%204.jpeg)

### Decision Helpers

- No sign-in within 30 days: **Enabled**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%205.jpeg)

### Advanced Settings

- Justification required: **Enabled**
- Email notifications: **Enabled**
- Reminders: **Enabled**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%206.jpeg)

---

## Step 6: Review + Create

- Review configuration summary
- Click **Create**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%207.jpeg)

---

## Step 7: Access Review Created Successfully

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%208.jpeg)

---

## Step 8: Validation & Review Overview

### Observed Status

- Review Status: **Active**
- Instance Status: **Complete**
- Warning: **No access to review**

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%209.jpeg)

### Explanation

This warning is **expected behavior** because:
- Review scope is **Guest users only**
- The group currently contains **zero guest users**
- No identities exist to evaluate

This does **not** indicate a configuration error.

---

## Step 9: Identity Governance Validation

![image.jpeg](PIM_User_Administrator_Access_Review_Runbook/image%2010.jpeg)

---

## Optional Extension (Not Required)

To generate review items:
1. Add a guest user to `PIM-User-Administrator-Lab`
2. Wait for the next review cycle or manually start a review

---

## Key Learning Outcome

Successfully implemented a **monthly automated access review** for a privileged group using Microsoft Entra ID Identity Governance to reduce privilege creep and enforce least-privilege access.

---

## Lab Status

**Complete ✅**