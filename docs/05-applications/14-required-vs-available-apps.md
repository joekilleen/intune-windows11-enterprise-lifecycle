This document formalizes assignment strategy, ESP protection, and user experience boundaries, which is essential to keep enrollment reliable and audits defensible

# Required vs Available Applications  
**Assignment Strategy, ESP Protection, and User Experience Boundaries**

---

## Purpose

This document defines the **authoritative application assignment model** for Windows 11 endpoints managed by Microsoft Intune.

Correct use of **Required** versus **Available** assignments is critical to:
- Enrollment reliability
- Security posture enforcement
- Predictable user experience
- Reduced operational incidents

Misclassification of applications is one of the **most common causes of ESP failure**.

---

## Assignment Design Principles

1. **Minimum required footprint**
2. **Security before productivity**
3. **ESP is sacred**
4. **Users never install security controls**
5. **Optional apps must never block enrollment**

---

## Assignment Types Overview

| Assignment Type | Description | User Action |
---|---|---|
| Required | Automatically installed | None |
| Available | Optional via Company Portal | User-initiated |
| Uninstall | Forced removal | None |

---

## Required Applications (Authoritative Definition)

### Definition

Required applications are **non-optional components** necessary for:
- Security
- Compliance
- Device operability
- Baseline productivity

Users **cannot opt out**.

---

### Approved Required App Categories

| Category | Timing |
---|---|
| Microsoft 365 Apps | ESP |
| Company Portal | ESP |
| Security agents (Defender, EDR components) | ESP |
| VPN bootstrap (if required for compliance) | ESP |
| Device management utilities | ESP |
| Critical OS components | ESP |

---

### Prohibited as Required (During ESP)

| App Type | Reason |
---|---|
| Large LOB applications | Enrollment delays |
| Reboot-required installers | ESP failure |
| User-context apps | Breaks automation |
| Apps with unreliable detection | Non-deterministic |
| Apps requiring licenses per-user | Enrollment race conditions |

---

## ESP Protection Rules (Non-Negotiable)

- Only **ESP-safe** apps may be Required during enrollment
- Required apps during ESP must:
  - Install in <10 minutes
  - Require no reboot
  - Install in system context
  - Have deterministic detection

If an app breaks ESP **once**, it is removed from ESP permanently.

---

## Required Applications (Post-ESP)

Certain applications may be required **after** ESP completes.

### Examples

| App Type | Rationale |
---|---|
| Line-of-business apps | Productivity |
| Engineering tools | Role-based |
| Finance systems | Role-based |
| Admin tools | Restricted roles |

These apps:
- Are still Required
- Do **not** block enrollment
- May install in the background post-login

---

## Available Applications (Authoritative Definition)

### Definition

Available applications are:
- Optional
- User-initiated
- Non-critical to security or compliance

Failure to install **must not** impact compliance or access.

---

### Approved Available App Categories

| Category | Example |
---|---|
| Productivity tools | Visio, Project |
| Developer tools | IDEs |
| Utilities | File compression |
| Regional tools | Language packs |
| Training software | Optional learning apps |

---

### Available App Rules

- Must install in system context
- Must have deterministic detection
- Must not weaken security posture
- Must not modify baseline configurations

---

## Company Portal User Experience Boundaries

### Allowed

- User-initiated installs
- Viewing install status
- Self-service uninstall (where appropriate)

### Prohibited

- Installing security agents
- Bypassing Required apps
- Disabling managed software
- Elevation requests via app installs

---

## Assignment Scoping Strategy

| Scope | Usage |
---|---|
| Device groups | Required apps |
| User groups | Available apps |
| Dynamic rules | Role-based targeting |

**Rule**
Security and baseline apps are **never user-scoped**.

---

## Failure Modes and Impact

| Failure | Root Cause | Impact |
---|---|---|
| ESP timeout | Too many required apps | Enrollment failure |
| User blocked | Required LOB app failure | Access delay |
| App drift | Required app edited in place | Compliance issues |
| Support tickets | Poor Available app curation | Noise |

---

## Validation Checklist

- [ ] ESP-required apps reviewed quarterly
- [ ] Required apps limited to baseline only
- [ ] LOB apps assigned post-ESP
- [ ] Available apps tested via Company Portal
- [ ] Detection rules validated
- [ ] No user-context installs

---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| App assignments | Intune |
| ESP app list | Intune |
| Install success rates | Intune reports |
| Company Portal catalog | Device |

---

## Change Control

Assignment changes:
- Require Pilot validation
- Must not increase ESP risk
- Must be documented in the Decision Log
- Must include rollback plan

---

## Summary

Correct application assignment is the difference between:
- Fast, reliable enrollment
- And fragile, support-heavy environments

ESP must remain **minimal, predictable, and boring**.

---

## Next File

Proceed to:

**`docs/05-applications/15-supersedence-and-version-control.md`**

This file defines **upgrade, downgrade, and rollback governance** for applications.
