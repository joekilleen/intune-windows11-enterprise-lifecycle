# Autopilot Deregistration Runbook  
**Permanent Removal of Device Identity from Windows Autopilot**

---

## Purpose

This runbook defines the **authoritative procedure** for deregistering a Windows device from **Windows Autopilot**.

Autopilot deregistration is a **trust-termination action** that:
- Permanently removes the device from Autopilot
- Prevents automatic re-enrollment
- Breaks device identity inheritance
- Completes the device decommissioning lifecycle

Once deregistered, a device **cannot be reintroduced** without explicit re-registration.

---

## When to Perform Autopilot Deregistration (Mandatory)

Autopilot deregistration **must** occur in the following scenarios:

| Scenario | Required |
---|---|
| Device decommissioning | Yes |
| Device resale or disposal | Yes |
| Device loss or theft | Yes |
| Hardware replacement | Yes |
| Legal or regulatory directive | Yes |
| Device leaving organizational control permanently | Yes |

Failure to deregister creates **re-enrollment and data exposure risk**.

---

## When NOT to Deregister

| Scenario | Action Instead |
---|---|
| User reassignment | Autopilot Reset |
| Periodic refresh | Autopilot Reset |
| Temporary loaner device | No action |
| Incident under investigation | Security approval required |

Deregistration is **irreversible** and must not be used casually.

---

## Preconditions (MANDATORY)

Before deregistering a device, confirm:

- [ ] Device has been **wiped** or is confirmed unrecoverable
- [ ] Device is **no longer required** by the organization
- [ ] HR / Asset Management approval obtained (if applicable)
- [ ] No legal hold applies
- [ ] Evidence capture completed (wipe, asset retirement)
- [ ] Device identity verified (serial number)

If any precondition fails, **STOP**.

---

## Access Requirements

The operator must have:

| Requirement | Notes |
---|---|
| Intune role | Windows Autopilot Administrator or equivalent |
| Scope tag access | Device in scope |
| Change / asset record | Required |

---

## Execution Method (Authoritative)

### Intune Portal Path

### Intune admin center
→ Devices
→ Windows
→ Windows enrollment
→ Devices


---

## Deregistration Procedure

1. Locate the device using:
   - Serial number (preferred)
   - Windows Autopilot device ID
2. Verify device identity matches asset records
3. Select the device
4. Choose **Delete**
5. Confirm permanent deletion

**Rule**  
Always validate the **serial number** before deletion.

---

## Expected Outcomes

| Component | Outcome |
---|---|
| Autopilot registration | Permanently removed |
| Zero-touch enrollment | Disabled |
| Device re-enrollment | Impossible without re-import |
| Tenant association | Removed |

This action **cannot be undone**.

---

## Post-Deregistration Validation Checklist

- [ ] Device no longer appears in Autopilot device list
- [ ] Device cannot be automatically enrolled
- [ ] Asset inventory reflects retirement
- [ ] Related Intune device record removed or archived
- [ ] Evidence retained

If the device remains visible, **do not proceed with disposal**.

---

## Failure Scenarios and Escalation

| Failure | Action |
---|---|
| Device not found | Verify serial / tenant |
| Wrong device identified | STOP and escalate |
| Deletion fails | Retry once, then escalate |
| Device reappears | Security escalation |

---

## Evidence and Audit Artifacts

The following evidence **must be retained**:

| Artifact | Source |
---|---|
| Autopilot deletion action | Intune audit logs |
| Preceding wipe record | Intune audit logs |
| Asset retirement approval | Asset system |
| Disposal or transfer record | Asset / vendor |
| Change record | Change system |

Screenshots alone are **not sufficient**.

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Operations | Execution |
| Asset Management | Authorization |
| Security | Oversight |
| GRC | Evidence retention |

---

## Common Failure Patterns (Avoid)

| Failure | Risk |
---|---|
| Skipping deregistration | Re-enrollment risk |
| Deleting wrong device | Service disruption |
| No evidence retained | Audit failure |
| Deregistering before wipe | Data exposure |

---

## Summary

Autopilot deregistration is the **final trust severance** for a Windows device.

When executed correctly:
- Re-enrollment is impossible
- Data exposure risk is eliminated
- Asset records are clean
- Audits are satisfied

When executed incorrectly:
- Devices can reappear unexpectedly
- Trust boundaries fail
- Legal and security risk increases

---

## Runbook Status

- ☐ Draft
- ☐ Approved
- ☐ Operational
- ☐ Reviewed (Annual)

---

