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

![image](https://github.com/user-attachments/assets/aca9da24-47fa-4956-a21a-df01cbf6a8d2)

---

## Step 3: Configure Reviewers

**Reviewer Configuration:**
- Users review their own

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/fcd80cc8-35a6-43e3-b577-73c77c6947ef" />

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

![image](https://github.com/user-attachments/assets/8145ffd6-44ef-4efc-a10c-ca21fb44fb88)

---

## Step 5: Configure Review Settings

### Upon Completion

- Auto-apply results to resource: **Enabled**
- If reviewers don’t respond: **Remove access**
- Action on denied guest users: **Remove group membership**

![image](https://github.com/user-attachments/assets/1f62393d-ce9f-471c-8383-59dfcfe5b4ce)


### Decision Helpers

- No sign-in within 30 days: **Enabled**

![image](https://github.com/user-attachments/assets/6c75009c-157f-42b8-a6b8-0cb889954278)


### Advanced Settings

- Justification required: **Enabled**
- Email notifications: **Enabled**
- Reminders: **Enabled**

![image](https://github.com/user-attachments/assets/3acc20d2-02d5-4eff-bb51-2deb82dcb160)

---

## Step 6: Review + Create

- Review configuration summary
- Click **Create**

![image](https://github.com/user-attachments/assets/91327aeb-a99c-4e54-bd8d-7dc9967bb457)

---

## Step 7: Access Review Created Successfully

![image](https://github.com/user-attachments/assets/9364d7b5-c0e2-4bcd-916f-de2a61a2712a)


---

## Step 8: Validation & Review Overview

### Observed Status

- Review Status: **Active**
- Instance Status: **Complete**
- Warning: **No access to review**

![image](https://github.com/user-attachments/assets/5066bfe8-ed99-4d47-94cd-d470069d56cf)


### Explanation

This warning is **expected behavior** because:
- Review scope is **Guest users only**
- The group currently contains **zero guest users**
- No identities exist to evaluate

This does **not** indicate a configuration error.

---

## Step 9: Identity Governance Validation

![image](https://github.com/user-attachments/assets/dd71eb94-9fdc-4b29-9584-bb6acc405cad)


---

## Optional Extension (Not Required)

To generate review items:
1. Add a guest user to `PIM-User-Administrator-Lab`
2. Wait for the next review cycle or manually start a review

---

## Key Learning Outcome

Successfully implemented a **monthly automated access review** for a privileged group using Microsoft Entra ID Identity Governance to reduce privilege creep and enforce least-privilege access.

---

