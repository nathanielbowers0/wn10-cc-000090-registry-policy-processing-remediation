# Registry Policy Processing Remediation

## Overview

This project focused on configuring Windows registry policy processing settings to align with DISA STIG compliance requirements.

The remediation process included Group Policy configuration, registry-based hardening, and PowerShell automation to ensure registry policies continue processing even when Group Policy Objects (GPOs) have not changed.

---

## STIG Information

| Category | Details |
|---|---|
| STIG ID | WN10-CC-000090 |
| Severity | Medium |
| Platform | Windows 11 |
| Remediation Type | Group Policy Hardening & Registry Configuration |

---

## Requirement

Windows systems must properly configure registry policy processing settings to ensure security policies continue to apply consistently, even when Group Policy Objects have not changed.

---

## Manual Remediation Procedure

### Step 1 — Open Local Group Policy Editor

Launch:

```powershell
gpedit.msc
```

---

### Step 2 — Navigate to the Policy Location

```powershell
Computer Configuration → Administrative Templates → System → Group Policy
```

---

### Step 3 — Configure the Required Policy

Enable the following policy:

```powershell
Configure registry policy processing
```

Enable the option:

```powershell
Process even if the Group Policy objects have not changed
```

---

### Step 4 — Apply Policy Changes

Save and apply the updated policy configuration.

---

### Step 5 — Update Group Policy

Execute:

```powershell
gpupdate /force
```

to apply updated policy settings across the system.

---

### Step 6 — Validate Registry Configuration

Verify the following registry path:

```powershell
HKLM:\Software\Policies\Microsoft\Windows\System
```

Confirm the following registry values are configured:

```powershell
EnableRegistryPolicyProcessing = 1
RegistryPolicyProcessing = 1
```

---

## PowerShell Remediation Procedure

The PowerShell remediation automated the registry configuration process required to configure registry policy processing settings.

### PowerShell Actions Performed

- Verified required registry policy paths
- Created missing registry keys when necessary
- Configured registry policy processing settings
- Applied compliance registry values
- Validated successful configuration

---

### PowerShell Remediation Commands

```powershell
$RegPath = "HKLM:\Software\Policies\Microsoft\Windows\System"

$RegName1 = "EnableRegistryPolicyProcessing"
$RegName2 = "RegistryPolicyProcessing"

$RegValue1 = 1
$RegValue2 = 1

if (-not (Test-Path -Path $RegPath)) {
    New-Item -Path $RegPath -Force
}

Set-ItemProperty -Path $RegPath -Name $RegName1 -Value $RegValue1

Set-ItemProperty -Path $RegPath -Name $RegName2 -Value $RegValue2
```

---

## Technologies Utilized

- Windows 11
- PowerShell
- Windows Registry
- Group Policy
- DISA STIGs
- Vulnerability Management

---

## Skills Demonstrated

- Windows security hardening
- Group Policy configuration
- Registry-based remediation
- PowerShell automation
- Compliance validation
- Endpoint security configuration
- Security documentation
- Vulnerability remediation
