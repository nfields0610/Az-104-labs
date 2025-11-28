# AZ-104 Lab 1 --- Manage Identities

### Azure Administrator Certification Series

### by Nichelle Fields (YouTube: @nichellef)

## Overview

This lab demonstrates foundational identity management tasks in
Microsoft Entra ID, including: - Creating users using the Azure Portal -
Creating users using Azure CLI - Assigning directory roles - Creating a
security group - Adding members to a group - Understanding MFA behavior
during first sign-in

This lab aligns with AZ-104 Objective: Manage Azure identities and
governance.

## Learning Objectives

After completing this lab, you will be able to: - Create Azure AD users\
- Use Azure CLI to automate identity creation\
- Assign directory roles using least-privilege principles\
- Create security groups for access organization\
- Add users to groups\
- Interpret MFA requirements in secure tenants

## Prerequisites

-   Azure subscription\
-   Access to Microsoft Entra ID\
-   Cloud Shell enabled

# 1. Create a User in the Portal (Lab User 1)

Navigation Path: Microsoft Entra ID \> Users \> New user

Configuration values:

  Field                 Value
  --------------------- ---------------------------------------------
  Display Name          Lab User 1
  User Principal Name   Lab-user1@`<tenant>`{=html}.onmicrosoft.com
  Password              Temporary password
  User Type             Member

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/b921361f-f860-414f-8b13-b4b9feca2894" />


# 2. Create a User with Azure CLI (Lab User 2)

Run the following in Cloud Shell:

``` bash
az ad user create   --display-name "Lab User 2"   --user-principal-name lab-user2@<tenant>.onmicrosoft.com   --password "Pass@word123!"   --force-change-password-next-sign-in true
```

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/2ddec37c-3623-4ba5-8090-56f6e75c78bb" />


# 3. Assign Directory Roles

## Lab User 1 --- User Administrator

Role capabilities: - Manage user accounts\
- Reset passwords

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/b02b6a47-bd9d-4edf-a068-b5e8c52e706c" />


## Lab User 2 --- Helpdesk Administrator

Role capabilities: - Reset passwords for non-admin accounts

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/9443dff8-723c-4d11-8ea6-1285caa37ff8" />


# 4. Create a Security Group

Navigation Path: Entra ID \> Groups \> New group

Configuration values:

  Field             Value
  ----------------- -----------------------
  Group Type        Security
  Group Name        Lab-operations-group
  Description       Test group for AZ-104
  Membership Type   Assigned

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/a969094a-4c75-4e75-b2c6-cf1bea2b8997" />


# 5. Add Members to the Group

Add the following users: - Lab User 1\
- Lab User 2

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/03f90d7a-e44b-44f1-9852-6fe61d60991f" />


# 6. Group Creation Confirmation

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/037aac9b-0e04-40ff-b58b-ca6285cfe6bc" />


# 7. Login Attempt and MFA Behavior

When logging in with newly created accounts, a Multi-Factor
Authentication prompt may appear.

This is expected because: - Security defaults are enabled\
- MFA is required for all users\
- Free-tier tenants cannot modify MFA or conditional access settings

This is normal for AZ-104 training tenants.

# Reflection

This lab covers essential identity skills required for Azure
Administrators: - User lifecycle management\
- Directory role assignment\
- Group-based access organization\
- Azure CLI identity automation\
- Authentication and MFA defaults

These skills form the identity foundation for the AZ-104 exam.

# Part of My AZ-104 YouTube Series

This lab corresponds to "Manage Identities -- Part 1" on my YouTube
channel.

Channel: @nichellef

# Next Lab

AZ-104 Lab 2 --- Manage Group Membership, Access, and Licensing

# HUMN-X Alignment

"I build systems that remember people."
