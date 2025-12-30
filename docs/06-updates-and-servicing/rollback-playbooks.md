# Rollback Playbooks  
**Controlled Recovery from Update, Driver, and Platform Failures**

---

## Purpose

This document defines the **authoritative rollback playbooks** for Windows 11 devices managed by Microsoft Intune.

Rollback playbooks exist to ensure that when servicing changes cause instability, the organization can:
- Restore service rapidly
- Contain blast radius
- Preserve security posture
- Produce audit-ready evidence
- Avoid improvisation during incidents

Rollback is a **planned operation**, not an emergency reaction.

---

## Design Principles

All rollback actions must be:

1. **Pre-approved**
2. **Repeatable**
3. **Automated where possible**
4. **Fail-safe**
5. **Auditable**
6. **Time-bound**

Manual, undocumented fixes are **explicitly prohibited**.

---

## Rollback Scope Matrix

| Change Type | Rollback Required | Playbook |
---|---|---|
| Quality update | Yes | RB-01 |
| Feature update | Yes | RB-02 |
| Driver update | Yes | RB-03 |
| Firmware update | Yes | RB-04 |
| Application update | Yes | RB-05 |

---

## RB-01 — Quality Update Rollback

### Trigger Conditions

- Widespread BSODs
- Login failures
- Critical application outage
- Performance regression confirmed

---

### Rollback Method

**Primary**
- Allow Windows Update automatic rollback (if within window)

**Secondary**
- Pause quality updates
- Extend update deadline
- Force remediation on affected devices

---

### Execution Steps

1. Identify affected ring (Pilot / Broad / Enterprise)
2. Pause quality updates in impacted ring
3. Validate rollback success on sample devices
4. Resume updates only after root cause resolved
5. Document incident

---

### Evidence Required

| Artifact | Source |
---|---|
| Update pause record | Intune |
| Device update status | Intune |
| Rollback confirmation | Device timeline |
| Incident record | Change system |

---

## RB-02 — Feature Update Rollback

### Trigger Conditions

- LOB application incompatibility
- OS stability regression
- Security control failure
- Vendor advisory

---

### Rollback Method

| Method | Use Case |
---|---|
| Windows rollback window | Immediate (<10 days) |
| OS version re-pin | Controlled downgrade |
| Device reset | Persistent failure |

---

### Execution Steps

1. Stop feature update promotion
2. Remove assignment of new feature update policy
3. Reassign previous approved version
4. Validate OS version compliance
5. Escalate resets if rollback window expired

---

### Evidence Required

| Artifact | Source |
---|---|
| Feature update policy changes | Intune |
| OS version inventory | Intune |
| Rollback success metrics | Intune |
| Change approval | Change system |

---

## RB-03 — Driver Rollback

### Trigger Conditions

- Hardware-specific failures
- Peripheral non-functionality
- Increased crash rates
- Security agent malfunction

---

### Rollback Method

| Method | Preference |
---|---|
| OS driver rollback | Preferred |
| OEM rollback utility | Preferred for firmware |
| Device reset | Last resort |

---

### Execution Steps

1. Identify impacted hardware models
2. Remove driver approval or package
3. Execute rollback via OS or OEM tool
4. Validate stability
5. Block re-deployment of faulty driver

---

### Evidence Required

| Artifact | Source |
---|---|
| Driver deployment record | Intune |
| Rollback execution logs | Device |
| Stability metrics | Endpoint Analytics |
| Change record | Change system |

---

## RB-04 — Firmware Rollback

### Trigger Conditions

- Boot failures
- TPM / Secure Boot breakage
- BIOS instability
- Vendor recall

---

### Rollback Method

| Method | Notes |
---|---|
| OEM firmware rollback | Primary |
| Hardware replacement | If rollback impossible |

---

### Execution Steps

1. Halt firmware deployment immediately
2. Engage OEM support
3. Execute rollback on pilot hardware
4. Expand rollback if successful
5. Replace hardware if rollback fails

---

### Evidence Required

| Artifact | Source |
---|---|
| Firmware deployment logs | OEM tooling |
| Rollback confirmation | OEM tooling |
| Device compliance state | Intune |
| Incident documentation | Change system |

---

## RB-05 — Application Supersedence Rollback

### Trigger Conditions

- App crashes
- Performance degradation
- Security regression
- User productivity impact

---

### Rollback Method

- Remove assignments from new version
- Reassign previous version
- Allow Intune supersedence to execute rollback

---

### Execution Steps

1. Remove production assignment from new app
2. Reassign previous app version
3. Monitor uninstall/install success
4. Validate detection of old version
5. Document incident and resolution

---

### Evidence Required

| Artifact | Source |
---|---|
| App assignment changes | Intune |
| Install/uninstall reports | Intune |
| Supersedence chain | Intune |
| Incident record | Change system |

---

## Communication Protocol (All Rollbacks)

| Audience | Communication |
---|---|
| IT Operations | Immediate |
| Service Desk | Before user impact |
| Business stakeholders | If impact > 2 hours |
| Security | If control affected |

User messaging must be **clear, factual, and non-speculative**.

---

## Post-Rollback Review (Mandatory)

Within 5 business days:

- Root cause analysis completed
- Preventive controls updated
- Documentation revised
- Decision Log updated
- Lessons learned recorded

---

## Common Failure Patterns (Avoid)

| Failure | Prevention |
---|---|
| No rollback plan | Mandatory playbooks |
| Manual fixes | Automation only |
| Ring bypass | Enforce progression |
| Evidence gaps | Artifact checklist |
| Reoccurrence | Root cause correction |

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Endpoint Engineering | Execution |
| Security | Risk validation |
| Change Management | Approval and tracking |
| Management | Risk acceptance |

---

## Summary

Rollback playbooks convert **incidents into controlled events**.

They ensure that:
- Recovery is fast
- Risk is contained
- Security is preserved
- Audits are satisfied
- Trust in the platform is maintained

No servicing change is approved **without a rollback plan**.

---

## Section Completion

With this document, **Section 6 — Updates & Servicing** is **operationally complete**.

---

## Next Section

Proceed to:

**`docs/07-monitoring-and-operations/21-endpoint-analytics-and-health.md`**

This section defines **continuous visibility, health signals, and operational readiness**.
