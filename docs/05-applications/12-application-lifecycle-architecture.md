# Application Lifecycle Architecture  
**Win32 Packaging, Deployment Strategy, and Version Governance**

---

## Purpose

This document defines the **authoritative application lifecycle architecture** for Windows 11 endpoints managed by Microsoft Intune.

It establishes how applications are:
- Packaged
- Deployed
- Updated
- Replaced
- Retired

in a way that is **deterministic, ESP-safe, and enforceable**.

Applications are treated as **security-relevant configuration**, not convenience tooling.

---

## Application Lifecycle Objectives

The application model must ensure:

1. **Predictable installation outcomes**
2. **No user dependency for required apps**
3. **Safe enrollment (ESP-compatible)**
4. **Deterministic detection and versioning**
5. **Controlled upgrades and rollbacks**
6. **Clear ownership and auditability**

---

## Supported Application Types (Authoritative)

| App Type | Supported | Notes |
---|---|---|
| Win32 (.intunewin) | Yes | Primary standard |
| Microsoft Store (new) | Limited | Non-critical apps only |
| Microsoft 365 Apps | Yes | Required baseline |
| MSI (native) | No | Must be wrapped |
| Scripts-only installs | No | Must be packaged |

**Rule**  
All line-of-business (LOB) applications **must** be packaged as Win32 apps.

---

## Application Lifecycle Stages

Every application progresses through the following stages:

1. Intake
2. Packaging
3. Validation
4. Deployment
5. Maintenance
6. Supersedence
7. Retirement

Skipping stages is not permitted.

---

## Stage 1 — Application Intake

### Required Intake Metadata

| Field | Description |
---|---|
| Application name | Canonical name |
| Version | Vendor version |
| Publisher | Vendor |
| Business owner | Accountable party |
| Deployment type | Required / Available |
| ESP suitability | Yes / No |
| Security impact | Low / Medium / High |

Applications without an owner **are not deployed**.

---

## Stage 2 — Packaging Standard (Win32)

### Packaging Requirements

| Requirement | Mandatory |
---|---|
| System context install | Yes |
| Silent install switches | Yes |
| Deterministic detection | Yes |
| Explicit uninstall command | Yes |
| No hard-coded paths | Yes |
| No user interaction | Yes |

---

### Naming Convention (Authoritative)

APP-W11-<Publisher>-<AppName>-<Version>
APP-W11-Microsoft-Edge-122.0


---

## Stage 3 — Validation

### Validation Environment

- Dedicated Pilot device group
- Representative hardware
- No production users

### Validation Criteria

- Install succeeds
- Detection evaluates correctly
- Uninstall works
- No reboot required (ESP-safe apps)
- No user prompts

Apps failing validation **do not advance**.

---

## Stage 4 — Deployment Strategy

### Assignment Types

| Assignment | Use Case |
---|---|
| Required | Security-critical or baseline apps |
| Available | Optional productivity tools |

---

### ESP Application Rules

Only **ESP-safe applications** may be assigned as **Required** during enrollment.

| ESP-Safe Criteria |
---|
| Install time < 10 minutes |
| No reboot |
| System context |
| Reliable detection |
| No external dependencies |

---

### Required App Categories

| Category | Timing |
---|---|
| Security agents | During ESP |
| Microsoft 365 Apps | During ESP |
| VPN bootstrap | During ESP (if required) |
| LOB apps | Post-ESP |

---

## Stage 5 — Maintenance

### Update Model

- New versions are **new app objects**
- Existing versions are not edited
- Version drift is corrected via supersedence

---

## Stage 6 — Supersedence (Mandatory)

### Supersedence Rules

| Rule | Requirement |
---|---|
| Direction | Old → New |
| Uninstall previous | Yes |
| Target | Same assignment scope |
| Validation | Required before production |

---

### Supersedence Use Cases

- Version upgrades
- Security patches
- Vendor re-packaging
- Application rebranding

---

## Stage 7 — Retirement

### Retirement Criteria

- Application no longer supported
- Superseded by new app
- Business owner approval

### Retirement Actions

1. Remove assignments
2. Validate uninstall
3. Archive documentation
4. Retain evidence

---

## Failure Handling

| Failure | Response |
---|---|
| Install failure | Fix package |
| Detection failure | Fix detection |
| ESP failure | Remove from ESP |
| Repeated issues | Retire app |

Manual fixes on endpoints are prohibited.

---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| App configuration | Intune |
| Assignment scope | Intune |
| Install success/failure | Intune reports |
| Supersedence chain | Intune |
| Retirement record | Change log |

---

## Change Control

Application changes:
- Require Pilot validation
- Must not modify production apps in place
- Must be logged in the Decision Log
- Must include rollback path

---

## Summary

This application lifecycle architecture ensures that:

- Applications are predictable
- Enrollment remains reliable
- Security posture is preserved
- Updates are controlled
- Rollbacks are possible
- Audits are straightforward

Applications that cannot meet these standards **do not belong in production**.

---

## Next File

Proceed to:

**`docs/05-applications/13-win32-packaging-standards.md`**

This file defines **exact packaging requirements, detection rules, and common anti-patterns**.
