
Automate the provisioning of 1,000+ user accounts into Microsoft Entra ID (Azure AD) using the Microsoft Graph PowerShell SDK.
# Microsoft Entra ID – Automated User Provisioning with PowerShell & Microsoft Graph

This project demonstrates automated **large-scale user provisioning** in **Microsoft Entra ID** using **PowerShell** and the **Microsoft Graph SDK**.

The lab simulates an enterprise identity scenario where hundreds or thousands of users must be onboarded efficiently, securely, and consistently—without relying on manual portal-based creation.

---

## Project Overview

- Automated the provisioning of **1,000+ user accounts** in Microsoft Entra ID
- Used **PowerShell** with the **Microsoft Graph SDK**
- Authenticated securely using **Microsoft Graph delegated permissions**
- Resolved execution and module security constraints
- Demonstrated scalable identity automation aligned with enterprise IAM practices

**Business Problem Solved:**  
- Eliminates time-consuming and error-prone manual user creation  
- Enables scalable onboarding for large organizations  
- Ensures consistent identity configuration across users  
- Aligns with least-privilege and modern identity automation practices  

---

## PowerShell Environment Preparation

- Adjusted PowerShell execution policy to allow script execution
- Installed required Microsoft Graph modules for user management
- Imported specific Graph modules to reduce scope and overhead

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Install-Module Microsoft.Graph -Scope CurrentUser -Force
Import-Module Microsoft.Graph.Users
