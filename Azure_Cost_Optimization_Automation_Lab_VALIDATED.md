
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

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/58814f22-a0b3-403e-a98c-6f2a2c203dca" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/ac76fca6-acc5-4ed5-98ac-e0cd3cf170cf" />


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

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/27e712b9-3ab3-42e5-9336-6aeebc953a0f" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/e2c7a00e-c313-4cc1-b807-95b3f86c6213" />


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

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/0e6c89c1-af49-453d-b74c-81c37a041111" />


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

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/c4afbf4c-ab67-4d97-b10b-69180b0b4f30" />

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/7670a641-c1b3-4e86-9367-49d2c6131505" />


---

## Step 5 – Schedule the Runbook
**Schedule Name:** `Nightly-Full-Cleanup`

- Frequency: Daily
- Execution: Nightly (off‑hours)
- Linked to runbook successfully

<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/6b2046e3-93e8-4952-9c3f-0e7028a79050" />


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


<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/2271b645-9acf-435b-b86c-911f666a2d5a" />


<img width="1366" height="1024" alt="image" src="https://github.com/user-attachments/assets/b8afd77a-1236-4b16-a1ae-efcb12054672" />

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


