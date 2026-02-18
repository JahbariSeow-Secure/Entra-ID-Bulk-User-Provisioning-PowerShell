# 🚀 Entra ID Bulk User Provisioning — PowerShell

> Automate the provisioning of 1,000+ user accounts into Microsoft Entra ID (Azure AD) using the Microsoft Graph PowerShell SDK.

---

## 📋 Business Case

Manually creating user accounts one-by-one in the Entra ID portal is time-consuming, error-prone, and completely unscalable. This project solves that.

### The Problem
When onboarding large cohorts of users — new employees, students, contractors, or project teams — IT admins face:
- **Hours of manual data entry** per batch of users
- **Human error** in naming, domain assignment, and role configuration
- **No audit trail** of what was created and when
- **Inconsistent formatting** of UPNs, display names, and mail nicknames

### The Solution
This script allows you to:
- Provision **1,000+ accounts in minutes** from a single CSV file
- Automatically **handle duplicate UPNs** by appending an incremental suffix
- Generate a **full audit log** (CSV) of every success and failure
- Run with **delegated or app-only authentication** via Microsoft Graph

### Who This Is For
| Role | Use Case |
|---|---|
| IT Administrators | Bulk onboarding new employees |
| Project Managers | Spinning up accounts for a new project team |
| Universities / Schools | Onboarding a new cohort of students |
| MSPs | Provisioning accounts across client tenants |

---

## 📁 Repository Structure

```
entra-bulk-provisioning/
│
├── Provision-EntraUsers.ps1       # Main provisioning script
├── Fix-DuplicateUPNs.ps1          # Helper: handles duplicate name collisions
├── sample-users.csv               # Example CSV input file
├── provisioning_results.csv       # Output: generated after running the script
└── README.md
```

---

## ✅ Prerequisites

- PowerShell 7+
- Microsoft Graph PowerShell SDK

```powershell
# Set execution policy
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Install the Microsoft Graph module
Install-Module Microsoft.Graph -Scope CurrentUser -Force
```

- Entra ID role: **User Administrator** or **Global Administrator**

---

## ⚙️ Setup

**1. Clone the repo**
```bash
git clone https://github.com/yourusername/entra-bulk-provisioning.git
cd entra-bulk-provisioning
```

**2. Prepare your CSV**

Your CSV should follow this structure (see `sample-users.csv`):
```csv
FirstName,LastName,Department,JobTitle
John,Doe,Engineering,Developer
Jane,Smith,Marketing,Manager
```

**3. Update the script config**

Open `Provision-EntraUsers.ps1` and update:
```powershell
$csvPath     = "C:\your\path\users.csv"
$defaultDomain = "yourdomain.onmicrosoft.com"
$defaultPassword = "TempP@ssword123!"
```

**4. Connect to Microsoft Graph**
```powershell
Connect-MgGraph -Scopes "User.ReadWrite.All"

# Verify your connection
Get-MgContext
```

**5. Run the script**
```powershell
.\Provision-EntraUsers.ps1
```

---

## 📸 Screenshots to Include in This Repo

Here are the key screenshots you should capture and add to a `/screenshots` folder:

| Screenshot | What to Capture |
|---|---|
| `01-graph-connected.png` | Terminal output after `Connect-MgGraph` showing tenant ID and delegated access confirmation |
| `02-script-running.png` | PowerShell terminal mid-run showing green "Created:" lines scrolling |
| `03-duplicate-handled.png` | Example of a duplicate UPN being resolved (e.g. `John.Smith1@...`) |
| `04-entra-portal-users.png` | Entra ID portal showing the newly created users in the All Users list |
| `05-results-csv.png` | Excel/Notepad view of the `provisioning_results.csv` output file |
| `06-get-mgcontext.png` | Output of `Get-MgContext` showing your account, tenant, and scopes |

> 💡 Tip: Use **Snipping Tool** or `Win + Shift + S` to capture your screenshots.

---

## 📊 Output

After the script runs, a `provisioning_results.csv` is saved with:

```
UPN,Status,ID,Error
john.doe@lees671.onmicrosoft.com,Success,xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,
jane.smith@lees671.onmicrosoft.com,Success,xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,
john.smith1@lees671.onmicrosoft.com,Success,xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx,
bad.user@lees671.onmicrosoft.com,Failed,,Some error message here
```

---

## ⚠️ Known Considerations

- **Rate limiting**: Microsoft Graph may throttle requests at scale. The script includes basic error handling; for very large batches consider adding `Start-Sleep -Milliseconds 200` between calls.
- **Licenses**: Accounts are created **unlicensed** by default. Assign licenses separately via `Set-MgUserLicense`.
- **Passwords**: All users are created with `ForceChangePasswordNextSignIn = $true` for security.

---

## 📄 License

MIT License — free to use and modify.
