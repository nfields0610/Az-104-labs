# ⚙️ Lab 21 -- Part 2: Azure Bastion Integration for Secure VM Access

## 🧩 Step Objective

Deploy **Azure Bastion** to enable secure RDP access to virtual machines
in **vm-lab-rg** without exposing Public IP addresses.

------------------------------------------------------------------------

## ⚙️ CLI Deployment Commands

``` bash
# 1) Create a Public IP for Bastion
az network public-ip create   --name LabBastionHost-pip   --resource-group vm-lab-rg   --sku Standard   --location centralus
```

``` bash
# 2) Create the Bastion Host
az network bastion create   --name LabBastionHost   --resource-group vm-lab-rg   --vnet-name winlabvm01VNET   --public-ip-address LabBastionHost-pip   --location centralus
```

------------------------------------------------------------------------

## 🧪 Verification Commands

If the initial "Succeeded" output wasn't captured, confirm deployment
with:

``` bash
az network bastion show   --name LabBastionHost   --resource-group vm-lab-rg   --query "{Name:name, Location:location, ProvisioningState:provisioningState, PublicIP:ipConfigurations[0].publicIpAddress.id, Subnet:ipConfigurations[0].subnet.id}"   -o table
```

**📸 Screenshot #1:** Output showing `ProvisioningState: Succeeded`\
**📸 Screenshot #2:** Azure Portal → **Bastion → Overview** page
confirming **Running** status.

------------------------------------------------------------------------

## 🧱 Enterprise Relevance -- Why This Step Matters

In enterprise environments, remote admin access should **not** rely on
exposed RDP/SSH ports. Deploying **Azure Bastion** provides:

-   🔒 **Zero Public Exposure** --- Admins connect via the Azure Portal
    using HTTPS (443) only.\
-   🧩 **Network Isolation** --- Bastion runs in `AzureBastionSubnet` as
    a private jump host in the VNet.\
-   📜 **Compliance Alignment** --- Supports controls aligned to
    NIST/ISO/HIPAA for restricted admin access.\
-   🧠 **Reduced Attack Surface** --- Eliminates public RDP/SSH
    endpoints targeted by scanning/brute-force.

> **In short:** Bastion replaces legacy VPN or public IP--based RDP with
> a managed, auditable, enterprise-grade access layer.

------------------------------------------------------------------------

## 🧹 Cost & Cleanup Reminder

``` bash
# Delete Bastion when the lab ends to avoid hourly charges
az network bastion delete   --name LabBastionHost   --resource-group vm-lab-rg   --yes

# (Optional) Delete the Bastion public IP if you won’t reuse it
az network public-ip delete   --name LabBastionHost-pip   --resource-group vm-lab-rg
```

💡 **Tip:** Bastion is billed hourly (\~\$0.18/hr). Delete after each
session (you have Tue/Wed/Thu 8:30 PM reminders).

------------------------------------------------------------------------

## ✅ Summary

  Step                  Purpose                                   Screenshot
  --------------------- ----------------------------------------- ------------
  Create Public IP      Prepare secure entry point for Bastion    
  Deploy Bastion Host   Establish private RDP gateway             
  Verify Deployment     Confirm `ProvisioningState = Succeeded`   📸 #1
  Portal Verification   Confirm Bastion **Running**               📸 #2
  Cleanup               Stop hourly billing                       
