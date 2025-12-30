# Win32 Packaging Standards  
**Deterministic Installation, Detection, and Removal**

---

## Purpose

This document defines the **authoritative Win32 application packaging standards** for Windows 11 devices managed by Microsoft Intune.

These standards exist to ensure:
- Reliable installation outcomes
- Predictable detection logic
- Safe Enrollment Status Page (ESP) behavior
- Clean upgrades and removals
- Clear troubleshooting and auditability

Any application that does not meet these standards **must not be deployed**.

---

## Packaging Philosophy

Win32 applications are treated as **infrastructure components**, not ad-hoc software.

Key principles:

1. **System-context execution only**
2. **Silent, non-interactive installs**
3. **Deterministic detection**
4. **Explicit uninstall capability**
5. **Idempotent behavior**
6. **ESP safety by design**

---

## Packaging Tooling (Approved)

| Tool | Purpose |
---|---|
| IntuneWinAppUtil.exe | Package creation |
| PowerShell (signed) | Install / uninstall wrappers |
| Vendor installers | Only when silent switches supported |

**Prohibited**
- Batch files
- Unsigned scripts
- MSI deployed directly without wrapping

---

## Package Structure Standard

/Source
/Install.ps1
/Uninstall.ps1
/Detection.ps1 (if script-based detection)
/Payload
<Vendor installer files>


**Rules**
- Scripts must be UTF-8
- Scripts must exit deterministically
- Logging is mandatory

---

## Install Command Standard

### Required Characteristics

| Requirement | Mandatory |
---|---|
| System context | Yes |
| Silent switches | Yes |
| No reboot | Yes (ESP-safe apps) |
| Exit code handling | Yes |
| Logging | Yes |

---

### Example Install Command

```text
powershell.exe -ExecutionPolicy Bypass -File Install.ps1
```
---

## Uninstall Command Standard

| Requirement               | Mandatory |
| ------------------------- | --------- |
| Fully removes application | Yes       |
| Silent                    | Yes       |
| Idempotent                | Yes       |
| No user prompts           | Yes       |

---

## Example Uninstall Command

powershell.exe -ExecutionPolicy Bypass -File Uninstall.ps1

---

## Detection Rules (Critical)
### Detection rules are the single most important factor in Win32 reliability.

Approved Detection Methods

| Method                   | Allowed           |
| ------------------------ | ----------------- |
| File existence + version | Yes               |
| Registry key + version   | Yes               |
| MSI product code         | Yes               |
| Script-based detection   | Yes (last resort) |

---

## Detection Requirements

- Must uniquely identify one version
- Must survive reboot
- Must not rely on user profile paths
- Must return consistent exit codes

---

## Example Detection Logic (Registry)

$Version = (Get-ItemProperty `
  "HKLM:\Software\Vendor\App").Version
if ($Version -eq "5.4.2") { exit 0 } else { exit 1 }

---

## ESP Safety Rules

Only applications that meet all criteria below may be required during ESP.

| Criterion                               | Required |
| --------------------------------------- | -------- |
| Install time < 10 minutes               | Yes      |
| No reboot                               | Yes      |
| No network dependency beyond vendor CDN | Yes      |
| Deterministic detection                 | Yes      |
| System context                          | Yes      |

---

Rule
If an app ever breaks ESP, it is permanently removed from ESP.

---

## Exit Code Handling

| Exit Code | Meaning                             |
| --------- | ----------------------------------- |
| 0         | Success                             |
| 3010      | Soft reboot required (not ESP-safe) |
| Non-zero  | Failure                             |

Applications returning reboot codes must not be used during ESP.

---

## Logging Standard
### Requirements

- Logs written to %ProgramData%\Company\AppName

- Timestamped

- Include install start, success/failure, and exit code

### Example
C:\ProgramData\Company\Edge\install.log

---

## Supersedence Readiness Checklist

Before an app can supersede another:

 Old version uninstalls cleanly

 New version installs silently

 Detection rules are version-specific

 Rollback path exists

 Pilot validation complete

 ---

 ## Common Anti-Patterns (Prohibited)

 | Anti-Pattern                    | Reason                 |
| ------------------------------- | ---------------------- |
| Editing production app in place | Breaks rollback        |
| File-only detection             | Causes false positives |
| User-context installs           | Breaks ESP             |
| Hard-coded paths                | Fragile                |
| Reboot-required apps in ESP     | Enrollment failure     |
| “Install then fix” scripts      | Non-deterministic      |

---

## Troubleshooting Guidance

When troubleshooting app failures:

- Validate detection logic first

- Review Intune install logs

- Review custom install logs

- Test uninstall independently

- Rebuild package if necessary

- Do not fix applications manually on endpoints.

---

## Evidence and Audit Artifacts

| Artifact                  | Source            |
| ------------------------- | ----------------- |
| App package configuration | Intune            |
| Install / failure reports | Intune            |
| Detection rules           | Intune            |
| Supersedence chain        | Intune            |
| Logs                      | Device filesystem |

---

## Change Control

Win32 packaging changes:

- Require Pilot validation

- Must not modify production apps in place

- Must be logged in the Decision Log

- Must include rollback plan

---

## Summary

Strict Win32 packaging standards are the difference between:

- Reliable automation

- And fragile, technician-dependent environments

- If packaging is inconsistent, everything upstream breaks.

---

## Next File

Proceed to:

docs/05-applications/14-required-vs-available-apps.md

This file defines assignment strategy, user experience boundaries, and ESP protection rules.
