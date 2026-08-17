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

```text
technova-active-directory-lab
│
├── README.md
├── diagrams
│   ├── technova-network.drawio
│   └── technova-network.png
├── screenshots
│   ├── phase1
│   ├── phase2
│   ├── phase3
│   ├── phase4
│   ├── phase5
│   ├── phase6
│   ├── phase7
│   └── phase8
├── scripts
│   ├── Create-Users.ps1
│   └── Employees.csv
└── docs
```

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