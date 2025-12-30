# Device Reassignment Runbook  
**Secure Transfer of Devices Between Users Without Trust Inheritance**

---

## Purpose

This runbook defines the **authoritative procedure** for reassigning a Windows 11 device from one user to another in a Microsoft Intune–managed environment.

Device reassignment is a **trust reset operation**. It must:
- Remove all prior user data and access
- Preserve device enrollment and identity
- Reapply security and compliance baselines
- Prevent credential or data inheritance
- Produce complete audit evidence

Reassignment without a reset is **explicitly prohibited**.

---

## Approved Reassignment Scenarios

Device reassignment is **approved** for the following:

| Scenario | Approved |
---|---|
| Employee role change | Yes |
| Employee transfer | Yes |
| Device pool reuse | Yes |
| Contractor offboarding / onboarding | Yes |
| Break/fix replacement (same device) | Yes |

---

## Prohibited Scenarios

| Scenario | Action Instead |
---|---|
| Confirmed or suspected compromise | Full Wipe |
| Device decommissioning | Full Wipe + Deregistration |
| Legal hold | Security / Legal approval |
| Hardware trust failure | Full Wipe |
| Lost or stolen device | Full Wipe |

---

## Preconditions (MANDATORY)

Before beginning reassignment, confirm:

- [ ] Device is **present and online**
- [ ] Previous user access revoked
- [ ] No active security incident
- [ ] Business owner approval obtained
- [ ] Asset record identifies new assignee (if known)
- [ ] Autopilot profile remains assigned (if applicable)

If any precondition fails, **STOP**.

---

## Access Requirements

The operator must have:

| Requirement | Notes |
---|---|
| Intune role | Endpoint Administrator (or delegated equivalent) |
| Scope tag access | Device in scope |
| Service ticket | Required |
| Asset system access | For ownership update |

---

## Reassignment Method (Authoritative)

**Autopilot Reset is mandatory** for reassignment.

### Intune Portal Path

### Intune admin center
→ Devices
→ Windows
→ Select target device
→ Autopilot Reset


**Rule**  
Do **not** use Fresh Start or Full Wipe for reassignment unless directed by Security.

---

## Expected Technical Outcomes

| Component | Outcome |
---|---|
| Previous user profile | Removed |
| Local accounts | Removed |
| Device enrollment | Preserved |
| Azure AD / Entra ID join | Preserved |
| Compliance policies | Re-evaluated |
| Required applications | Reinstalled |
| Available applications | Remain optional |

---

## Post-Reset Assignment Workflow

After Autopilot Reset completes:

1. Verify device shows **Not assigned** (or no primary user)
2. Assign device to new user (if your process requires it)
3. Provide device to new user
4. User completes first sign-in
5. Monitor ESP completion and compliance

**Do not** assign the user before reset completion.

---

## Validation Checklist (MANDATORY)

Before closing the reassignment ticket:

- [ ] Autopilot Reset completed successfully
- [ ] No previous user profile exists
- [ ] Device reports **Compliant**
- [ ] Security baselines applied
- [ ] Required apps installed
- [ ] Conditional Access allows access
- [ ] New user can sign in successfully

If any check fails, **do not release the device**.

---

## Failure Scenarios and Actions

| Failure | Action |
---|---|
| Reset fails | Retry once, then escalate |
| ESP fails | Fix app/config issue, retry reset |
| Compliance not achieved | Investigate policy conflicts |
| Old user data present | Full Wipe immediately |
| Security alert post-reset | Initiate IR workflow |

Manual endpoint fixes are **not permitted**.

---

## Communication Protocol

| Audience | Timing |
---|---|
| Service Desk | During execution |
| Security | If anomalies occur |
| New user | When device is ready |
| Asset Management | Post-reassignment |

User messaging must be non-technical and action-focused.

---

## Evidence and Audit Artifacts

The following evidence **must be retained**:

| Artifact | Source |
---|---|
| Autopilot Reset action | Intune audit logs |
| Device timeline | Intune |
| Compliance post-reset | Intune |
| New user assignment | Intune / Asset system |
| Service ticket | Ticketing system |

Screenshots alone are **not sufficient**.

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Operations | Execution |
| Security | Oversight |
| Service Desk | User coordination |
| Asset Management | Ownership accuracy |
| GRC | Evidence retention |

---

## Change and Review

- This runbook must be reviewed annually
- Deviations require documented approval
- Repeat failures trigger process review

---

## Summary

Secure device reassignment requires **resetting trust, not transferring it**.

When executed correctly:
- No user data persists
- Security posture is restored
- Enrollment integrity is preserved
- Audits are satisfied

When executed incorrectly:
- Data leaks occur
- Compliance fails
- Incidents repeat

---

## Runbook Status

- ☐ Draft
- ☐ Approved
- ☐ Operational
- ☐ Reviewed (Annual)

---

