# Windows-AD-Lab

This Project documents my personal setup used to practice Windows Server 2022/25 adminstrastion and Active Directory Services

## Lab Overview

- **Host OS**: Windows 10 Pro
- **Virtualization Software**: Proxmox
- **Guest OS**: Windows Server 2025, Windows 10/11
- **Domain Name**: `company.local`


## Project Objectives

- Set up a functioning Active Directory Domain Services (AD DS) environment.
- Create and manage Organizational Units (OUs) and user accounts.
- Join both physical and virtual machines to the domain.
- Implement and test Group Policy Objects (GPOs) such as password policies.
- Understand basic domain networking, DNS, and account management.


## Setup Steps

### 1. Windows Server Installation
- Installed Windows Server 2025 on a VM.
- Configured a static IP address: `10.10.0.254`


### 2. Active Directory Configuration
- Promoted the server to a Domain Controller using Server Manager.
- Created a new forest and domain: `company.local`
- Verified DNS setup.

### 3. Client Configuration
- Added a physical PC and a Windows 11 VM to the domain.
- Verified domain login functionality with both test account and admin accounts.

### 4. User & OU Management
- Created OUs:  "US", "EU", "Asia" to represent different branches
- Created Groups: "IT", "HR", "Accounting" within certain OU's
- Created user accounts.
- Assigned users to various OUs.
- Tested login credentials on new accounts.

### 5. Group Policy Configuration
- Created a GPO for password policies (complexity, min length, age).
- Policies for drive mapping, restricting access to control panel certain personalization features.
- Linked GPOs to specific OUs and computers and tested results.
- Practiced with account lockout settings and logon restrictions.
