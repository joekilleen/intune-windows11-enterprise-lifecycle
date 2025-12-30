# Conditional Access Enforcement Model  
**Identity-Centric Access Control Driven by Device Compliance**

---

## Purpose

This document defines the **authoritative Conditional Access (CA) model** that enforces device compliance for Windows 11 endpoints.

Conditional Access is the **enforcement engine** that:
- Converts compliance signals into access decisions
- Enforces Zero Trust regardless of network location
- Prevents data access from unhealthy or compromised devices

CA policies are **production-critical controls** and must be designed, tested, and changed with rigor.

---

## Conditional Access Design Objectives

The CA model must ensure:

1. **Identity-first enforcement**
2. **Device compliance as a hard requirement**
3. **Minimal policy overlap and ambiguity**
4. **Explicit exclusions with strong governance**
5. **Fail-closed behavior**

---

## Architectural Principles

- **Few, strong policies** over many weak ones
- **Device compliance required** for all user access
- **Platform-targeted** policies to reduce blast radius
- **Explicit admin protection**
- **No permanent bypasses**

---

## Policy Inventory (Authoritative)

| Policy ID | Name | Purpose |
|---|---|---|
| CA-01 | Require Compliant Device – Windows | Enforce device health |
| CA-02 | Require MFA – All Users | Identity assurance |
| CA-03 | Block Legacy Authentication | Eliminate weak auth |
| CA-04 | Admin Protection – Strong MFA | Privileged access |
| CA-05 | Enrollment Access Allowlist | Enable Autopilot/ESP |

---

## CA-01 — Require Compliant Device (Windows)

### Purpose
Block access to corporate cloud resources from non-compliant Windows devices.

---

### Policy Configuration  
**Exact UI Click-Path**

### Entra admin center
→ Protection
→ Conditional Access
→ Create new policy


---

### Assignments

#### Users

| Setting | Value |
---|---|
| Include | All users |
| Exclude | Break-glass accounts |

---

#### Cloud Apps

| Setting | Value |
---|---|
| Include | Microsoft 365, Azure, SaaS apps |
| Exclude | None |

---

#### Conditions

| Condition | Value |
---|---|
| Device platforms | Windows |
| Client apps | Browser, Mobile apps and desktop clients |
| Locations | Any |
| Device state | Any |

---

### Access Controls

| Control | Value |
---|---|
| Grant access | Require device to be marked as compliant |
| Additional controls | None |

---

### Enablement

| Setting | Value |
---|---|
| Policy state | On |

---

## CA-02 — Require MFA for All Users

### Purpose
Ensure strong authentication for all user access attempts.

---

### Assignments

| Setting | Value |
---|---|
| Include users | All users |
| Exclude users | Break-glass accounts |

---

### Access Controls

| Control | Value |
---|---|
| Grant | Require multi-factor authentication |

---

## CA-03 — Block Legacy Authentication

### Purpose
Eliminate authentication methods that bypass modern security controls.

---

### Assignments

| Setting | Value |
---|---|
| Include users | All users |
| Client apps | Legacy authentication clients |

---

### Access Controls

| Control | Value |
---|---|
| Grant | Block access |

---

## CA-04 — Admin Protection (Privileged Users)

### Purpose
Apply stronger authentication controls to privileged roles.

---

### Assignments

| Setting | Value |
---|---|
| Include | Directory roles (Admins) |
| Exclude | Break-glass accounts |

---

### Access Controls

| Control | Value |
---|---|
| Grant | Require MFA |
| Session | Sign-in frequency reduced |

---

## CA-05 — Enrollment and ESP Allowlist

### Purpose
Allow required enrollment endpoints while maintaining overall enforcement.

---

### Scope

| Area | Value |
---|---|
| Users | All users |
| Cloud apps | Microsoft Intune, Enrollment endpoints |
| Conditions | Device state = Unknown |

---

### Access Controls

| Control | Value |
---|---|
| Grant | Allow access |

**Rule**
This policy must be **narrowly scoped** and reviewed quarterly.

---

## Policy Evaluation Order

Conditional Access evaluates **all applicable policies** and enforces the **most restrictive outcome**.

| Scenario | Result |
---|---|
| Compliant + MFA | Access granted |
| Non-compliant | Access blocked |
| Legacy auth | Access blocked |
| Admin without MFA | Access blocked |

---

## Failure Modes and Mitigation

| Issue | Cause | Mitigation |
---|---|---|
| Users blocked during enrollment | CA-05 misconfigured | Fix allowlist |
| Unexpected access | Over-broad exclusions | Reduce scope |
| Admin lockout | Missing break-glass | Validate emergency access |
| App incompatibility | Legacy auth usage | Modernize app |

---

## Validation Checklist

- [ ] CA-01 blocks non-compliant devices
- [ ] MFA enforced for all users
- [ ] Legacy auth blocked
- [ ] Admins receive stronger controls
- [ ] Enrollment endpoints accessible
- [ ] Break-glass accounts tested

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| CA policy configuration | Entra ID |
| Sign-in logs | Entra ID |
| Block events | CA insights |
| Policy changes | Audit logs |

---

## Change Control

Conditional Access changes:
- Require security approval
- Must be validated in Pilot
- Must be documented in the Decision Log
- Must include rollback plan

---

## Summary

Conditional Access is the **final enforcement point** in the device lifecycle.

If Conditional Access is misconfigured, **all other controls can be bypassed**.

Correct CA design ensures that **only healthy devices operated by verified users shows up in production**.

---

## Next File

Proceed to:

**`docs/05-applications/12-application-lifecycle-architecture.md`**

This file defines the **Win32 application packaging, deployment, and versioning model**.
