# Hardware Replacement Runbook  
**Secure Device Replacement Without Trust or Data Inheritance**

---

## Purpose

This runbook defines the **authoritative procedure** for replacing Windows 11 endpoint hardware in a Microsoft Intune–managed environment.

Hardware replacement is a **security-sensitive lifecycle event**.  
It must ensure that:
- The old device is fully decommissioned
- No data or trust transfers to the replacement device
- The new device is provisioned from a clean baseline
- Asset, security, and audit records remain accurate

Hardware replacement is **not** a simple swap.

---

## Approved Replacement Scenarios

Hardware replacement is approved for:

| Scenario | Approved |
---|---|
| Hardware failure | Yes |
| Performance degradation beyond remediation | Yes |
| Warranty replacement | Yes |
| Incident response (post-compromise) | Yes |
| Lifecycle refresh | Yes |

---

## Prohibited Scenarios

| Scenario | Action Instead |
---|---|
| Temporary loaner | Loaner workflow |
| User reassignment (same hardware) | Autopilot Reset |
| Device decommissioning without replacement | Decommissioning runbook |
| Legal hold | Security / Legal approval |

---

## Design Principles

1. **New hardware = new trust**
2. **No data migration without approval**
3. **Provision from zero-trust baseline**
4. **Old hardware is hostile until destroyed**
5. **Evidence is mandatory**

---

## Preconditions (MANDATORY)

Before beginning replacement:

- [ ] Replacement hardware received and inventoried
- [ ] Old device identified and confirmed
- [ ] Security approval obtained (if incident-related)
- [ ] User notified and downtime coordinated
- [ ] Asset records prepared for update
- [ ] Autopilot registration status known (new device)

If any precondition fails, **STOP**.

---

## Access Requirements

The operator must have:

| Requirement | Notes |
---|---|
| Intune role | Endpoint Administrator |
| Autopilot role | Windows Autopilot Administrator |
| Asset system access | Required |
| Service ticket | Required |

---

## Replacement Workflow (Authoritative)

### Phase 1 — Old Device Containment

Depending on scenario:

| Condition | Action |
---|---|
| Device operational | Autopilot Reset or Full Wipe |
| Suspected compromise | Device Isolation → Full Wipe |
| Hardware failure | Full Wipe if possible |
| Unrecoverable | Assume hostile |

**Rule**  
Old hardware must not remain active.

---

### Phase 2 — Old Device Decommissioning

Follow, in order:

1. Full Wipe (if possible)
2. Remove device from Intune
3. Remove device from Entra ID
4. Deregister from Autopilot
5. Update asset status (Retired / Replaced)

If wipe is not possible, proceed to **physical destruction**.

---

### Phase 3 — Replacement Device Preparation

#### Autopilot Registration

- Import hardware hash (if not OEM-registered)
- Assign standard Autopilot profile
- Verify device appears in Autopilot inventory

No device may be issued without Autopilot registration.

---

#### Provisioning Method

| Method | Approved |
---|---|
| Windows Autopilot (User-driven) | Yes |
| Pre-provisioning (White Glove) | Yes |
| Manual build | No |

---

### Phase 4 — User Provisioning

1. Assign replacement device to user (if required)
2. User completes Autopilot enrollment
3. ESP completes successfully
4. Device reports **Compliant**
5. Conditional Access allows access

---

## Data Migration Rules

| Data Type | Allowed |
---|---|
| OneDrive / cloud data | Yes |
| Application data | Reinstalled |
| Local files | No |
| Browser profiles | Via cloud sync only |
| Credentials | Never |

Manual file copy from old hardware is **prohibited**.

---

## Validation Checklist (MANDATORY)

Before closing replacement ticket:

- [ ] Old device wiped or destroyed
- [ ] Old device removed from Intune and Entra ID
- [ ] Old device deregistered from Autopilot
- [ ] Replacement device enrolled via Autopilot
- [ ] Replacement device compliant
- [ ] User access restored successfully
- [ ] Asset inventory updated

If any check fails, **do not close the ticket**.

---

## Failure Scenarios and Escalation

| Failure | Action |
---|---|
| Autopilot enrollment fails | Fix profile, retry |
| ESP failure | Fix blocking app/config |
| Compliance not achieved | Investigate policy |
| Old device resurfaces | Security escalation |
| Data loss claim | Escalate to management |

---

## Evidence and Audit Artifacts

The following evidence **must be retained**:

| Artifact | Source |
---|---|
| Old device wipe record | Intune audit logs |
| Autopilot deregistration | Intune audit logs |
| Replacement Autopilot enrollment | Intune |
| Compliance status | Intune |
| Asset replacement record | Asset system |
| Service ticket | Ticketing system |

Screenshots alone are **not sufficient**.

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Operations | Execution |
| Security | Oversight |
| Service Desk | User coordination |
| Asset Management | Inventory accuracy |
| GRC | Evidence retention |

---

## Change and Review

- This runbook must be reviewed annually
- Deviations require documented approval
- Incident-driven replacements require post-action review

---

## Summary

Hardware replacement is **trust termination plus trust re-establishment**.

When executed correctly:
- Old trust is destroyed
- New trust is clean
- Users resume work safely
- Audits are satisfied

When executed poorly:
- Data leaks occur
- Devices reappear unexpectedly
- Compliance fails
- Incidents repeat

---

## Runbook Status

- ☐ Draft
- ☐ Approved
- ☐ Operational
- ☐ Reviewed (Annual)

---

## Status Update

Hardware replacement runbook complete

All critical lifecycle runbooks now complete:

- Autopilot Reset

- Full Wipe

- Autopilot Deregistration

- Device Reassignment

- Incident Isolation

- Hardware Replacement
