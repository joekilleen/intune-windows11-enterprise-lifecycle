# Disaster Recovery and Configuration Backup  
**Control-Plane Resilience, Export Discipline, and Rebuild Readiness**

---

## Purpose

This document defines the **authoritative disaster recovery (DR) and configuration backup strategy** for Windows 11 endpoint management using Microsoft Intune and Microsoft Entra ID.

The objectives are to:
- Preserve recoverability of the endpoint control plane
- Enable deterministic rebuild of configurations
- Reduce recovery time after control-plane incidents
- Provide audit-defensible evidence of preparedness

DR for endpoint management is about **configuration recovery**, not device imaging.

---

## Design Objectives

The DR strategy must ensure:

1. **Complete configuration coverage**
2. **Regular, validated exports**
3. **Secure, immutable storage**
4. **Offline availability**
5. **Documented rebuild procedures**
6. **No reliance on tribal knowledge**

---

## DR Scope (Authoritative)

The following **must** be recoverable:

| Domain | Examples |
---|---|
| Enrollment | Autopilot profiles, ESP |
| Configuration | Baselines, settings catalogs |
| Compliance | Compliance policies |
| Security | Defender, ASR, BitLocker |
| Updates | Update rings, feature policies |
| Applications | Win32 apps, assignments |
| Access | Conditional Access dependencies |
| Governance | RBAC, scope tags |
| Operations | Proactive remediations |

Devices themselves are **re-enrolled**, not restored.

---

## Backup Strategy Overview

### What We Back Up

| Item | Method |
---|---|
| Intune policies | Export |
| App metadata | Export |
| Assignments | Export |
| Entra ID configs | Export |
| RBAC and scope tags | Export |
| Decision records | Repository |

### What We Do NOT Back Up

- Device local state
- User data (covered by OneDrive)
- Cached tokens
- Temporary logs beyond retention

---

## Export Cadence (Mandatory)

| Artifact | Frequency |
---|---|
| Intune configuration exports | Monthly |
| App and assignment inventory | Monthly |
| RBAC and scope tags | Quarterly |
| Autopilot device inventory | Monthly |
| Conditional Access policies | Monthly |
| Break-glass configuration | Quarterly |
| Full DR package | Quarterly |

Any major change triggers an **out-of-cycle export**.

---

## Export Methods (Approved)

### Intune

- Native export (JSON / CSV where available)
- Graph-based scripted export (approved scripts only)
- Screenshot exports are **supplemental only**

---

### Entra ID

- Native policy export
- Audit logs for change reconstruction
- PIM configuration export

---

## Storage and Retention

### Storage Requirements

Exports must be stored in:

- Encrypted repository
- Access-controlled location
- Separate from production tenant
- With version history enabled

Examples:
- Private Git repository
- Secure document vault
- GRC evidence repository

---

### Retention Requirements

| Artifact | Minimum Retention |
---|---|
| Monthly exports | 12 months |
| Quarterly DR packages | 24 months |
| Incident-related exports | Case lifetime + 1 year |

---

## DR Package Structure (Standard)

Each quarterly DR package **must** include:

DR-Package-YYYY-Q#
│
├─ intune/
│ ├─ configuration-profiles/
│ ├─ compliance-policies/
│ ├─ update-policies/
│ ├─ security-baselines/
│ ├─ apps/
│ └─ assignments/
│
├─ entra-id/
│ ├─ conditional-access/
│ ├─ roles-and-pim/
│ └─ audit-exports/
│
├─ autopilot/
│ ├─ profiles/
│ └─ device-inventory/
│
├─ governance/
│ ├─ rbac-matrix.md
│ ├─ scope-tags.md
│ └─ access-reviews/
│
└─ README.md


---

## Recovery Scenarios

### Scenario 1 — Accidental Policy Deletion

**Response**
1. Identify last known-good export
2. Recreate policy from export
3. Reassign scopes and tags
4. Validate compliance and access
5. Document incident

---

### Scenario 2 — Tenant Compromise (Control Plane)

**Response**
1. Contain incident (security-led)
2. Revoke privileged access
3. Stand up clean tenant (if required)
4. Recreate configuration from DR package
5. Re-enroll devices via Autopilot
6. Validate compliance and access
7. Retire compromised tenant

---

### Scenario 3 — Service Outage or Corruption

**Response**
1. Validate scope of impact
2. Pause changes
3. Use exports for reference
4. Restore configurations as services return
5. Perform post-incident review

---

## Rebuild Order (Authoritative)

When rebuilding from scratch, apply in this order:

1. Identity baseline (Entra ID)
2. RBAC and scope tags
3. Enrollment profiles (Autopilot / ESP)
4. Security baselines
5. Compliance policies
6. Update policies
7. Applications (required first)
8. Conditional Access dependencies
9. Monitoring and remediations

Skipping order creates **hidden failures**.

---

## Validation After Recovery

After any recovery action:

- [ ] Devices can enroll
- [ ] ESP completes
- [ ] Compliance evaluates correctly
- [ ] Conditional Access enforces
- [ ] Security signals report
- [ ] Updates function normally
- [ ] Apps install as expected

Recovery is incomplete until **validation passes**.

---

## Evidence and Audit Artifacts

| Artifact | Source |
---|---|
| Export logs | Export tooling |
| DR packages | Secure storage |
| Recovery steps | Incident records |
| Validation results | Intune / Entra ID |
| Post-incident review | Change system |

Auditors expect **proof of exports and tests**, not intent.

---

## Testing and Exercises

### DR Testing Requirements

- Tabletop exercise: Semi-annual
- Partial restore test: Annual
- Full rebuild simulation: Every 2 years or after major change

Test results must be documented.

---

## Common Failure Modes (Avoid)

| Failure | Impact |
---|---|
| No exports | Irrecoverable state |
| Incomplete exports | Rebuild gaps |
| Untested backups | False confidence |
| Shared storage | Compromise risk |
| No rebuild order | Extended outage |

---

## Change Control

DR strategy changes:
- Require security and GRC approval
- Must not reduce coverage or frequency
- Must be documented in the Decision Log
- Must include updated test plan

---

## Summary

Disaster recovery for endpoint management is **control-plane recovery**, not device recovery.

When implemented correctly:
- Configuration can be rebuilt deterministically
- Incidents are survivable
- Audit posture is strong
- Confidence is justified

When neglected:
- Recovery becomes guesswork
- Outages extend
- Trust erodes

---

## Next File

Proceed to:

**`docs/10-nonprod-dr-expansion/29-tenant-expansion-and-migration-patterns.md`**

This file defines **M&A, carve-out, and tenant growth patterns with controlled risk**.
