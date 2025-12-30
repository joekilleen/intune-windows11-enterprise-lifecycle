# ESP-Safe Application Design  
**Protecting Enrollment Integrity and Security Gating**

---

## Purpose

This document defines the **authoritative design standards for ESP-safe applications** in a Windows 11 Intune environment.

The Enrollment Status Page (ESP) is a **security gate**.  
Applications executed during ESP directly determine whether a device:

- Enters production securely
- Fails closed and is rebuilt
- Or silently bypasses intended controls

Any application that destabilizes ESP **undermines the entire device lifecycle**.

---

## Why ESP Safety Is a Security Requirement

ESP ensures that:

- Devices are fully secured **before first use**
- Compliance evaluation begins from a known-good state
- Conditional Access decisions are trustworthy

An unreliable ESP introduces:
- Partial configuration
- False compliance signals
- Undetected security gaps

Therefore, ESP safety is **non-negotiable**.

---

## Authoritative Definition: ESP-Safe Application

An ESP-safe application is one that:

- Installs silently and deterministically
- Requires no user context
- Requires no reboot
- Completes quickly and reliably
- Can be validated with absolute certainty

If any of these conditions are not met, the application is **not ESP-safe**.

---

## Mandatory ESP-Safe Criteria (ALL REQUIRED)

| Criterion | Requirement |
---|---|
| Install context | System |
| User interaction | None |
| Reboot required | No |
| Install duration | < 10 minutes |
| Detection logic | Deterministic |
| External dependencies | None beyond vendor CDN |
| Licensing | Machine-based |
| Failure behavior | Clean failure with exit code |

Failure on **any single criterion** disqualifies the app.

---

## Approved ESP-Safe Application Categories

| Category | Examples |
---|---|
| Microsoft 365 Apps | Core productivity |
| Company Portal | Self-service |
| Security agents | Defender components |
| VPN bootstrap | Pre-auth connectivity (if required) |
| Management extensions | IME dependencies |

These applications are foundational and tightly controlled.

---

## Explicitly Prohibited During ESP

| Application Type | Reason |
---|---|
| Large LOB applications | Timeout risk |
| Reboot-required installers | ESP failure |
| User-context installers | Breaks automation |
| Apps with flaky detection | False success |
| Apps requiring user licensing | Race conditions |
| Apps chaining multiple installers | Non-deterministic |

These applications **must be post-ESP** or Available only.

---

## Design Pattern: ESP-Safe Packaging

### Required Characteristics

- Single entry install script
- Explicit exit codes
- Version-specific detection
- Logging enabled
- No retries or “best effort” logic

---

### Example ESP-Safe Install Flow

```text
Install.ps1
 ├─ Validate prerequisites
 ├─ Execute silent installer
 ├─ Validate installation state
 ├─ Write log
 └─ Exit 0 or non-zero
```
No branching based on user state is permitted.

---

## Detection Design (Critical)

### Detection rules must:

- Identify one and only one version

- Be immune to timing issues

- Not rely on services starting later

- Not rely on user logon

## Approved Detection Signals

- Registry value + version

- File version + path

- MSI product code (wrapped only)

File-existence-only detection is prohibited.

---

## Failure Handling Philosophy
### ESP failures are not retried endlessly.

| Scenario             | Outcome   |
| -------------------- | --------- |
| App fails to install | ESP fails |
| Detection fails      | ESP fails |
| Timeout reached      | ESP fails |
| Reboot requested     | ESP fails |

Correct response:
Fix the app → Re-enroll the device.

Manual fixes are prohibited.

---

## ESP App Count Guidance

| Metric                   | Recommendation |
| ------------------------ | -------------- |
| Required apps during ESP | ≤ 5            |
| Total ESP install time   | < 30 minutes   |
| ESP failures tolerated   | 0              |

If ESP becomes slow or fragile, reduce scope immediately.

---

$$ Testing Requirements

Before any app is marked ESP-safe:

 - Installed on clean Autopilot device

 - Installed at least 3 times successfully

 - Tested on lowest-spec hardware

 - Detection validated across reboots

 - Failure path verified

Pilot success does not imply ESP safety.

---

## Governance Rules

- ESP-safe status must be explicitly approved

- ESP-safe apps reviewed quarterly

- Any ESP incident triggers immediate review

- Apps may be permanently banned from ESP

---

## Evidence and Audit Artifacts

| Artifact                      | Source          |
| ----------------------------- | --------------- |
| App assignment (ESP-required) | Intune          |
| ESP app list                  | Intune          |
| Enrollment success metrics    | Intune          |
| Failure logs                  | Device + Intune |
| Change approvals              | Decision Log    |

---

## Common ESP Failure Root Causes

| Root Cause         | Prevention                |
| ------------------ | ------------------------- |
| Overloading ESP    | Minimal required apps     |
| Weak detection     | Version-specific rules    |
| Hidden reboots     | Strict exit code handling |
| Network dependency | Localized installers      |
| Licensing delays   | Machine-based licensing   |

---

## Summary

ESP is the front door to production.

Every application executed during ESP must be:

- Predictable

- Fast

- Silent

- Boring

- Trustworthy

If an application cannot meet this bar, it does not belong in ESP.
