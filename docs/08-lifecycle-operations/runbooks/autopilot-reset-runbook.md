# Autopilot Reset Runbook  
**Secure Device Reset While Preserving Enrollment Integrity**

---

## Purpose

This runbook defines the **authoritative procedure** for executing an **Autopilot Reset** on Windows 11 devices managed by Microsoft Intune.

Autopilot Reset is used to:
- Remove user data and profiles
- Restore the device to a known-good baseline
- Preserve Azure AD / Entra ID and Intune enrollment
- Reapply security, compliance, and application baselines automatically

This is a **security-sensitive operation** and must be executed exactly as defined.

---

## When to Use Autopilot Reset

Autopilot Reset is **approved** for the following scenarios:

| Scenario | Approved |
---|---|
| User departure / device reassignment | Yes |
| Persistent compliance drift | Yes |
| Application corruption | Yes |
| Performance degradation | Yes |
| Periodic device refresh | Yes |

---

## When NOT to Use Autopilot Reset

| Scenario | Action Instead |
---|---|
| Confirmed compromise | Full Wipe |
| Lost or stolen device | Full Wipe |
| Hardware trust failure (TPM/Secure Boot) | Full Wipe |
| Device decommissioning | Full Wipe |
| Legal hold or investigation | Security approval required |

Using Autopilot Reset in these cases **creates risk**.

---

## Preconditions (MANDATORY)

Before executing Autopilot Reset, confirm:

- [ ] Device is **managed by Intune**
- [ ] Device is **Windows 11**
- [ ] Device is **online**
- [ ] No active security incident on the device
- [ ] Business owner or manager approval obtained (if reassignment)
- [ ] User notified (if applicable)

If any precondition fails, **stop**.

---

## Access Requirements

The operator must have:

| Requirement | Notes |
---|---|
| Intune role | Endpoint Administrator (or delegated equivalent) |
| Scope tag access | Device in scope |
| Change record | If required by policy |

---

## Execution Method (Authoritative)

### Intune Portal Path

### Intune admin center
→ Devices
→ Windows
→ Select target device
→ Autopilot Reset


---

### Reset Confirmation

When prompted:

- Confirm Autopilot Reset (not Wipe)
- Acknowledge user data removal
- Proceed only once correct device is verified

**Rule**  
Always double-check the **device name and serial number** before confirming.

---

## Expected Technical Outcomes

| Component | Outcome |
---|---|
| User profiles | Removed |
| Local accounts | Removed |
| Device enrollment | Preserved |
| Azure AD join | Preserved |
| Compliance policies | Re-evaluated |
| Required apps | Reinstalled |
| Available apps | Remain optional |

---

## Post-Reset Monitoring

Immediately after triggering reset:

| Check | Expected Result |
---|---|
| Device status | Reset in progress |
| User assignment | Cleared |
| Access | Blocked until compliance |

---

## Post-Reset Validation Checklist

After the device completes reset and re-enrollment:

- [ ] Device successfully completes ESP
- [ ] No user logged in automatically
- [ ] Device shows **Compliant**
- [ ] Security baselines applied
- [ ] Required applications installed
- [ ] Conditional Access allows access post-login

If any check fails, **do not assign a user**.

---

## Common Failure Scenarios and Actions

| Failure | Action |
---|---|
| Reset fails to start | Verify connectivity, retry |
| Device stuck resetting | Allow up to 60 minutes, then Full Wipe |
| ESP failure | Fix app/config issue, retry reset |
| Compliance not restored | Investigate policy conflicts |
| User data persists | Full Wipe immediately |

Manual fixes on the endpoint are **prohibited**.

---

## Escalation Path

Escalate immediately if:

- Reset targets wrong device
- Device does not re-enroll
- Compliance cannot be restored
- Security alerts appear post-reset

| Escalation | Contact |
---|---|
| Endpoint Engineering | Tier 2 |
| Security Operations | If alerts present |
| Asset Management | If reassignment blocked |

---

## Evidence and Audit Artifacts

The following evidence **must be retained**:

| Artifact | Source |
---|---|
| Autopilot Reset action | Intune audit logs |
| Device timeline | Intune |
| Enrollment completion | Intune |
| Compliance post-reset | Intune |
| User reassignment record | Asset / ticket system |

Screenshots alone are **not sufficient**.

---

## Documentation Updates (Required)

After completion:

- Update service ticket
- Update asset ownership records
- Update Decision Log (if applicable)
- Close change record (if required)

---

## Security Notes

- Autopilot Reset **does not** destroy device identity
- BitLocker remains enabled and enforced
- Trust is restored only after compliance success
- Access remains blocked until all controls pass

---

## Summary

Autopilot Reset is the **preferred reset mechanism** for managed Windows 11 devices.

When executed correctly:
- User data is removed
- Security posture is restored
- Enrollment integrity is preserved
- Audit evidence is complete

When executed incorrectly:
- Trust leaks
- Data exposure risk increases
- Rework and incidents follow

---

## Runbook Status

- ☐ Draft
- ☐ Approved
- ☐ Operational
- ☐ Reviewed (Annual)

---

