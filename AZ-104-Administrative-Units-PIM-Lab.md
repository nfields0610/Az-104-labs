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

![Create Administrative Unit](images/step1-create-au.png)
![Administrative Unit Created](images/step1-au-created.png)

---

## Step 2: Add User to the Administrative Unit
A test user (`AU-Test`) was assigned to the Administrative Unit to simulate an in-scope identity.

![User Added to Administrative Unit](images/step2-user-added-au.png)
![User Administrative Unit Membership](images/step2-user-au-membership.png)

---

## Step 3: Assign Scoped Role Using Privileged Identity Management (PIM)
Using **Privileged Identity Management**, the **User Administrator** role was assigned:
- **Assignment Type:** Eligible
- **Scope:** Administrative Unit (`Az-104-IT-AU`)
- **Member:** `AU-Test`

![PIM Role Assignment Scoped to AU](images/step3-pim-role-assignment.png)
![Role Assigned Successfully](images/step3-role-assigned.png)

---

## Step 4: Activate Role (Just-In-Time Access)
The `AU-Test` user activated the **User Administrator** role through PIM:
- **Activation Duration:** 1 hour
- **Reason:** Temporary administrative configuration task

![Activate Role in PIM](images/step4-activate-role.png)
![Role Activation Successful](images/step4-activation-success.png)

---

## Step 5: Verify Active Role Assignment
Verification confirmed:
- Role is active
- Scope is limited to `Az-104-IT-AU`
- Assignment follows JIT and least-privilege principles

![Active Role Verification](images/step5-active-role.png)

---

## Step 6: Validate Access Boundaries (Security Verification)

### In-Scope User
The `AU-Test` user can manage users **within** the Administrative Unit only.

![In-Scope User Access](images/step6-in-scope-access.png)

### Out-of-Scope User
A separate user (`Outside-AU`) confirms access is denied outside the AU scope.

![Out-of-Scope User - No AU Membership](images/step6-outside-au.png)
![Access Denied Verification](images/step6-access-denied.png)

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
