
# Azure Cost Optimization & Automation Lab (Validated Execution)
**Focus:** Budgets, Automation Accounts, RBAC, Runbooks, Scheduling  
**Platform:** Microsoft Azure  
**Level:** Intermediate / Enterprise-Aligned (AZ‑104, FinOps)

---

## Lab Summary
This lab demonstrates **end‑to‑end Azure cost governance** using native services:
- Cost Management budgets
- Azure Automation with managed identity
- RBAC-based permissions
- Scheduled PowerShell cleanup

The solution was **successfully executed and validated** via an Automation runbook job.

---

## Objectives
- Prevent uncontrolled Azure spending
- Automate cleanup of lab/non‑production resources
- Use identity‑based authentication (no secrets)
- Simulate real enterprise governance patterns

---

## Step 1 – Create Monthly Budget
**Service:** Azure Cost Management

- Budget name: `Monthly-Lab-Budget`
- Scope: Subscription
- Amount: $10
- Period: Monthly
- Forecast tracking enabled

**Result:**  
Budget successfully created and visible under Cost Management.

📸 Screenshot: Create Budget wizard  
📸 Screenshot: Budget created confirmation

---

## Step 2 – Create Automation Account
**Service:** Azure Automation

Configuration:
- Name: `DailyCleanupAutomation`
- Resource Group: `Mgmt-rg`
- Region: Central US
- Identity: **System‑assigned (enabled)**

**Why this matters:**  
Managed identities eliminate credential storage and align with enterprise security practices.

📸 Screenshot: Automation Account creation  
📸 Screenshot: Deployment succeeded

---

## Step 3 – Assign RBAC Permissions
**Tool:** Azure Cloud Shell (PowerShell)

Granted the Automation Account permission to manage resources at the subscription scope.

```powershell
$sub = (az account show --query id -o tsv)

$identityId = (
  az resource list   --name DailyCleanupAutomation   --resource-type Microsoft.Automation/automationAccounts   --query "[0].identity.principalId" -o tsv
)

az role assignment create   --assignee $identityId   --role "Contributor"   --scope /subscriptions/$sub
```

**Result:**  
Role assignment successfully created.

📸 Screenshot: Role assignment output

---

## Step 4 – Create PowerShell Runbook
**Runbook Name:** `Delete-All-ResourceGroups`  
**Runtime:** PowerShell 7.2

### Runbook Logic
```powershell
Connect-AzAccount -Identity

Write-Output "Fetching all resource groups..."

$skipRg = "Mgmt-rg"
$rgList = Get-AzResourceGroup

foreach ($rg in $rgList) {
    if ($rg.ResourceGroupName -eq $skipRg) {
        Write-Output "Skipping $skipRg (persistent management RG)"
        continue
    }

    Write-Output "Deleting resource group: $($rg.ResourceGroupName)..."
    Remove-AzResourceGroup -Name $rg.ResourceGroupName -Force -AsJob
}
```

**Design Considerations:**
- Protects the management resource group
- Uses asynchronous deletion jobs
- Safe for repeated execution

📸 Screenshot: Runbook editor  
📸 Screenshot: Runbook published

---

## Step 5 – Schedule the Runbook
**Schedule Name:** `Nightly-Full-Cleanup`

- Frequency: Daily
- Execution: Nightly (off‑hours)
- Linked to runbook successfully

📸 Screenshot: Schedule creation confirmation

---

## Step 6 – Execution & Validation (Proof)
The runbook executed successfully via the schedule.

### Job Details
- **Status:** Completed
- **Execution Time:** 12/10/2025 00:09
- **Run Environment:** Azure Automation

### Output Highlights
```
Fetching all resource groups...
Deleting resource group: AZ-104NF-RG...
Skipping mgmt-rg (persistent management RG)
Deleting resource group: TestCleanupRG...
```

**Observed Behavior:**
- Target resource groups deleted
- Management RG preserved
- No errors or exceptions

📸 Screenshot: Job output (Completed)  
📸 Screenshot: Resource group recreation test

---

## Results
- Automated cost controls enforced
- Subscription protected from orphaned resources
- Repeatable lab cleanup achieved
- Governance validated through execution

---

## Enterprise Relevance
This pattern mirrors real-world practices used for:
- Dev/Test subscriptions
- Sandbox environments
- FinOps guardrails
- Platform engineering standards

---

## Future Enhancements
- Budget threshold email alerts
- Azure Monitor alerts on job failures
- Tag-based deletion logic
- Approval workflows via Logic Apps

---

## Skills Demonstrated
- Azure Cost Management
- Azure Automation
- Managed Identities
- RBAC
- PowerShell Automation
- Cloud Governance

---

**Lab Status:** ✅ Completed & Validated  
**Use Case:** Portfolio / Interviews / AZ‑104 / Real‑world readiness
