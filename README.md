# Windows 11 Upgrade Simulation Using Microsoft Intune

## 🛠️ Overview
This project simulates an enterprise-scale upgrade of Windows 10 devices to Windows 11 using Microsoft Intune and Endpoint Manager. The goal was to mirror what an organization like LA Care Health Plan would most likely perform during a real-world upgrade of 3,900 managed workstations.

Using a Microsoft 365 Business Premium trial, I enrolled a Windows 10 VM into Intune, assigned a Windows Update Ring to upgrade to Windows 11, and applied a compliance policy to enforce enterprise security standards.

---

## ✅ Objectives
- Set up a Microsoft 365 tenant and access Microsoft Endpoint Manager (Intune)
- Create and assign a Windows 11 Update Ring policy
- Create and assign a Windows 11 Compliance Policy
- Enroll a Windows 10 virtual machine into Intune
- Validate policy deployment, compliance status, and device registration

---

## 💻 Tools & Technologies
- Microsoft 365 Business Premium Trial
- Microsoft Endpoint Manager (Intune)
- Azure Active Directory (AAD)
- Windows 10 Virtual Machine (VirtualBox)

---

## 🧭 Project Steps

### 🔹 1. Setup & Environment
- Registered a free M365 Business Premium trial
- Created a test user and assigned an Intune license
  <img src="images/UserSetup.png" alt="img" width="800">
- Verified MDM auto-enrollment settings

### 🔹 2. Intune Policy Creation

#### ✅ Windows Update Ring
- Enabled automatic upgrade to Windows 11
- Configured update behavior (7-day deadline, 1-day grace)
- Assigned to **All Devices**
<br>
<b>Allow Microsoft Product Updates</b> - This ensures updates for Microsoft apps like Office, Edge, etc., are delivered along with Windows Updates
<b>Allow Windows driver</b> - Allows Windows Update to install updated hardware drivers <br>
<b> Quality update deferral period & Feature update deferral period</b> - We don't want any delays so I set it to 0.
<img src="images/RingSettings1.png" alt="img" width="600">
<br>
<b>Set feature update uninstall period (days) -> 10</b> - If a user runs into issues, they can roll back the OS upgrade within this number of days
<img src="images/RingSettings2.png" alt="img" width="600">
<br>
Deadline for feature updates -> 7. Devices must install Windows 11 within 7 days of poliy assignment
<br>
Deadline for quality updates -> 2. Security Patches must install within 2 days
<br>
Grace Period -> 1. After deadline passes, the user has 1 more day before reboot is forced.
<img src="images/RingSettings3.png" alt="img" width="600">

#### ✅ Compliance Policy
- Required minimum OS version: `10.0.22000.0` (Windows 11)
- Enforced BitLocker, Secure Boot, AV, and firewall
- Assigned to **All Devices**
<img src="images/Compliance1.png" alt="img">

<img src="images/Compliance3.png" alt="img" width="600">

<img src="images/Compliance4.png" alt="img" width="600">

<img src="images/Compliance5.png" alt="img" width="600">

<img src="images/Compliance7.png" alt="img" width="600">

### 🔹 3. Device Enrollment & Sync

#### VM Setup
- Created a Windows 10 VM in VirtualBox
- Set correct time zone and verified network access

#### Azure AD Join
- Joined the device using the test user under `Access work or school`

<img src="images/VMClientSetup1.png" alt="img" width="600">

However, at this step I encountered an error:

<img src="images/VMClientSetupError.png" alt="img" width="600">

To fix this I had to set WIP user scope to none since I’m not using any WIP policies it didn’t have any functional impact on me.
<br>
<img src="images/VMClientSetupErrorFix.png" alt="img" width="600">

<img src="images/VMClientSetup3.png" alt="img" width="600">

#### Device Enrollment Confirmation
<img src="images/VMClientSetup4.png" alt="img">

