# TechNova Enterprise Active Directory Lab

Enterprise Infrastructure Engineering project demonstrating the deployment of an on-premises Active Directory environment using Windows Server 2022, Group Policy, DNS, PowerShell, and Windows 10.

![TechNova Network Architecture](diagrams/technova-network.png)

---

## Project Overview

This project simulates the IT infrastructure of **TechNova**, a medium-sized enterprise. The environment was built entirely inside Oracle VirtualBox and includes a Domain Controller, domain-joined client, Organizational Units, Security Groups, Group Policy, File Shares, Folder Redirection, and automated onboarding of **513 employees** using PowerShell.

---

## Technologies Used

- Windows Server 2022
- Windows 10
- Active Directory Domain Services
- DNS
- Group Policy (GPO)
- PowerShell
- Oracle VirtualBox

---

## Lab Environment

| Component | Details |
|-----------|---------|
| Domain Controller | DC01 |
| Client Machine | CLIENT01 |
| Domain | TECHNOVA.LOCAL |
| Server OS | Windows Server 2022 |
| Client OS | Windows 10 |
| Hypervisor | Oracle VirtualBox |

---

## Project Phases

| Phase | Implementation |
|-------|----------------|
| 1 | Windows Server Installation & Domain Controller Deployment |
| 2 | Organizational Units & Department Structure |
| 3 | Domain Join & Active Directory User Management |
| 4 | Group Policy Configuration |
| 5 | Enterprise File Shares & NTFS Permissions |
| 6 | Folder Redirection |
| 7 | PowerShell User Provisioning Automation |
| 8 | 513 Employee Enterprise Onboarding |

---

## Key Features

- Active Directory domain deployment
- Department-based Organizational Units
- Security Group administration
- DNS configuration and authentication
- Group Policy implementation
- File Share & NTFS permissions
- Folder Redirection
- Home Folder creation
- CSV-driven PowerShell automation
- User creation logging and reporting

---

## PowerShell Automation

The onboarding script performs the following tasks automatically:

- Imports employee data from CSV
- Creates Active Directory users
- Assigns department attributes
- Creates User Principal Names
- Adds users to Security Groups
- Creates Home Folders
- Generates creation logs
- Displays onboarding summary

---

## Results

| Metric | Value |
|---------|------:|
| Total Employee Records | **513** |
| Users Successfully Created | **500+** |
| Department OUs | **5** |
| Security Groups | **8+** |
| Domain Joined Clients | **1** |
| PowerShell Automation | **Implemented** |

---

## Repository Structure

| Folder | Purpose |
|---------|---------|
| `README.md` | Complete project documentation |
| `diagrams/` | Draw.io network & workflow diagrams |
| `screenshots/phase1-8/` | Evidence for each implementation phase |
| `scripts/Create-Users.ps1` | PowerShell automation script |
| `scripts/Employees.csv` | Bulk onboarding employee dataset |
| `docs/` | Supporting project documents |

---

## Skills Demonstrated

- Windows Server Administration
- Active Directory Management
- DNS Administration
- Group Policy
- PowerShell Scripting
- Bulk User Provisioning
- NTFS Permissions
- Folder Redirection
- Infrastructure Documentation
- Git & GitHub

---

## Author

**Nithin Reddy**

Infrastructure Engineering Lab

---

# Phase 1 — Domain Controller Deployment

## Objective

Deploy the first Domain Controller (DC01) and establish the **TECHNOVA.LOCAL** Active Directory domain for centralized authentication and management.

## Implementation

- Installed Windows Server 2022 in Oracle VirtualBox
- Renamed the server to **DC01**
- Configured a static IP address
- Installed **Active Directory Domain Services (AD DS)**
- Promoted the server to the first Domain Controller
- Created the **TECHNOVA.LOCAL** forest
- Configured DNS automatically during promotion

## Architecture

The lab consists of a Windows 10 client connected to a Windows Server Domain Controller through an isolated internal virtual network.

![TechNova Network Architecture](screenshots/phase1/01-network-architecture.png)

---

## Verification Commands

```powershell
ipconfig /all
hostname
nslookup technova.local
whoami
```

These commands verified network configuration, hostname, DNS resolution, and authentication.

## Troubleshooting

| Issue | Resolution |
|--------|------------|
| Domain not reachable | Verified VirtualBox network configuration |
| DNS resolution failed | Configured DC01 as the DNS server |
| Client unable to find domain | Confirmed static IP and DNS settings |

## Evidence

Place the following screenshots inside `screenshots/phase1/`:

1. Windows Server 2022 desktop
2. AD DS installed in Server Manager
3. Domain promotion successful
4. `ipconfig /all`
5. `nslookup technova.local`

---

# Phase 2 — Organizational Units & Department Structure

## Objective

Design a scalable Active Directory structure by organizing users into departmental Organizational Units (OUs) and implementing department-based Security Groups.

## What I Implemented

Created the following Organizational Units:

- IT
- HR
- Finance
- Sales
- Marketing
- Operations

Created Security Groups:

- IT_Users
- HR_Users
- Finance_Users
- Sales_Users
- Marketing_Users
- Operations_Users

Each department receives its own OU and Security Group to simplify administration and permission management.

## Active Directory Structure

TECHNOVA.LOCAL

- IT
- HR
- Finance
- Sales
- Marketing
- Operations

## PowerShell Verification

```powershell
Get-ADOrganizationalUnit -Filter *
Get-ADGroup -Filter *
Get-ADGroupMember "IT_Users"
```

## Troubleshooting

| Issue | Resolution |
|--------|------------|
| Incorrect OU path in PowerShell | Verified Distinguished Name using `Get-ADOrganizationalUnit` |
| Users created in wrong location | Updated the `-Path` parameter with the correct OU |
| Group membership not verified | Used `Get-ADGroupMember` to confirm users |

## Screenshots

![Organizational Units](screenshots/phase2/01-organizational-units.png)

![Security Groups](screenshots/phase2/02-security-groups.png)

![Group Members](screenshots/phase2/03-group-members.png)

### Step 4: CLIENT01 successfully joined the technova.local domain

![Domain Join Success](screenshots/phase2/03-04-domain-join-success.png)

---

# Phase 3 — Domain Join & Active Directory User Management

## Objective

Join CLIENT01 to the TECHNOVA.LOCAL domain and validate centralized authentication using Active Directory user accounts.

## What I Implemented

- Configured CLIENT01 to use DC01 as its DNS server
- Joined Windows 10 client to **TECHNOVA.LOCAL**
- Restarted the client after domain join
- Logged in using domain credentials
- Verified communication between CLIENT01 and DC01

## Authentication Workflow

This workflow shows how a domain user is authenticated after signing in from CLIENT01.

![Authentication Workflow](screenshots/phase3/01-authentication-workflow.png)

## Verification Commands

```powershell
ipconfig /all
ping DC01
nslookup technova.local
whoami
```

## Troubleshooting

| Issue | Resolution |
|--------|------------|
| Domain join failed | Verified DNS was pointing to DC01 |
| Client couldn't locate domain | Tested using `nslookup technova.local` |
| Unable to authenticate | Confirmed domain credentials and restarted CLIENT01 |
| Network communication issue | Verified connectivity using `ping DC01` |

## Screenshots

![Client Joined Domain](screenshots/phase3/01-domain-join.png)

![Domain Login](screenshots/phase3/02-domain-login.png)

![Whoami Verification](screenshots/phase3/03-whoami.png)

## Part B: User Must Change Password at First Logon

After creating the domain user account, the **User must change password at next logon** option was enabled in Active Directory. When the user signed in for the first time, Windows forced a password change before allowing desktop access.

### Screenshots

**03B-01:** Enable **User must change password at next logon** in Active Directory

![Enable Password Change](screenshots/phase3/03b-01-enable-password-change.png)

**03B-02:** CLIENT01 prompts the user to change the password before sign-in

![First Logon Password Change](screenshots/phase3/03b-02-first-logon-password-change.png)



---

# Phase 4 — Group Policy Management (GPO)

## Objective

Implement and validate Group Policy Objects (GPOs) to centrally manage Windows client settings across the TECHNOVA domain.

## What I Implemented

- Created a new Group Policy Object (GPO)
- Linked the GPO to the appropriate Organizational Unit (OU)
- Applied User and Computer Configuration settings
- Updated policies on CLIENT01
- Verified successful GPO application

## Group Policy Workflow

This workflow illustrates how a Group Policy Object (GPO) is created on DC01, linked to an Organizational Unit, and automatically applied to domain-joined client computers.

![Group Policy Workflow](screenshots/phase4/01-group-policy-workflow.png)

## Verification Commands

```powershell
gpupdate /force
gpresult /r
gpresult /h C:\Temp\GPReport.html
```

## Troubleshooting

| Issue | Resolution |
|--------|------------|
| GPO changes not visible | Forced refresh using `gpupdate /force` |
| Policy not applied | Verified with `gpresult /r` |
| Incorrect OU link | Confirmed GPO was linked to the correct OU |
| User settings missing | Logged in with the correct domain user |

## Screenshots

![Group Policy Management](screenshots/phase4/01-gpo-management.png)

![GPO Linked](screenshots/phase4/02-gpo-linked.png)

![GPResult](screenshots/phase4/03-gpresult.png)

---

# Phase 4A — Corporate Desktop Wallpaper

## Objective

Deploy a standardized TechNova corporate desktop wallpaper to all domain users using Group Policy.

## What I Implemented

- Created a new Group Policy Object named **Corporate Desktop Wallpaper**
- Linked the GPO to the `technova.local` domain
- Stored the company wallpaper on the DC01 shared folder
- Configured the Desktop Wallpaper policy using a UNC path
- Applied and verified the policy on CLIENT01

## Screenshots

### Step 1: Create Corporate Desktop Wallpaper GPO

![Create GPO](screenshots/phase4/04a-01-wallpaper-creation.png)

### Step 2: Open Group Policy Management Editor

![GPO Editor](screenshots/phase4/04a-02-gpo-editor.png)

### Step 3: Store TechNova Wallpaper on DC01

![Wallpaper Folder](screenshots/phase4/04a-03-wallpaper-folder.png)

### Step 4: Enable Desktop Wallpaper Policy

![Wallpaper Policy Enabled](screenshots/phase4/04a-04-wallpaper-policy-enabled.png)

### Step 5: Verify Wallpaper on CLIENT01

![Wallpaper Applied](screenshots/phase4/04a-05-wallpaper-applied.png)

---

# Phase 4B — USB Storage Restriction

## Objective

Prevent users from accessing USB storage devices across all domain-joined computers using Group Policy.

## What I Implemented

- Created a new GPO named **USB Storage Restriction**
- Linked the GPO to the `technova.local` domain
- Enabled **All Removable Storage classes: Deny all access**
- Applied the policy to domain computers
- Verified the GPO was successfully applied on the client

## Screenshots

### Step 1: Create USB Storage Restriction GPO

![USB GPO Creation](screenshots/phase4/04b-01-usb-gpo-creation.png)

### Step 2: Enable "Deny All Removable Storage Access"

![USB Policy Enabled](screenshots/phase4/04b-02-usb-policy-enabled.png)

### Step 3: Verify GPO Applied on CLIENT01

![USB Verification](screenshots/phase4/04b-03-usb-gpresult.png)

---

# Phase 4C — Block Control Panel Using Group Policy

## Objective

Prevent domain users from accessing Control Panel and Windows Settings using Group Policy.

## What I Implemented

- Created a new GPO named **Block Control Panel**
- Linked the GPO to the `technova.local` domain
- Enabled **Prohibit access to Control Panel and PC settings**
- Applied the policy to domain users
- Verified the restriction on CLIENT01

## Result

- Domain users cannot open Control Panel.
- Windows Settings is restricted.
- The policy is centrally managed through Active Directory.

## Screenshots

### Step 1: Create Block Control Panel GPO

![Create Block Control Panel GPO](screenshots/phase4/04c-01-block-control-panel-gpo.png)

### Step 2: Link the GPO to the Domain

![Link GPO](screenshots/phase4/04c-02-link-gpo.png)

### Step 3: Navigate to Control Panel Policy

![Control Panel Policy](screenshots/phase4/04c-03-control-panel-policy.png)

### Step 4: Enable Control Panel Restriction

![Enable Control Panel Restriction](screenshots/phase4/04c-04-enable-control-panel.png)

### Step 5: Verify Control Panel restriction on CLIENT01

![Control Panel Block Verification](screenshots/phase4/04c-05-control-panel-block-verification.png)

---
# Phase 5 — File Shares & NTFS Permissions

## Objective
Create departmental shared folders and secure them using Share Permissions and NTFS Permissions.

## Department Folders

The following folders were created under `C:\CompanyShares`:

- Finance
- HR
- IT
- Marketing
- Operations
- Sales

![Company Share Folders](../screenshots/phase5/01-company-share-folders.png)

## Configure Share Permissions

Each departmental folder was shared using **Advanced Sharing**.

Share name example: `HR`

Permission configured:

- Everyone → Read

![Share Permissions](../screenshots/phase5/02-share-permissions.png)

## Disable Inheritance

Inherited permissions were disabled and converted into explicit permissions.

![Disable Inheritance](../screenshots/phase5/03-disable-inheritance.png)

## Configure NTFS Permissions

Default inherited permissions were removed and departmental security groups were assigned.

Example:

- HR_Users → Modify
- Administrators → Full Control
- SYSTEM → Full Control

![NTFS Permissions](../screenshots/phase5/04-ntfs-permissions.png)

## Department Group Access

The HR security group was granted **Modify** permission for the HR department folder.

![HR Modify Permission](../screenshots/phase5/05-hr-group-modify.png)

## Final Result

Final permissions show only the required security principals with least-privilege access.

![Final Permissions](../screenshots/phase5/06-final-permissions.png)

### Outcome

- Created 6 departmental shared folders
- Configured network sharing
- Implemented NTFS least-privilege permissions
- Restricted access using Active Directory security groups

# Phase 6A — Drive Mapping with Group Policy

## Objective

Automatically map the company shared drive (S:) to all domain users using Group Policy Preferences.

## Step 1: Create a Drive Mapping GPO

A new Group Policy Object named **Map Company Drive** was created in Group Policy Management.

![Create Drive Mapping GPO](../screenshots/phase6/01-create-drive-gpo.png)

## Step 2: Create a Mapped Drive

Navigate to:

`User Configuration → Preferences → Windows Settings → Drive Maps`

Create a new **Mapped Drive** preference.

![New Mapped Drive](../screenshots/phase6/02-new-mapped-drive.png)

## Step 3: Configure Drive Properties

The shared folder was configured with the following settings:

| Setting | Value |
|---|---|
| Action | Create |
| Drive Letter | S: |
| Network Path | `\\DC01\Companyshares` |
| Label | TechNova Shared Drive |

![Drive Properties](../screenshots/phase6/03-drive-properties.png)

## Step 4: Verify GPO Configuration

The Drive Maps policy now contains the S: drive mapping and is ready for deployment.

![Drive Map Created](../screenshots/phase6/04-drive-map-created.png)

### Result

- Created a dedicated Drive Mapping GPO
- Configured automatic S: network drive mapping
- Centralized access to company shared folders

# Phase 6B — Folder Redirection & Access Verification

## Objective

Deploy Folder Redirection through Group Policy and verify that users can access only authorized departmental network shares.

## Link Folder Redirection GPO

The **Folder Redirection** Group Policy Object was linked to the **Workstations** Organizational Unit so that all domain-joined client computers receive the policy.

![Folder Redirection Linked](../screenshots/phase6/01-folder-redirection-linked.png)

## Verify Network Shares

From CLIENT01, the user successfully browsed the DC01 server and viewed all published departmental shares.

Available shares included:

- CompanyData
- Finance
- HR
- IT
- Marketing
- Operations
- Sales

![Network Shares Visible](../screenshots/phase6/02-network-share-visible.png)

## Verify Access Restrictions

Attempting to open the **IT** departmental share from an unauthorized user resulted in an **Access Denied** message, confirming that NTFS and security group permissions were enforced correctly.

![Access Denied Verification](../screenshots/phase6/03-access-denied-verification.png)

### Outcome

- Folder Redirection GPO linked successfully
- Network shares accessible from domain clients
- Unauthorized departmental access blocked
- Least-privilege security model verified

---

# Phase 7 – PowerShell Automated User Provisioning

## Objective

Automate the creation of Active Directory users using PowerShell and a CSV file, eliminating manual account creation and ensuring consistent enterprise onboarding.

## What I Implemented

- Created a structured employee CSV database
- Imported employee records using `Import-Csv`
- Automated AD user creation with `New-ADUser`
- Assigned users to departmental OUs
- Generated User Principal Names (UPN)
- Applied department attributes
- Detected duplicate usernames
- Implemented error handling using `try` / `catch`

## Automation Workflow

![PowerShell Automation Workflow](screenshots/phase7/01-automation-workflow.png)

## PowerShell Commands

```powershell
Import-Csv
Get-ADUser
Get-ADOrganizationalUnit
New-ADUser
ConvertTo-SecureString
```

## Troubleshooting

| Issue | Resolution |
|--------|------------|
| CSV not loading correctly | Verified column headers and file path |
| Duplicate usernames | Checked with `Get-ADUser` before creation |
| Users created in wrong OU | Corrected the `-Path` Distinguished Name |
| Password format error | Converted plaintext using `ConvertTo-SecureString` |
| Script stopped on error | Implemented `try` / `catch` for continuous processing |

## Screenshots

**04A – Employee CSV Import**

Shows the employee records successfully imported from `Employees.csv` using the `Import-Csv` command.

![Employee CSV Import](screenshots/phase7/01-employees-csv.png)

**04B – PowerShell Automation Script**

Displays the complete PowerShell script used to automate Active Directory user provisioning.

![PowerShell Script](screenshots/phase7/02-powershell-script.png)

**04C – Organizational Unit Verification**

Verifies the Distinguished Names of all Organizational Units before automated user creation.

![OU Verification](screenshots/phase7/03-ou-verification.png)

**04D – Successful User Creation**

Confirms that users were created successfully and placed into their respective departmental OUs.

![Successful User Creation](screenshots/phase7/04-user-created.png)


## Phase 7.1 – Implementation Walkthrough

This section demonstrates the PowerShell automation workflow used to provision Active Directory users from a CSV file.

### 07A – PowerShell Automation Script

The PowerShell script imports employee records, validates existing users, creates new AD accounts, assigns organizational attributes, and writes execution logs.

![PowerShell Script](screenshots/phase7/7.1-01-powershell-script.png)

---

### 07B – Automated User Provisioning

Execution of the automation script showing successful creation of a new Active Directory user and departmental group assignment.

![Script Execution](screenshots/phase7/7.1-02-script-execution.png)

---

### 07C – Department Security Group Verification

Verification that the newly created account was added to the correct departmental security group using `Get-ADGroupMember`.

![Security Group Verification](screenshots/phase7/7.1-03-group-verification.png)

---

### 07D – Execution Summary

Final output displaying users created, skipped duplicate accounts, and failed operations after the automation completed.

![Execution Summary](screenshots/phase7/7.1-04-execution-summary.png)

---

### 07E – Audit Log Verification

Review of the user creation log confirming successful provisioning events and duplicate account detection.

![Audit Log](screenshots/phase7/7.1-05-audit-log.png)

---

# Phase 8 – Enterprise User Onboarding (500+ Employees)

## Objective

Perform enterprise-scale onboarding by provisioning **513 employee accounts** automatically through a single PowerShell script while assigning Organizational Units, Security Groups, Home Folders, and generating audit logs.

## What I Implemented

- Imported **513 employee records** from CSV
- Created Active Directory user accounts automatically
- Assigned users to department OUs
- Added users to departmental Security Groups
- Created individual Home Folders
- Generated onboarding audit logs
- Displayed final provisioning summary
- Continued processing even when duplicate accounts existed

## Enterprise Onboarding Workflow

![Enterprise Onboarding Workflow](screenshots/phase8/01-enterprise-onboarding-workflow.png)

## PowerShell Components

```powershell
Import-Csv
New-ADUser
Add-ADGroupMember
New-Item
Get-Acl
Add-Content
```

## Troubleshooting

| Issue | Resolution |
|--------|------------|
| Duplicate employee accounts | Existing users skipped automatically |
| Home folder not created | Verified destination path using `New-Item` |
| Security group assignment failed | Confirmed group name before `Add-ADGroupMember` |
| Permission validation required | Verified NTFS permissions with `Get-Acl` |
| Enterprise execution auditing | Logged every action using `Add-Content` |

## Screenshots

### 08A – Enterprise Onboarding PowerShell Script

Shows the complete provisioning script including user creation, security group assignment, home folder creation, and audit logging.

![Enterprise Script](screenshots/phase8/01-enterprise-script.png)

---

### 08B – Automated Enterprise User Provisioning

Execution of the script successfully creating a new employee account, generating the home folder, and assigning the departmental security group.

![Enterprise Provisioning](screenshots/phase8/02-enterprise-provisioning.png)

---

### 08C – Home Folder Generation

Automatically created personal home folder for the provisioned employee under the centralized HomeFolders directory.

![Home Folder](screenshots/phase8/03-home-folder.png)

---

### 08D – NTFS Permission Verification

Validated folder permissions using the `Get-Acl` PowerShell command to confirm enterprise access control.

![NTFS Permissions](screenshots/phase8/04-ntfs-permissions.png)

---

## Project Architecture Summary

The TechNova Enterprise Infrastructure Lab integrates Active Directory, Group Policy, file services, PowerShell automation, and enterprise-scale onboarding into a complete Windows Server infrastructure solution.

![Project Architecture Summary](screenshots/final/01-project-architecture-summary.png)

---

# Project Outcome

The TechNova Enterprise Infrastructure Lab successfully demonstrates the complete deployment and administration of an on-premises Active Directory environment. The project includes centralized authentication, DNS, Group Policy, file services, folder redirection, and enterprise-scale onboarding through PowerShell automation.

## Skills Demonstrated

- Windows Server 2022 Administration
- Active Directory Domain Services
- DNS Configuration
- Group Policy Management
- Organizational Unit Design
- Security Group Administration
- NTFS & Share Permissions
- Folder Redirection
- PowerShell Automation
- Bulk User Provisioning (513 Users)
- Infrastructure Documentation
- Git & GitHub

---

## Author

**Nithin**


