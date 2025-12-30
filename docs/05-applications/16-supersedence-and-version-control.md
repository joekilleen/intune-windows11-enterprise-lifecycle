# Supersedence and Version Control  
**Application Upgrade Safety, Rollback Governance, and Drift Prevention**

---

## Purpose

This document defines the **authoritative supersedence and version control model** for Win32 applications deployed via Microsoft Intune.

Supersedence is the mechanism that ensures:
- Controlled application upgrades
- Predictable uninstall/install behavior
- Prevention of version drift
- Safe rollback during incidents

Editing applications in place is **explicitly prohibited**.

---

## Supersedence Design Objectives

The supersedence model must ensure:

1. **One version installed at a time**
2. **Explicit upgrade paths**
3. **Deterministic uninstall behavior**
4. **Safe rollback capability**
5. **Clear audit trails**

---

## Authoritative Rules (Non-Negotiable)

| Rule | Requirement |
---|---|
| New version | New Intune app object |
| Old version | Never edited in place |
| Supersedence direction | Old → New only |
| Uninstall previous | Always enabled |
| Testing | Mandatory before production |
| Rollback | Must be defined |

Violation of these rules introduces **silent drift and audit failure**.

---

## Supersedence Use Cases

Supersedence **must** be used for:

- Version upgrades
- Security patches
- Vendor re-packaging
- Installer technology changes
- Application rebranding or renaming

Supersedence **must not** be skipped for “minor” updates.

---

## Supersedence Configuration  
**Exact UI Click-Path**

### Intune admin center
→ Apps
→ Windows
→ Select new Win32 app
→ Properties
→ Supersedence
→ Edit


---

## Supersedence Configuration Standards

### Required Settings

| Setting | Value | Rationale |
---|---|---|
| Supersede | Previous version(s) | Explicit chain |
| Uninstall previous version | Yes | Prevent duplicates |
| Install behavior | System | Consistency |
| Target assignment | Same as previous | Predictable scope |

---

## Supersedence Chain Design

### Linear Chain (Preferred)

v1.0 → v1.1 → v1.2 → v1.3


### Parallel Chains (Prohibited)

v1.0 → v1.2
v1.1 → v1.2


Parallel chains create ambiguity and are not permitted.

---

## Rollback Strategy (Mandatory)

### Rollback Triggers

| Trigger | Example |
---|---|
| App crashes | Vendor defect |
| Security regression | Misconfiguration |
| Performance degradation | Resource leak |
| Compatibility failure | LOB conflict |

---

### Rollback Procedure

1. Remove assignments from new version
2. Reassign previous version
3. Validate uninstall/install sequence
4. Monitor remediation
5. Document incident

Rollback must **not** require manual endpoint work.

---

## Detection Versioning Requirements

Detection rules must:

- Match **exact version**
- Fail cleanly when version differs
- Be updated for each new version
- Never detect “any version”

**Anti-Pattern**
```text
Detect file exists → TRUE
```
This breaks supersedence and causes false success.

---

## Assignment Strategy During Supersedence

| Phase      | Assignment                  |
| ---------- | --------------------------- |
| Pilot      | New version only            |
| Production | Supersedence active         |
| Rollback   | Previous version reassigned |

Assignments must remain device-based.

---

## Supersedence and ESP

Critical Rule

No supersedence occurs during ESP.

- ESP-required apps must be version-pinned

- Supersedence occurs post-enrollment only

- New ESP versions require new Autopilot cycles

---

## Failure Modes and Mitigation

| Failure                   | Root Cause              | Mitigation        |
| ------------------------- | ----------------------- | ----------------- |
| App reinstall loop        | Bad detection           | Fix detection     |
| Multiple versions present | Uninstall disabled      | Enforce uninstall |
| Upgrade fails             | Vendor installer defect | Repackage         |
| Rollback fails            | Missing uninstall       | Fix package       |

Manual remediation is prohibited.

---

## Monitoring and Validation

| Signal            | Source               |
| ----------------- | -------------------- |
| Install success   | Intune app reports   |
| Uninstall success | Intune reports       |
| Version drift     | Endpoint Analytics   |
| Error trends      | App install failures |

---

## Evidence and Audit Artifacts

| Artifact                   | Source            |
| -------------------------- | ----------------- |
| Supersedence configuration | Intune            |
| App version inventory      | Intune            |
| Upgrade success metrics    | Intune            |
| Rollback actions           | Intune audit logs |
| Incident records           | Change log        |

---

## Change Control

Supersedence changes:

- Require Pilot validation

- Must be documented in the Decision Log

- Must include rollback testing evidence

- Must not overlap with ESP

---

## Summary

Supersedence is the only safe mechanism for managing application change at scale.

Without strict version control:

- ESP becomes unstable

- Devices drift

- Rollbacks fail

- Audits break

With proper supersedence:

- Upgrades are boring

- Rollbacks are fast

- Drift is eliminated

- Evidence is automatic
