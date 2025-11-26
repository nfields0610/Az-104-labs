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

Screenshot reference: images/create-user-portal.png

# 2. Create a User with Azure CLI (Lab User 2)

Run the following in Cloud Shell:

``` bash
az ad user create   --display-name "Lab User 2"   --user-principal-name lab-user2@<tenant>.onmicrosoft.com   --password "Pass@word123!"   --force-change-password-next-sign-in true
```

Screenshot reference: images/create-user-cli.png

# 3. Assign Directory Roles

## Lab User 1 --- User Administrator

Role capabilities: - Manage user accounts\
- Reset passwords

Screenshot reference: images/assign-role-user1.png

## Lab User 2 --- Helpdesk Administrator

Role capabilities: - Reset passwords for non-admin accounts

Screenshot reference: images/assign-role-user2.png

# 4. Create a Security Group

Navigation Path: Entra ID \> Groups \> New group

Configuration values:

  Field             Value
  ----------------- -----------------------
  Group Type        Security
  Group Name        Lab-operations-group
  Description       Test group for AZ-104
  Membership Type   Assigned

Screenshot reference: images/create-group.png

# 5. Add Members to the Group

Add the following users: - Lab User 1\
- Lab User 2

Screenshot reference: images/add-members.png

# 6. Group Creation Confirmation

Screenshot reference: images/group-created.png

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
