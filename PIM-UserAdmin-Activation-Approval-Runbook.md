# Lab Walkthrough: PIM Role Activation + Approval (User Administrator scoped to an Admin Unit)

> **Scenario (story-based):**  
You’re operating a small-but-growing tenant (HX) and you want **least-privilege** administration. Instead of giving permanent User Administrator rights, you use **Privileged Identity Management (PIM)** so admins elevate **just-in-time** and (optionally) require **approval** before the role becomes active.  
In this run, the user **AU-Test** has an **eligible** assignment for **User Administrator** scoped to an **Administrative Unit** (example: `Az-104-IT-AU`). The user requests activation, an approver reviews it, and the role becomes **Activated** for a limited window.

---

## What you accomplished (high level)

- Requested **PIM activation** for **User Administrator**
- Triggered an **approval workflow**
- Approved the request as the approver
- Verified the role moved from **Eligible** → **Active (Activated)**
- Confirmed the role is **scoped to an Administrative Unit** (not tenant-wide)

---

## Prerequisites / assumptions

- Microsoft Entra ID **PIM** is available (Entra ID P2 / Microsoft 365 E5 / equivalent licensing).
- A user (example: `AU-Test`) is assigned **Eligible** for:
  - **Role:** User Administrator  
  - **Scope:** Administrative Unit (example: `Az-104-IT-AU`)
  - **Activation:** requires **approval** (and may require MFA/justification)
- You have an approver account (or role) that can approve PIM activation requests.

> **Cost note:** PIM typically requires P2 licensing. In labs, this may be via trial or bundled licensing.

---

## Evidence / screenshots to include

Add these images to your repo (example path: `./images/`) and replace filenames below:

- `01-activate-pane.png`  *(activation pane with reason + duration slider)*
- `02-pending-approval-toast.png`
- `03-active-assignments-empty.png`
- `04-approve-requests-list.png`
- `05-approve-selected.png`
- `06-approved-toast.png`
- `07-active-assignments-activated.png`

---

# Step-by-step (with the “meta layer”)

## Step 1 — Navigate to PIM > My roles and start activation

**Path:** Microsoft Entra admin center → **Identity Governance** → **Privileged Identity Management** → **My roles** → *Microsoft Entra roles*  
Under **Eligible assignments**, locate **User Administrator** (scoped to your Admin Unit) and click **Activate**.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/cea20deb-9821-449e-9733-887a84d0d5fe" />


### Meta layer
- **Core decision practice:** *Just-in-time elevation* instead of permanent admin rights.
- **Risk / failure mode addressed:** Standing privileges are a top cause of identity compromise impact (attackers love permanent admin access).
- **Business / human impact:** Reduces blast radius; fewer “keys to the kingdom” floating around. Safer operations without slowing work too much.
- **Transferable insight:** When you can’t remove admin work, remove **always-on admin**. Use JIT + scope.

---

## Step 2 — Configure the activation request (duration + justification)

In the **Activate – User Administrator** pane:
1. Set **Duration (hours)** (example: 1 hour).
2. Enter a clear **Reason** (max 500 chars). Example:
   - “Lab admin tasks: create/update users in Az-104-IT-AU, validate group membership, and review sign-in activity.”
3. Click **Activate**.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/99d614e2-4255-4071-9581-51011f0e3329" />


### Meta layer
- **Core decision practice:** *Time-boxing* + *explicit justification*.
- **Risk / failure mode addressed:** “Privilege creep” (roles left active too long) and audit ambiguity (“why did we elevate?”).
- **Business / human impact:** Faster incident review, cleaner audits, and less stress when you have to explain actions later.
- **Transferable insight:** Write reasons like you’re helping your future self (or an auditor) understand intent in 10 seconds.

---

## Step 3 — Confirm the request is pending approval

After submitting, you should see a notification/toast like:
> “Your request is pending for approval…”

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/3a81253c-80a1-4139-8bb5-4b39bf252c1d" />


Optional check:
- In **My roles**, click **Active assignments**.  
  If approval is required, the role may **not** appear as active yet.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/f55570a2-dfcf-47f4-8a01-2c083474914c" />


### Meta layer
- **Core decision practice:** *Expectation management*—approval gating is working as designed.
- **Risk / failure mode addressed:** Assuming access is active and performing changes without the right permissions (leads to errors, lockouts, or misconfig).
- **Business / human impact:** Prevents accidental unauthorized changes; enforces separation of duties.
- **Transferable insight:** If access is gated, build “verify activation status” into your workflow before admin actions.

---

## Step 4 — Switch to the approver view: Approve requests

Sign in as the approver (or switch role/account), then go to:

**Path:** Privileged Identity Management → **Approve requests** (Microsoft Entra roles)

Look under **Requests for role activations** and locate the request:
- **Role:** User Administrator  
- **Requestor:** AU-Test  
- **Resource:** `Az-104-IT-AU`  
- **Resource type:** AdministrativeUnit

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/f2931374-f103-49fc-a2cd-07d666ede5b8" />


### Meta layer
- **Core decision practice:** *Separation of duties* (requestor ≠ approver).
- **Risk / failure mode addressed:** Single-person control over privileged access (fraud, mistakes, or compromised accounts).
- **Business / human impact:** Stronger governance; builds trust that admin elevation is reviewed.
- **Transferable insight:** Even in small orgs, approval workflows create an audit trail that scales with you.

---

## Step 5 — Approve the activation request

1. Select the request checkbox.
2. Click **Approve**.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/a9675c6c-dc8a-415e-8818-b3fc21cf075b" />


You should see confirmation that the request is approved.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/f1e572d2-5ded-4c0e-9eeb-1663600d06b5" />


### Meta layer
- **Core decision practice:** *Explicit authorization* of privileged action.
- **Risk / failure mode addressed:** Approving the wrong scope/role or approving without context.
- **Business / human impact:** The approver acts as a safety net—catching mis-scoped requests before privileges go live.
- **Transferable insight:** Approvers should sanity-check: **role**, **scope**, **duration**, **reason**. Fast doesn’t mean careless.

---

## Step 6 — Verify activation is now active (Activated)

Return to the requestor account (`AU-Test`) and refresh:

**Path:** PIM → My roles → **Active assignments**

You should now see:
- **Role:** User Administrator  
- **Scope:** `Az-104-IT-AU`  
- **State:** **Activated**  
- **End time:** (timestamp based on duration)  
- **Action:** Deactivate (optional)

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/4e033b26-be54-4235-af69-ffd3939dbb10" />


### Meta layer
- **Core decision practice:** *Close the loop*—verify access before you start admin work.
- **Risk / failure mode addressed:** Confusing “eligible” with “active,” or proceeding with partial permissions.
- **Business / human impact:** Less wasted time troubleshooting permission errors; fewer support escalations.
- **Transferable insight:** Always confirm the **state** and **scope** of privilege before changes (especially in production).

---

## Step 7 — Perform the scoped admin task (example)

Now that the role is active, perform the minimum required tasks inside the **Administrative Unit** scope, for example:
- Create a test user in `Az-104-IT-AU`
- Reset a password for a user *within the AU*
- Update group membership inside the AU

> If you try to admin objects **outside** the AU, you may be blocked—this is *good* and confirms scoping works.

### Meta layer
- **Core decision practice:** *Least privilege + scoped administration*.
- **Risk / failure mode addressed:** Tenant-wide impact from routine admin tasks (accidental edits across the entire directory).
- **Business / human impact:** Safer identity operations, fewer tenant-wide outages or mistakes.
- **Transferable insight:** Scope is a superpower—Admin Units let you delegate safely without over-granting.

---

## Step 8 — Deactivate (optional but recommended)

When finished, go back to **Active assignments** and click **Deactivate** (or just let the timer expire).

### Meta layer
- **Core decision practice:** *Privilege hygiene*.
- **Risk / failure mode addressed:** Forgetting elevated access is active (the “I’ll do it later” problem).
- **Business / human impact:** Reduces window of opportunity for attackers and mistakes.
- **Transferable insight:** End privileged sessions like you end SSH sessions—don’t leave them open.

---

# Core learning takeaways (quick summary)

- **Eligibility ≠ activation.** PIM is a two-step model: eligible → active.
- **Approval adds governance.** It slows you down by minutes, but saves you from major mistakes.
- **Scope matters.** Admin Unit scoping is how you delegate without tenant-wide risk.
- **Auditability is the real win.** Duration + reason + approval = clean story for reviewers.

---

## Optional “real-world” improvements (if you want to level this up)

- Require **MFA on activation**
- Use **ticketing integration** (change request number in justification)
- Create **access reviews** for eligible assignments
- Add alerts/workbooks to track:
  - activations by role
  - unusual activation times
  - repeated denials/approvals patterns

---

