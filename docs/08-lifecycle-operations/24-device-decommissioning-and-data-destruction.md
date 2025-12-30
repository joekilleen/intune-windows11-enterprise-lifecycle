# Device Decommissioning and Data Destruction  
**Secure Retirement, Cryptographic Erasure, and Asset Closure**

---

## Purpose

This document defines the **authoritative procedures** for decommissioning Windows 11 devices managed by Microsoft Intune.

Decommissioning is a **terminal lifecycle event**.  
It must ensure that:
- All organizational data is irreversibly destroyed
- Access is permanently revoked
- Device trust is not transferable
- Asset records are closed accurately
- Evidence is preserved for audit and legal review

Improper decommissioning creates **data breach and regulatory risk**.

---

## Design Principles

1. **Assume the device is hostile**
2. **Destroy data before trust**
3. **Cryptographic erasure is the default**
4. **Access is revoked first**
5. **Evidence is mandatory**
6. **No device re-enters production after decommissioning**

---

## Decommissioning Triggers (Authoritative)

A device **must** be decommissioned when any of the following occur:

| Trigger | Example |
---|---|
| End of hardware lifecycle | Warranty expiration |
| Device loss or theft | Unrecoverable asset |
| Confirmed compromise | Malware or credential exposure |
| Hardware trust failure | TPM / Secure Boot failure |
| Employee termination | Device not reassigned |
| Legal or regulatory directive | Litigation hold release |

---

## Pre-Decommissioning Controls

Before data destruction:

| Control | Action |
---|---|
| Access revocation | Immediate CA block |
| User offboarding | Completed |
| Incident closure | If applicable |
| Evidence capture | Required |

Devices must not retain **any active access** at this stage.

---

## Approved Decommissioning Methods

| Method | Use Case | Enrollment |
---|---|---|
| Full Wipe (Intune) | Primary | Removed |
| Cryptographic erase | Preferred | Removed |
| Physical destruction | Last resort | N/A |

Manual OS resets are **explicitly prohibited**.

---

## Primary Method — Intune Full Wipe

### Execution Path  
**Exact UI Click-Path**

### Intune admin center
→ Devices
→ Windows
→ Select device
→ Wipe

---


### Required Options

| Setting | Value |
---|---|
| Retain enrollment state | No |
| Retain user data | No |
| Wipe reason | Decommissioning |

---

### Wipe Outcomes

| Element | Result |
---|---|
| User data | Destroyed |
| BitLocker keys | Invalidated |
| Enrollment | Removed |
| Compliance | Terminated |
| Access | Revoked |

This constitutes **cryptographic erasure** when BitLocker is enabled.

---

## Cryptographic Erasure Validation

Cryptographic erasure is considered successful when:

- BitLocker was enabled prior to wipe
- Device reports wipe completion
- Recovery keys are destroyed or inaccessible
- Device no longer reports to Intune

If BitLocker status is unknown, **physical destruction is required**.

---

## Physical Destruction (Escalation)

Physical destruction is required when:

- Device cannot be wiped remotely
- Device is unrecoverable
- Regulatory requirements mandate destruction
- Hardware trust cannot be validated

### Approved Methods

- Certified shredding
- Certified degaussing (where applicable)
- Vendor-certified destruction

Certificates of destruction **must be retained**.

---

## Post-Decommissioning Actions

| Action | Requirement |
---|---|
| Remove from Intune | Mandatory |
| Remove from Entra ID | Mandatory |
| Remove Autopilot record | Mandatory |
| Update asset inventory | Mandatory |
| Close user-device association | Mandatory |

Devices must not exist in a **zombie state**.

---

## Autopilot Record Handling

### Rule

Decommissioned devices **must not** retain Autopilot registration unless explicitly approved for resale or reuse.

### Execution Path

### Intune admin center
→ Devices
→ Windows
→ Windows enrollment
→ Devices
→ Delete Autopilot device


---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| Wipe action record | Intune audit logs |
| Wipe completion status | Intune device timeline |
| BitLocker key destruction | Key management logs |
| Autopilot record deletion | Intune |
| Asset retirement record | Asset system |
| Destruction certificate (if applicable) | Vendor |

---

## Evidence Retention Requirements

| Evidence | Minimum Retention |
---|---|
| Decommissioning logs | 1 year |
| Asset retirement records | 7 years (or per policy) |
| Destruction certificates | 7 years (or per policy) |

Retention must align with **legal and regulatory obligations**.

---

## Failure Modes and Mitigation

| Failure | Risk | Mitigation |
---|---|---|
| Wipe fails | Data exposure | Physical destruction |
| Device resurfaces | Unauthorized access | Verify removal |
| Autopilot record remains | Re-enrollment risk | Delete record |
| Evidence missing | Audit failure | Halt process until resolved |

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Operations | Execution |
| Security | Oversight |
| Asset Management | Inventory closure |
| Legal / GRC | Retention and compliance |

---

## Change Control

Decommissioning procedures:
- Must not be bypassed
- Must be logged and approved
- Must retain evidence
- Must be reviewed annually

---

## Summary

Decommissioning is **data destruction plus trust termination**.

When executed correctly:
- Data is irrecoverable
- Access is permanently revoked
- Assets are closed cleanly
- Audits are satisfied

When executed poorly:
- Breach risk persists
- Compliance fails
- Legal exposure increases

---

## Section Completion

With this document, **Section 8 — Device Lifecycle Operations** is **complete and defensible**.

---

## Next Section

Proceed to:

**`docs/08-lifecycle-operations/runbooks/autopilot-reset-runbook.md**


