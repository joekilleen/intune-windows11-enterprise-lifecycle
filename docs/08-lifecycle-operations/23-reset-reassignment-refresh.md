# Device Reset, Reassignment, and Refresh  
**Controlled Transitions Without Trust Leakage**

---

## Purpose

This document defines the **authoritative operational procedures** for resetting, reassigning, and refreshing Windows 11 devices managed by Microsoft Intune.

These lifecycle actions are **security-sensitive events**.  
Improper execution can result in:
- Data leakage
- Residual access
- Broken compliance signals
- Audit failure

All reset and reassignment actions must be **intentional, logged, and verifiable**.

---

## Lifecycle Definitions (Authoritative)

| Term | Definition |
---|---|
| Reset | Rebuild OS while retaining enrollment (Autopilot Reset) |
| Reassignment | Transfer device to a new user |
| Refresh | Periodic rebuild to restore baseline |
| Wipe | Full data destruction and de-enrollment |

Each action has **distinct security implications**.

---

## Design Principles

1. **Trust is not inherited**
2. **Rebuild over repair**
3. **Enrollment integrity preserved**
4. **Evidence retained**
5. **Automation preferred**
6. **Fail closed**

---

## Supported Reset Methods

| Method | Use Case | Enrollment |
---|---|---|
| Autopilot Reset | User change, drift correction | Preserved |
| Fresh Start | OS cleanup | Re-enroll |
| Full Wipe | Compromise, decommission | Removed |

Manual local resets are **prohibited**.

---

## Autopilot Reset (Primary Method)

### When to Use

- User departure or role change
- Persistent compliance drift
- Application corruption
- Performance degradation

Autopilot Reset is **preferred** because it:
- Preserves device identity
- Retains Intune enrollment
- Reapplies baseline automatically

---

### Execution Path  
**Exact UI Click-Path**

### Intune admin center
→ Devices
→ Windows
→ Select device
→ Autopilot Reset


---

### Autopilot Reset Outcomes

| Element | Result |
---|---|
| User data | Removed |
| Local accounts | Removed |
| Device enrollment | Preserved |
| Compliance | Re-evaluated |
| Apps | Reinstalled per policy |

---

## Device Reassignment Workflow

### Preconditions

- Previous user offboarded
- Device reset completed
- Compliance verified
- No open incidents

---

### Reassignment Steps

1. Perform Autopilot Reset
2. Verify device shows **Not assigned**
3. Assign device to new user (if required)
4. Monitor enrollment and ESP
5. Validate compliance and access

Users must **never** inherit a live session or profile.

---

## Periodic Device Refresh

### Purpose

Periodic refresh:
- Eliminates long-term drift
- Restores performance
- Resets configuration entropy

---

### Refresh Policy

| Attribute | Standard |
---|---|
| Refresh interval | 12–24 months |
| Method | Autopilot Reset |
| User notification | Required |
| Scheduling | Off-hours |

---

## Full Wipe (Escalation)

### When Required

- Confirmed compromise
- Device lost or stolen
- Hardware trust failure
- Decommissioning
- Legal or HR directive

---

### Execution Path  
**Exact UI Click-Path**

### Intune admin center
→ Devices
→ Windows
→ Select device
→ Wipe


**Optional**
- Retain enrollment state: No
- Retain user data: No

---

## Compliance and Access Enforcement

| State | Access |
---|---|
| Reset in progress | Blocked |
| Post-reset non-compliant | Blocked |
| Fully compliant | Allowed |

Access is restored **only after compliance success**.

---

## Failure Modes and Mitigation

| Failure | Cause | Mitigation |
---|---|---|
| Reset fails | Network or hardware | Retry or wipe |
| ESP failure | App misconfiguration | Fix app, retry |
| User data persists | Incorrect method | Full wipe |
| Compliance not restored | Policy issue | Remediate |

Manual intervention on endpoints is **not permitted**.

---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| Reset or wipe action | Intune audit logs |
| Device timeline | Intune |
| Enrollment status | Intune |
| Compliance post-reset | Intune |
| User reassignment record | Asset system |

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Operations | Execution |
| Security | Oversight |
| Service Desk | User coordination |
| Asset Management | Inventory accuracy |

---

## Change Control

Reset and reassignment actions:
- Must be logged
- Must follow approved methods
- Must retain evidence
- Must not bypass compliance

---

## Summary

Device reset and reassignment are **trust-reset operations**.

When executed correctly:
- Data is removed
- Configuration is restored
- Compliance is enforced
- Risk is contained

When executed poorly:
- Trust leaks
- Audits fail
- Incidents repeat

---

## Next File

Proceed to:

**`docs/08-device-lifecycle-operations/24-device-decommissioning-and-data-destruction.md`**

This file defines **secure device retirement, cryptographic wipe, and asset closure**.
