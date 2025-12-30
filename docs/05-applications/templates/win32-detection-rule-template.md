This template is designed to enforce deterministic, version-specific detection and to eliminate the most common causes of Win32 deployment failures and ESP instability.

# Win32 Detection Rule Template  
**Deterministic Version Detection and Compliance Signaling**

---

## Purpose

This document provides the **authoritative template** for defining and validating Win32 application detection rules in Microsoft Intune.

Detection rules are the **single source of truth** for whether an application is considered:
- Installed
- Failed
- Superseded
- Compliant

Weak or ambiguous detection rules are the **primary cause** of:
- Reinstall loops
- ESP failures
- False compliance
- Broken supersedence chains

---

## Detection Design Principles

All detection rules must be:

1. **Deterministic**
2. **Version-specific**
3. **System-context safe**
4. **Idempotent**
5. **Audit-friendly**

If a detection rule cannot **prove** the installed version, it is invalid.

---

## Approved Detection Methods (Priority Order)

| Priority | Method | Notes |
---|---|---|
| 1 | Registry value + exact version | Preferred |
| 2 | File version + path | Acceptable |
| 3 | MSI product code | Wrapped only |
| 4 | Script-based detection | Last resort |

**Anti-Pattern**  
Detecting “any version installed” is prohibited.

---

## Application Metadata

| Field | Value |
---|---|
| Application Name |  |
| Publisher |  |
| Version |  |
| Intune App Name |  |
| Detection Method | (Registry / File / MSI / Script) |

---

## Detection Rule Definition

### Option A — Registry-Based Detection (Preferred)

**Registry Path**
HKLM\Software<Vendor><Application>

**Value Name**


**Expected Value**

<Exact version string> ```

### Detection Logic

$expectedVersion = "<ExactVersion>"
$keyPath = "HKLM:\Software\<Vendor>\<Application>"

if (Test-Path $keyPath) {
    $installedVersion = (Get-ItemProperty $keyPath).Version
    if ($installedVersion -eq $expectedVersion) {
        exit 0
    }
}

exit 1

---

## Option B — File Version Detection

C:\Program Files\<Vendor>\<Application>\<binary>.exe

File Path

C:\Program Files\<Vendor>\<Application>\<binary>.exe

Expected File Version

<Exact version>

Detection Logic

$filePath = "C:\Program Files\<Vendor>\<Application>\<binary>.exe"
$expectedVersion = "<ExactVersion>"

if (Test-Path $filePath) {
    $version = (Get-Item $filePath).VersionInfo.FileVersion
    if ($version -eq $expectedVersion) {
        exit 0
    }
}

exit 1

---

## Option C — MSI Product Code Detection

MSI Product Code
{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}

Detection Logic

$productCode = "{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"
$installed = Get-WmiObject Win32_Product |
    Where-Object { $_.IdentifyingNumber -eq $productCode }

if ($installed) {
    exit 0
}

exit 1

MSI detection is allowed only when MSI is wrapped and version-specific.

---

## Option D — Script-Based Detection (Last Resort)

Script-based detection is permitted only when:

- Registry keys do not exist

- File versioning is unreliable

- MSI detection is unavailable

Script Requirements

- Explicit exit codes

- No user context

- No environment assumptions

- No external calls

Detection Logic

# Custom logic here
# Must return exit 0 for installed, exit 1 for not installed

---

## Detection Rule Validation Checklist

| Check                                     | Status |
| ----------------------------------------- | ------ |
| Detection uniquely identifies one version | ☐      |
| Detection fails for other versions        | ☐      |
| Detection survives reboot                 | ☐      |
| Detection works without user logon        | ☐      |
| Detection tested on clean device          | ☐      |
| Detection tested after uninstall          | ☐      |

---

## Supersedence Compatibility

Before enabling supersedence:

 Old version detection confirmed

 New version detection confirmed

 Detection logic updated per version

 No overlap between version detections

 Rollback detection validated

 ---

 ## Common Detection Anti-Patterns (Prohibited)

 | Anti-Pattern                | Impact              |
| --------------------------- | ------------------- |
| File existence only         | False positives     |
| Registry key existence only | Version drift       |
| Wildcard version matching   | Broken supersedence |
| User profile paths          | ESP failures        |
| Service running checks      | Timing issues       |

---

## Troubleshooting Detection Failures

1. Run detection script locally as SYSTEM

2. Verify exact version values

3. Confirm registry/file permissions

4. Test pre-install and post-uninstall

5. Review Intune install status details

Do not “fix” detection by broadening conditions.

---

## Evidence and Audit Artifacts

| Artifact                     | Source         |
| ---------------------------- | -------------- |
| Detection rule configuration | Intune         |
| Detection test results       | Packaging logs |
| Supersedence chain           | Intune         |
| Install state                | Intune reports |

---

## Change Control

Detection rule changes:

- Require re-validation

- Must be tested in Pilot

- Must be documented in the Decision Log

- Must align with supersedence strategy

---

## Summary

Detection rules are the gatekeepers of reliability.

If detection is weak:

- ESP breaks

- Supersedence fails

- Compliance lies

- Rollbacks are impossible

Strong detection makes everything else boring and predictable.

---

## Status

☐ Detection Rule Drafted

☐ Validated

☐ Approved

☐ Archived (Application Retired)

---
