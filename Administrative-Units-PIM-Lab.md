# AZ-104 Lab: Administrative Units with Privileged Identity Management (PIM)

## Overview
This lab demonstrates how to implement **Administrative Units (AUs)** in Microsoft Entra ID and apply **least-privilege, scoped administration** using **Privileged Identity Management (PIM)**.

The goal was to:
- Scope administrative permissions to a specific subset of users
- Assign roles using **Just-In-Time (JIT)** elevation
- Verify access boundaries by comparing **in-scope** vs **out-of-scope** users

This mirrors real-world enterprise identity governance practices.

---

## Lab Objectives
- Create an Administrative Unit
- Assign users to the Administrative Unit
- Assign a directory role scoped to the AU using PIM
- Activate the role using JIT access
- Validate scoped access and access denial

---

## Environment
- **Tenant:** Microsoft Entra ID
- **Role Used:** User Administrator
- **Security Feature:** Privileged Identity Management (PIM)
- **Scope Type:** Administrative Unit

---

## Step 1: Create an Administrative Unit
An Administrative Unit was created to logically group users for scoped administration.

- **Administrative Unit Name:** `Az-104-IT-AU`
- **Purpose:** Limit administrative control to a defined IT user scope

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/a080aabd-d242-45b1-bc18-a5563b60a4f2" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/635a6137-20b7-4cd7-aa25-9f1958c2854c" />


---

## Step 2: Add User to the Administrative Unit
A test user (`AU-Test`) was assigned to the Administrative Unit to simulate an in-scope identity.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/903e273c-1a6d-4369-a40e-bea0392df388" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/2e0b18d0-a296-4760-84b1-99f99e80ac7f" />



---

## Step 3: Assign Scoped Role Using Privileged Identity Management (PIM)
Using **Privileged Identity Management**, the **User Administrator** role was assigned:
- **Assignment Type:** Eligible
- **Scope:** Administrative Unit (`Az-104-IT-AU`)
- **Member:** `AU-Test`

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/ececd0eb-fc59-400d-874e-004a62e8f8fd" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/d58bbcb7-e8bf-4841-840c-fcdefcc14c6c" />


---

## Step 4: Activate Role (Just-In-Time Access)
The `AU-Test` user activated the **User Administrator** role through PIM:
- **Activation Duration:** 1 hour
- **Reason:** Temporary administrative configuration task

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/df3654cf-994c-461c-8ead-084daf2153fa" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/cde8971f-fdd2-4358-9fdc-d87626ce9527" />


---

## Step 5: Verify Active Role Assignment
Verification confirmed:
- Role is active
- Scope is limited to `Az-104-IT-AU`
- Assignment follows JIT and least-privilege principles

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/3c6d7876-ca07-4e95-8988-5f9e381dce2f" />


---

## Step 6: Validate Access Boundaries (Security Verification)

### In-Scope User
The `AU-Test` user can manage users **within** the Administrative Unit only.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/653613ef-4aab-4f0c-a3da-da7443a254d4" />


### Out-of-Scope User
A separate user (`Outside-AU`) confirms access is denied outside the AU scope.

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/519252d0-1ed7-4fcd-b009-e68d3ea51d18" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/32277b91-c84b-4c36-917f-bd0f591701d8" />


---

## Key Takeaways
- Administrative Units provide granular administrative scoping
- PIM enforces Just-In-Time access
- Scoped roles reduce lateral privilege exposure
- Aligns with Zero Trust and least-privilege models

---

## Enterprise Use Case
Administrative Units are used to:
- Delegate IT responsibilities by department or region
- Reduce blast radius of admin roles
- Support audit and compliance requirements
- Enforce identity governance at scale

---

## AZ-104 Exam Relevance
- Manage users and groups
- Implement role-based access control
- Apply identity governance best practices
- Understand Privileged Identity Management workflows

---

## Cleanup (Optional)
- Deactivate role assignment
- Remove test users
- Delete Administrative Unit if no longer required
