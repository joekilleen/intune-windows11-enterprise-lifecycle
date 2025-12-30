# Windows Update for Business Rings  
**Quality Updates, Feature Updates, and Deadline Enforcement**

---

## Purpose

This document defines the **authoritative Windows Update for Business (WUfB) ring architecture** for Windows 11 devices managed by Microsoft Intune.

The update ring model ensures that:
- Security updates are applied within defined SLAs
- Feature updates are introduced in a controlled manner
- Blast radius is minimized through staged deployment
- Update compliance is enforceable and auditable

Updates are treated as **security controls**, not user preferences.

---

## Update Design Objectives

The update strategy must ensure:

1. **Predictable rollout**
2. **Minimal blast radius**
3. **Clear validation stages**
4. **Enforced deadlines**
5. **User impact managed, not avoided**
6. **Audit-ready evidence**

---

## Update Governance Principles

- Updates are **device-scoped**
- Rings are **progressive**, not parallel free-for-all
- Deadlines are mandatory
- User deferral is limited
- Emergency response overrides convenience

---

## Ring Model Overview (Authoritative)

| Ring | Purpose | Approx. Coverage |
---|---|---|
| Ring 0 — Pilot | Early validation | 1–5% |
| Ring 1 — Broad | Business validation | 10–20% |
| Ring 2 — Enterprise | Full production | 75–90% |

Devices must progress **forward only** through rings.

---

## Ring Assignment Strategy

| Ring | Assignment Method |
---|---|
| Pilot | Static or tightly scoped dynamic device group |
| Broad | Dynamic device group |
| Enterprise | Dynamic device group |

**Rule**  
Ring membership is **device-based**, not user-based.

---

## Quality Update Ring Configuration  
**Exact UI Click-Path**

### Intune admin center
→ Devices
→ Windows
→ Update rings for Windows 10 and later
→ Create profile


---

## Quality Update Ring Settings (Authoritative)

### Common Settings (All Rings)

| Setting | Value | Rationale |
---|---|---|
| Microsoft product updates | Allow | Office + OS |
| Windows drivers | Controlled separately | Stability |
| Quality update deferral | Ring-specific | Staged rollout |
| Feature update deferral | Ring-specific | Governance |
| Automatic update behavior | Auto install and restart | Enforcement |
| User pause access | Disabled | Prevent bypass |

---

### Ring-Specific Deferrals and Deadlines

#### Ring 0 — Pilot

| Setting | Value |
---|---|
| Quality update deferral | 0 days |
| Deadline for quality updates | 2 days |
| Grace period | 1 day |
| Auto-restart before deadline | Allowed |

---

#### Ring 1 — Broad

| Setting | Value |
---|---|
| Quality update deferral | 5 days |
| Deadline for quality updates | 5 days |
| Grace period | 2 days |

---

#### Ring 2 — Enterprise

| Setting | Value |
---|---|
| Quality update deferral | 10 days |
| Deadline for quality updates | 7 days |
| Grace period | 2 days |

---

## Feature Update Governance

Feature updates are **not** delivered via deferral alone.

### Feature Update Control Model

- Feature updates are pinned using **Feature Update policies**
- Devices remain on an approved version until explicitly moved

This prevents surprise OS upgrades.

---

## Restart and Deadline Enforcement

| Behavior | Enforcement |
---|---|
| Restart notifications | Enabled |
| Snooze | Limited |
| Deadline expiry | Forced restart |
| User bypass | Not allowed |

Forced restarts are an **intentional control**.

---

## Interaction with Compliance and Access

| Control | Interaction |
---|---|
| Compliance policy | Evaluates OS version |
| Conditional Access | Blocks outdated devices |
| Remediation | Update enforcement |
| Reporting | Evidence generation |

Devices that fail to update become **non-compliant**.

---

## Failure Modes and Mitigation

| Issue | Cause | Mitigation |
---|---|---|
| Update failures | Driver issues | Use driver control policies |
| User disruption | Poor communication | Advance notice |
| Missed deadlines | Device offline | Remediation on reconnect |
| Ring contamination | Poor group design | Harden group logic |

---

## Validation Checklist

- [ ] Pilot ring receiving updates first
- [ ] Deferrals align with policy
- [ ] Deadlines enforced
- [ ] Forced restarts observed
- [ ] Compliance reflects update state

---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| Update ring configuration | Intune |
| Device update status | Intune reports |
| Deadline enforcement | Device timelines |
| Compliance state | Intune |

---

## Change Control

Update ring changes:
- Require Pilot validation
- Must be documented in the Decision Log
- Must not relax deadlines without approval
- Must include rollback strategy

---

## Summary

A disciplined update ring strategy ensures that:
- Security updates arrive on time
- Business impact is controlled
- Compliance is enforceable
- Audits are defensible

Updates are not optional.  
They are **part of the security baseline**.

---

## Next File

Proceed to:

**`docs/06-updates-and-servicing/18-feature-update-policy.md`**

This file defines **Windows 11 feature update pinning and release transitions**.
