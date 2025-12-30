# Device Wipe Runbook  
**Irreversible Data Destruction and Trust Termination**

---

## Purpose

This runbook defines the **authoritative procedure** for executing a **Full Device Wipe** on Windows 11 devices managed by Microsoft Intune.

A device wipe is a **terminal security action** intended to:
- Irreversibly destroy organizational data
- Revoke all access and trust
- Remove the device from Intune and Entra ID
- Prevent any future use without explicit re-enrollment

This action is **destructive and irreversible**.

---

## When to Use Device Wipe (Mandatory)

A **Full Wipe** must be executed in the following scenarios:

| Scenario | Required |
---|---|
| Confirmed device compromise | Yes |
| Lost or stolen device | Yes |
| Employee termination (no reassignment) | Yes |
| Device decommissioning | Yes |
| Hardware trust failure (TPM/Secure Boot) | Yes |
| Legal or regulatory directive | Yes |

Failure to wipe in these scenarios creates **material risk**.

---

## When NOT to Use Device Wipe

| Scenario | Action Instead |
---|---|
| User reassignment | Autopilot Reset |
| Periodic refresh | Autopilot Reset |
| Application corruption | Autopilot Reset |
| Performance issues | Autopilot Reset |

Using a wipe when not required increases operational cost and risk.

---

## Preconditions (MANDATORY)

Before initiating a wipe, confirm:

- [ ] Device is correctly identified (name, serial, user)
- [ ] Security approval obtained (for incidents)
- [ ] HR approval obtained (for terminations)
- [ ] No legal hold prevents destruction
- [ ] Evidence capture completed (if incident-related)
- [ ] User access already revoked via Conditional Access

If any precondition fails, **STOP**.

---

## Access Requirements

The operator must have:

| Requirement | Notes |
---|---|
| Intune role | Endpoint Administrator (or equivalent) |
| Scope tag access | Device in scope |
| Incident or change record | Required |

---

## Execution Method (Authoritative)

### Intune Portal Path

### Intune admin center
→ Devices
→ Windows
→ Select target device
→ Wipe


---

### Wipe Options (MANDATORY)

When prompted, set:

| Option | Value |
---|---|
| Retain enrollment state | No |
| Retain user data | No |
| Wipe reason | Security / Decommissioning / HR |

Any deviation requires security approval.

---

## Expected Technical Outcomes

| Component | Outcome |
---|---|
| User data | Irreversibly destroyed |
| BitLocker keys | Invalidated |
| Device enrollment | Removed |
| Azure AD / Entra ID trust | Removed |
| Compliance state | Terminated |
| Conditional Access | Permanently blocked |

This constitutes **cryptographic erasure** when BitLocker was enabled.

---

## Post-Wipe Monitoring

Immediately after initiating wipe:

| Check | Expected Result |
---|---|
| Device status | Wipe pending / completed |
| User access | Blocked |
| Device check-in | Ceases |

If the device does not report completion, assume **hostile**.

---

## Post-Wipe Validation Checklist

Within operational SLA:

- [ ] Wipe action recorded in Intune audit logs
- [ ] Device no longer appears in active device list
- [ ] Device removed from Entra ID
- [ ] Autopilot record reviewed and removed (if decommissioned)
- [ ] Asset inventory updated
- [ ] Incident or HR record closed

---

## Failure Scenarios and Escalation

| Failure | Action |
---|---|
| Device offline | Treat as hostile, escalate |
| Wipe fails | Attempt once, then physical destruction |
| Device resurfaces | Immediate security escalation |
| Evidence missing | Halt closure until resolved |

---

## Autopilot Record Handling

### Rule

A wiped device **must not** remain registered in Autopilot unless explicitly approved for reuse.

### Removal Path

### Intune admin center
→ Devices
→ Windows
→ Windows enrollment
→ Devices
→ Delete Autopilot device


---

## Evidence and Audit Artifacts

The following evidence **must be retained**:

| Artifact | Source |
---|---|
| Wipe initiation record | Intune audit logs |
| Wipe completion status | Intune device timeline |
| BitLocker key invalidation | Key management logs |
| Autopilot record deletion | Intune |
| Asset retirement record | Asset system |
| Destruction certificate (if applicable) | Vendor |

Retention must align with legal and regulatory requirements.

---

## Communication Protocol

| Audience | Timing |
---|---|
| Security Operations | Immediate (incidents) |
| HR | Before and after (terminations) |
| Asset Management | Post-wipe |
| User | Only if appropriate |

User communication must be factual and minimal.

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Operations | Execution |
| Security | Authorization and oversight |
| HR / Legal | Approval (as applicable) |
| Asset Management | Inventory closure |
| GRC | Evidence retention |

---

## Change and Review

- This runbook must be reviewed annually
- Deviations require documented approval
- Incidents must trigger post-action review

---

## Summary

A device wipe is **trust termination plus data destruction**.

When executed correctly:
- Data is unrecoverable
- Access is permanently revoked
- Compliance obligations are met
- Audit evidence is complete

When executed poorly:
- Breach risk persists
- Legal exposure increases
- Trust is compromised

---

## Runbook Status

- ☐ Draft
- ☐ Approved
- ☐ Operational
- ☐ Reviewed (Annual)

---

