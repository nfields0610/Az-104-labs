# **AZ-104 -- Lab 1: IAM & RBAC with Azure AD Groups**

## **Assigning "Reader" Role to Lab-operations-group at Resource Group Scope**

This lab demonstrates how to use **Azure Role-Based Access Control
(RBAC)** to assign permissions to an Azure AD security group using both:

-   **Azure Portal**
-   **Azure CLI (Cloud Shell)**

This aligns with AZ-104 learning objectives around IAM, least privilege,
and resource group access delegation.

------------------------------------------------------------------------

# -----------------------------------------

# **📸 Insert Your Header Image Here**

(Example: Your branded YouTube/AZ-104 banner) ![Header
Image](images/header.png) \# -----------------------------------------

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

### 📸 Insert screenshot of IAM blade:

![IAM Blade](images/iam-blade.png)

------------------------------------------------------------------------

## **2️⃣ Add a Role Assignment**

1.  Click **Add → Add role assignment**
2.  Select the **Reader** role\
3.  Click **Next**

### 📸 Insert screenshot of role selection:

![Role Selection](images/role-selection.png)

------------------------------------------------------------------------

## **3️⃣ Select the Security Group**

1.  Under **Members**, click **Select members**

2.  Search for:

        Lab-operations-group

3.  Select it\

4.  Click **Review + assign**

### 📸 Insert screenshot of group selection:

![Group Selection](images/group-selection.png)

------------------------------------------------------------------------

## **4️⃣ Confirmation**

Azure shows a success notification:

> **Lab-operations-group was added as Reader for AZ-104NF-RG**

### 📸 Insert screenshot of confirmation toast:

![Confirmation](images/role-assignment-confirmation.png)

------------------------------------------------------------------------

# -----------------------------------------

# **🧩 Part 2 --- Azure CLI Steps (Cloud Shell)**

# -----------------------------------------

### 📸 Insert screenshot of your Cloud Shell session:

![Cloud Shell](images/cloud-shell.png)

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

### 📸 Insert screenshot of the verification screen:

![Portal Verification](images/portal-verification.png)

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

This completes the IAM & RBAC portion of **AZ-104 Lab 1 -- Manage
Identities**.

------------------------------------------------------------------------

# -----------------------------------------

# **📸 Insert Your Footer Image or Branding**

![Footer](images/footer.png) \#
-----------------------------------------
