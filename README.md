<img width="1672" height="941" alt="ChatGPT Image May 24, 2026, 03_40_01 PM" src="https://github.com/user-attachments/assets/010e2ba5-2178-4157-9ce9-4bc1a9b38767" />

Read Articles;
TR: https://lnkd.in/eW25_pqY
EN: https://lnkd.in/eQfNi5eV

# Release Notes;
## 🚀 Endpoint Troubleshooter v1.2 

* Health Rule Engine — Dashboard now shows severity-ranked findings (Critical / Warning / Info / OK) with a concrete recommendation per finding. Rules cover signature age, passive mode without a 3rd-party AV, missing PRT, expiring certificates, stale sensor connection, * BitLocker/TPM/Secure Boot and more.
* Device Health panel — Compliance-relevant checks in one place: BitLocker, TPM, Secure Boot, VBS/HVCI, Credential Guard, LSA Protection (RunAsPPL), Network Protection/SmartScreen, pending reboot, uptime, time sync (w32tm) and last Windows Update success.
* Identity checks — Azure AD PRT status & expiry, Intune MDM device certificate and MS-Organization-Access (AAD device) certificate with expiry evaluation.
* MDE deep-dive — Last connected time, sensor (MsSense.exe) version, running mode, device tag, SenseCM state, third-party AV detection and MAPS/cloud validation via MpCmdRun -ValidateMapsConnection.
* Enrollment error decoding — Device Management events (e.g. 0x80180026, 0x8018002a, 0xcaa9001f) are translated into plain-language causes.
* IME log summary — Recent Win32 app activity and errors, plus scheduled task LastRunTime/LastResult.
* Co-management / Autopilot / WNS checks.
* JSON export and a headless mode (-NoGui / -ExportJson) suitable for Intune remediation scripts (non-zero exit on critical findings).
* Support bundle now includes MDM Diagnostics report, health findings, device-health snapshot and a sensitive-data warning.
🔧 Updated
* MDE connectivity test uses streamlined (post-2023) endpoints (*.endpoint.security.microsoft.com, x.cp.wd.microsoft.com, events.data.microsoft.com) alongside legacy gateways.
* Refreshed UI — color-coded status cards, styled data grids and severity-colored findings.
* Global TLS 1.2 and per-run transcript logging.

## 🚀 Endpoint Troubleshooter v1.1.0

Endpoint Troubleshooter **v1.1.0** is now available.

This release focuses on improving the quality of exported reports and adding better local policy visibility for Defender and Intune-managed endpoints.

---

### What's New

#### Enhanced Export Summary

The **Export Summary** output has been improved with a more detailed and structured HTML report.

The report now includes:

* Report generation date and time
* Device information
* Microsoft Defender Antivirus status
* Microsoft Defender for Endpoint / Sense details
* Intune Management Extension details
* Identity and enrollment information
* Network, proxy and firewall details
* Recent Defender, Sense and Device Management events
* Dashboard quick findings

This makes the exported report more useful for troubleshooting, documentation, support cases and internal investigations.

---

#### Local Policy Evidence

A new **Local Policy Evidence** section has been added.

This section provides local visibility into policy evidence available on the endpoint, including:

* Defender effective settings
* Defender policy registry evidence
* Intune / MDM PolicyManager evidence
* Recent Device Management policy events

> ASR rules are intentionally excluded from this section because they already have a dedicated ASR view in the tool.

---

### Notes

This release focuses on **local endpoint evidence**.

It does not yet correlate local settings with Intune policy display names from the cloud. Cloud-side policy correlation may be added in a future release with Microsoft Graph integration.

---

### Update

```powershell
Update-Module EndpointTroubleshooter
```

---

### Install

```powershell
Install-Module EndpointTroubleshooter -Scope CurrentUser
Start-EndpointTroubleshooter
```

---

### Version

```text
Current version: 1.1.0
```


EndpointTroubleshooter is a Windows PowerShell GUI toolkit for troubleshooting Microsoft-managed Windows endpoints from a single interface.

It helps administrators and support engineers quickly inspect Microsoft Defender Antivirus, Microsoft Defender for Endpoint, Intune Management Extension, device join and MDM enrollment, network/proxy settings, Windows Firewall state, logs, and support data collection workflows.

## What this tool can do

EndpointTroubleshooter provides a step-by-step diagnostic experience across these areas:

- **Dashboard / overview**
  - Shows a quick health summary for Defender AV, Microsoft Defender for Endpoint, and Intune Management Extension
  - Aggregates key findings for the current device
- **Microsoft Defender Antivirus**
  - Reads engine, platform, service, and signature versions
  - Shows protection status such as real-time protection, behavior monitoring, IOAV, and tamper protection
  - Lists Defender exclusions
- **Microsoft Defender for Endpoint (MDE)**
  - Checks Sense service status
  - Shows onboarding state, org/tenant details, device ID, and proxy information
  - Displays recent Sense events
- **Attack Surface Reduction (ASR)**
  - Reads configured ASR rules and their state
  - Captures a Defender security preference snapshot
- **Intune / IME**
  - Checks Intune Management Extension service, folder, binary version, and recent log activity
  - Lists EnterpriseMgmt enrollment tasks
  - Can trigger Intune / MDM sync-related tasks
- **Identity & enrollment**
  - Reads `dsregcmd /status` output
  - Shows Azure AD join, domain join, tenant, device ID, and MDM URL
  - Enumerates enrollment registry entries
- **Network and proxy**
  - Collects IP, gateway, DNS, and proxy information
  - Helps validate connectivity-related issues
- **Windows Firewall**
  - Displays firewall profiles and blocked connection events
- **Logs and events**
  - Provides quick access to logs and collected events
- **Tools and actions**
  - Refreshes all checks
  - Restarts Defender or Sense-related services
  - Exports an HTML summary report
  - Builds a support bundle
  - Checks latest Microsoft Defender versions
  - Updates Defender signatures
  - Runs Defender Performance Analyzer
  - Runs MDE Client Analyzer

## Requirements

- Windows 10/11 or Windows Server with Desktop Experience
- Windows PowerShell **5.1**
- Administrator permissions recommended for full functionality
- Internet connectivity for Microsoft-hosted downloads and version checks

## Installation

Install from PowerShell Gallery

```powershell
Install-Module EndpointTroubleshooter -Scope CurrentUser
Start-EndpointTroubleshooter
```

## Public command

```powershell
Start-EndpointTroubleshooter [-SkipAdminCheck] [-ReportFolder <path>]
```

### Parameters

- `-SkipAdminCheck`: Opens the UI without blocking when PowerShell is not elevated. Some actions may fail without administrator rights.
- `-ReportFolder`: Sets a custom folder for reports, support bundles, analyzer outputs, and exported files. Default: `%ProgramData%\EndpointTroubleshooter`

## Step-by-step usage

### 1. Open PowerShell as Administrator
For the best experience, launch **Windows PowerShell 5.1** as Administrator.

### 2. Start the tool
If installed from Gallery:

```powershell
Start-EndpointTroubleshooter
```

If running locally from source:

```powershell
Import-Module .\EndpointTroubleshooter\EndpointTroubleshooter.psd1 -Force
Start-EndpointTroubleshooter
```

### 3. Review the Dashboard first
When the GUI opens:

- Start on **Dashboard / Overview**
- Review quick health indicators for:
  - Defender AV
  - Microsoft Defender for Endpoint
  - Intune Management Extension
- Read the **Quick Findings** section for a summarized device snapshot

### 4. Validate Microsoft Defender Antivirus
Open **Defender Antivirus** and review:

- Engine version
- Product/platform version
- Signature version
- Real-time protection status
- Behavior monitoring
- IOAV protection
- Tamper protection
- Exclusions

Use this section when you suspect outdated signatures, disabled protection, or exclusion-related issues.

### 5. Validate Microsoft Defender for Endpoint
Open **Microsoft Defender for Endpoint** and review:

- Sense service status
- Onboarding state
- Org / tenant ID
- Device ID
- Proxy information
- Recent Sense events

Use this section for sensor health, onboarding, and connectivity troubleshooting.

### 6. Review ASR configuration
Open **Attack Surface Reduction** and check:

- Which ASR rules are configured
- Whether they are in block, audit, warn, or disabled mode
- The Defender security preference snapshot

This helps when validating hardening baselines or explaining prevention behavior.

### 7. Check Intune Management Extension
Open **Intune Management** and review:

- IME service status
- Install folder and binary version
- Latest IME log activity
- EnterpriseMgmt scheduled tasks

Use the Intune action area if you want to trigger sync-related tasks or confirm IME health.

### 8. Check identity and enrollment
Open **Identity & Enrollment** and review:

- Azure AD joined state
- Domain joined state
- Tenant information
- Device ID
- MDM URL
- Enrollment registry entries
- Raw `dsregcmd /status` output when needed

Use this section for join, registration, and MDM enrollment issues.

### 9. Review network and proxy information
Open **Network and Proxy** and confirm:

- IP configuration
- Gateway and DNS settings
- WinHTTP proxy configuration
- User proxy configuration
- Connectivity-related outputs

Use this section when Defender, MDE, Intune, or enrollment workflows appear blocked by networking or proxy issues.

### 10. Review Windows Firewall state
Open **Windows Firewall** and inspect:

- Active firewall profiles
- Default inbound/outbound actions
- Logged blocked connection events

This helps determine whether firewall policy may be blocking required traffic.

### 11. Check logs and events
Open **Logs and Events** to:

- View collected event information
- Access relevant diagnostic outputs quickly

This is useful for evidence gathering before escalation.

### 12. Run actions when deeper diagnostics are needed
Open **Tools and Actions** to perform guided actions such as:

- **Refresh All Checks** to reload the current device state
- **Export HTML Report** to generate a shareable summary
- **Collect Support Bundle** to package diagnostic data
- **Check for Latest Versions** to compare local Defender versions with Microsoft-published versions
- **Update Defender Signatures** if the endpoint is behind
- **Run Performance Analyzer** to capture Defender scan performance data
- **Run MDE Client Analyzer** to collect MDE client diagnostics

## Output files

By default, generated files are written under:

```text
%ProgramData%\EndpointTroubleshooter
```

This can include:

- HTML reports
- Support bundles
- Performance Analyzer recordings and reports
- MDE Client Analyzer output


## Typical use cases

- Defender AV health validation
- Microsoft Defender for Endpoint onboarding checks
- Intune Management Extension troubleshooting
- Azure AD join / MDM enrollment diagnostics
- Proxy and connectivity troubleshooting
- Firewall review
- Collecting support evidence before escalation
- Comparing local Defender versions with Microsoft’s latest published versions
- Capturing Defender performance diagnostics

## Notes

- Run as Administrator for full functionality.
- The module imports without automatically launching the GUI. The interface opens only when `Start-EndpointTroubleshooter` is called.
- The tool is designed for **Windows PowerShell 5.1+** on Windows endpoints.
- Do not commit secrets, tenant-specific values, customer names, API keys, or internal URLs to this repository.
