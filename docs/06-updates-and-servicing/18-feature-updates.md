# Feature Update Policy  
**Windows 11 Version Pinning, Promotion, and Rollback Governance**

---

## Purpose

This document defines the **authoritative feature update management model** for Windows 11 devices using Microsoft Intune.

Feature updates introduce:
- New functionality
- Platform changes
- Potential compatibility risk

Therefore, feature updates are **explicitly governed**, not delivered opportunistically.

---

## Feature Update Design Objectives

The feature update strategy must ensure:

1. **No surprise OS upgrades**
2. **Explicit version approval**
3. **Controlled blast radius**
4. **Clear rollback capability**
5. **Audit-ready evidence**

---

## Feature Update Governance Principles

- Feature updates are **pinned**, not deferred indefinitely
- Only **approved versions** are allowed
- Promotion occurs **ring by ring**
- Rollback is planned **before promotion**
- Feature updates are treated as **platform changes**

---

## Supported Windows 11 Versions

| State | Description |
---|---|
| Approved | Current production version |
| Pilot | Next candidate version |
| Blocked | Unsupported or unapproved versions |

Only **Approved** and **Pilot** versions are allowed to exist in the tenant.

---

## Feature Update Policy Creation  
**Exact UI Click-Path**

### Intune admin center
→ Devices
→ Windows
→ Feature updates for Windows 10 and later
→ Create profile


---

## Feature Update Policy Configuration  
**Field-by-Field (Authoritative Baseline)**

### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | FU-W11-Prod-<Version> | Deterministic naming |
| Description | Windows 11 feature update pinning | Audit clarity |
| Platform | Windows 10 and later | Applies to Windows 11 |

---

### Feature Update Settings

| Setting | Value | Rationale |
---|---|---|
| Feature update version | Windows 11 <Version> | Explicit pin |
| Rollout options | Immediate | Controlled by assignment |
| Windows edition | Enterprise | Licensing alignment |

---

## Feature Update Promotion Model

### Phase 1 — Pilot

| Aspect | Configuration |
---|---|
| Target | Pilot ring devices |
| Coverage | 1–5% |
| Validation period | 30–60 days |
| Exit criteria | Stability + app compatibility |

---

### Phase 2 — Broad

| Aspect | Configuration |
---|---|
| Target | Broad ring devices |
| Coverage | 10–20% |
| Validation period | 30 days |
| Exit criteria | No blocking issues |

---

### Phase 3 — Enterprise

| Aspect | Configuration |
---|---|
| Target | Enterprise ring devices |
| Coverage | Remaining fleet |
| Validation period | Ongoing |
| Exit criteria | Platform baseline updated |

---

## Rollback Strategy (Mandatory)

### Rollback Triggers

| Trigger | Example |
---|---|
| App incompatibility | LOB failure |
| Performance degradation | CPU or memory regression |
| Security regression | Control failure |
| Vendor advisory | Platform issue |

---

### Rollback Methods

| Method | Use Case |
---|---|
| Windows rollback window | Immediate post-upgrade |
| Device reset | Persistent instability |
| Version re-pin | Controlled downgrade |

**Rule**  
Rollback must not rely on manual device intervention.

---

## Interaction with Update Rings

| Control | Responsibility |
---|---|
| Update rings | Quality updates |
| Feature update policy | OS version |
| Compliance policy | Minimum OS version |
| Conditional Access | Enforces currency |

Feature update policies **override deferral behavior**.

---

## Compliance and Enforcement

| Signal | Enforcement |
---|---|
| OS version below minimum | Non-compliant |
| OS version above approved | Non-compliant |
| Update failure | Remediation required |

Devices outside approved versions **lose access**.

---

## Failure Modes and Mitigation

| Failure | Cause | Mitigation |
---|---|---|
| Devices upgrade early | No pin policy | Apply pin immediately |
| Devices stuck upgrading | Driver conflict | Pause ring, remediate |
| Rollback fails | Window expired | Reset device |
| Version drift | Multiple policies | Consolidate |

---

## Validation Checklist

- [ ] Feature update pinned
- [ ] Pilot devices upgraded first
- [ ] Apps validated on new version
- [ ] Rollback tested
- [ ] Compliance reflects OS version

---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| Feature update policy | Intune |
| Device OS version inventory | Intune |
| Promotion timelines | Change records |
| Rollback actions | Intune audit logs |

---

## Change Control

Feature update changes:
- Require formal change approval
- Must be validated in Pilot
- Must be documented in the Decision Log
- Must include rollback testing evidence

---

## Summary

Feature updates are **platform changes**, not routine patches.

By pinning versions and promoting deliberately:
- Stability is preserved
- Risk is controlled
- Compliance is enforceable
- Audits are defensible

---

## Next File

Proceed to:

**`docs/06-updates-and-servicing/19-driver-and-firmware-strategy.md`**

This file defines **driver and firmware update governance and risk controls**.
