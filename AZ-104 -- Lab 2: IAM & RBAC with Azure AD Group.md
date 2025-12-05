# **AZ-104 -- Lab 1: IAM & RBAC with Azure AD Groups**

## **Assigning "Reader" Role to Lab-operations-group at Resource Group Scope**

This lab demonstrates how to use **Azure Role-Based Access Control
(RBAC)** to assign permissions to an Azure AD security group using both:

-   **Azure Portal**
-   **Azure CLI (Cloud Shell)**

This aligns with AZ-104 learning objectives around IAM, least privilege,
and resource group access delegation.

------------------------------------------------------------------------

# 🎯 **Lab Objective**

Provide **view-only access** to the resource group **AZ-104NF-RG** by
assigning the **Reader** role to the **Lab-operations-group**.

This allows group members to see resources without being able to modify
or delete them.

------------------------------------------------------------------------

# -----------------------------------------

# **🧩 Part 1 --- Portal Steps**

# -----------------------------------------

## **1️⃣ Navigate to Access Control (IAM)**

1.  Go to **Resource groups**\
2.  Select **AZ-104NF-RG**\
3.  Click **Access control (IAM)**


<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/a66bead9-fae9-4cf2-8e4a-04c1da69f5f8" />


------------------------------------------------------------------------

## **2️⃣ Add a Role Assignment**

1.  Click **Add → Add role assignment**
2.  Select the **Reader** role\
3.  Click **Next**


<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/a14e12ca-a445-44dd-a87c-24b5b48c4679" />


------------------------------------------------------------------------

## **3️⃣ Select the Security Group**

1.  Under **Members**, click **Select members**

2.  Search for:

        Lab-operations-group

3.  Select it\

4.  Click **Review + assign**

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/12b33a61-18a0-4dc0-a82f-cdb6d0d2e517" />




------------------------------------------------------------------------

## **4️⃣ Confirmation**

Azure shows a success notification:

> **Lab-operations-group was added as Reader for AZ-104NF-RG**



<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/c371c0be-25ee-42fa-8ace-1c1436d73311" />


------------------------------------------------------------------------

# -----------------------------------------

# **🧩 Part 2 --- Azure CLI Steps (Cloud Shell)**

# -----------------------------------------



<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/31993e48-5388-491d-9b41-6db1bf46192d" />


------------------------------------------------------------------------

## **1️⃣ Retrieve the Group Object ID**

``` bash
az ad group list --display-name "lab-operations-group" --query "[0].id" -o tsv
```

> Output example:\
> `d97757ae-41fa-47b7-9e12-5dc1f94d1cc3`

------------------------------------------------------------------------

## **2️⃣ Create the Role Assignment**

``` bash
az role assignment create   --assignee d97757ae-41fa-47b7-9e12-5dc1f94d1cc3   --role "Reader"   --scope "/subscriptions/<yourSubID>/resourceGroups/AZ-104NF-RG"
```

CLI output confirms: - principalType = Group\
- roleDefinitionName = Reader\
- scope = AZ-104NF-RG

------------------------------------------------------------------------

# -----------------------------------------

# **🧩 Part 3 --- Verification**

# -----------------------------------------

## **Portal Verification**

Go to:

**Access control (IAM) → Role assignments → Search
"Lab-operations-group"**

You should see:

  Role     Scope           Condition
  -------- --------------- -----------
  Reader   This resource   None


<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/c9f0834d-66e6-4f9a-adee-2ec3d3dd0f6f" />


------------------------------------------------------------------------

## **CLI Verification**

``` bash
az role assignment list  --assignee d97757ae-41fa-47b7-9e12-5dc1f94d1cc3  --scope "/subscriptions/<subID>/resourceGroups/AZ-104NF-RG"  -o table
```

Expected output:

    Role     Scope
    -------  -------------------------------------------------------------
    Reader   /subscriptions/.../resourceGroups/AZ-104NF-RG

------------------------------------------------------------------------

# -----------------------------------------

# **📘 Key Learning Concepts**

# -----------------------------------------

### 🔐 IAM vs RBAC

-   IAM = identity management (users, groups, service principals)
-   RBAC = permission model that determines **what** identities can do

### 🚦 RBAC Scope Levels

-   Subscription\
-   Resource Group\
-   Resource

RBAC **inherits downward**.

### 👥 Use Groups for Scalability

Assign roles to **groups**, not individuals: - Cleaner auditing\
- Easy access onboarding/offboarding\
- Consistent permissions

### 🧭 Principle of Least Privilege

Reader role allows visibility without risk of modification.

------------------------------------------------------------------------

# -----------------------------------------

# **📌 Commands Used in This Lab**

# -----------------------------------------

``` bash
# Get Azure AD group ID
az ad group list --display-name "lab-operations-group" --query "[0].id" -o tsv

# Assign Reader role to the group
az role assignment create   --assignee <groupObjectID>   --role "Reader"   --scope "/subscriptions/<subID>/resourceGroups/AZ-104NF-RG"

# Verify via CLI
az role assignment list --assignee <groupObjectID> -o table
```

------------------------------------------------------------------------

# ✅ **Lab Completed Successfully**

You successfully assigned **Reader** permissions to
**Lab-operations-group** at the **resource group scope** using both:

✔️ Azure Portal\
✔️ Azure CLI

This completes the IAM & RBAC portion of **AZ-104 Lab 2 -- Manage
Identities**.

------------------------------------------------------------------------

# -----------------------------------------

# **📸 Insert Your Footer Image or Branding**

![Footer](images/footer.png) \#
-----------------------------------------
