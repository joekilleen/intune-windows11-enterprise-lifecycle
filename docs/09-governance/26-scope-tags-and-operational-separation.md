# Scope Tags and Operational Separation  
**Enforcing Administrative Boundaries at Scale**

---

## Purpose

This document defines the **authoritative scope tag strategy** for Microsoft Intune to enforce **operational separation, least privilege, and blast-radius reduction**.

Scope tags are not cosmetic.  
They are a **hard control** that determines what administrators can see, modify, and deploy.

---

## Design Objectives

The scope tag model must ensure:

1. **Clear administrative boundaries**
2. **Predictable delegation**
3. **Reduced blast radius**
4. **Audit-ready separation of duties**
5. **Scalability without role sprawl**

---

## Governance Principles

- Every managed object **must** have a scope tag
- Scope tags align to **operational responsibility**, not org charts
- Tags are **mutually exclusive where possible**
- No “catch-all” or “global” operational tags
- Scope tags are enforced **in addition to RBAC**, not instead of it

---

## Objects in Scope

Scope tags **must** be applied consistently to:

| Object Type |
---|---|
| Devices |
| Applications |
| Configuration profiles |
| Compliance policies |
| Update rings |
| Feature update policies |
| Proactive remediations |

Untagged objects are considered **non-compliant**.

---

## Scope Tag Taxonomy (Authoritative)

### 1. Environment-Based Tags (Mandatory)

| Tag | Description |
---|---|
| ENV-PROD | Production devices |
| ENV-NONPROD | Pilot / test devices |

Environment separation is **non-negotiable**.

---

### 2. Operational Domain Tags

| Tag | Description |
---|---|
| OPS-ENDPOINT | Endpoint engineering |
| OPS-SECURITY | Security-owned objects |
| OPS-SERVICEDESK | Service desk operations |

---

### 3. Device Class Tags

| Tag | Description |
---|---|
| DEV-WORKSTATION | Standard user devices |
| DEV-KIOSK | Kiosk / shared devices |
| DEV-PRIV | Privileged access devices |

---

### 4. Regulatory / Sensitivity Tags (Optional)

| Tag | Use Case |
---|---|
| REG-FINANCE | Financial systems |
| REG-HIPAA | Healthcare workloads |
| REG-GDPR | EU data protection |

Use only when **legally required**.

---

## Tag Combination Rules

### Approved Combinations

| Example | Meaning |
---|---|
| ENV-PROD + OPS-ENDPOINT | Production endpoint control |
| ENV-NONPROD + OPS-SECURITY | Security testing |
| ENV-PROD + DEV-PRIV | Privileged devices |

---

### Prohibited Combinations

| Combination | Reason |
---|---|
| ENV-PROD + ENV-NONPROD | Boundary violation |
| OPS-ENDPOINT + OPS-SECURITY | Separation of duties |
| DEV-PRIV + OPS-SERVICEDESK | Excessive access |

Violations require **explicit risk acceptance**.

---

## Assignment Strategy

### Devices

- Tagged at enrollment via Autopilot
- Inherited through group assignment
- Validated during compliance evaluation

---

### Applications

- Tagged at creation
- Never modified post-production without approval
- Superseding apps inherit same tags

---

### Policies and Profiles

- Created with correct scope tags
- Never retagged to expand reach
- Retiring policies retain tags until deletion

---

## Role-to-Tag Mapping

| Role | Allowed Tags |
---|---|
| Endpoint Administrator | ENV-PROD, ENV-NONPROD, OPS-ENDPOINT |
| Security Operator | OPS-SECURITY |
| Help Desk Operator | OPS-SERVICEDESK |
| Read Only Operator | All (read-only) |

Access outside assigned tags is **not visible**.

---

## Operational Separation Use Cases

### Service Desk Isolation

Service desk operators:
- Can reset devices
- Can reassign users
- Cannot deploy apps
- Cannot modify policies
- Cannot access privileged devices

---

### Security Isolation

Security operators:
- Control Defender settings
- Review compliance signals
- Isolate devices
- Cannot deploy apps
- Cannot modify enrollment profiles

---

### Non-Production Safety

Non-production admins:
- Can test freely
- Cannot touch production
- Cannot bypass pilot validation
- Cannot promote changes directly

---

## Validation and Enforcement

### Quarterly Validation Checklist

- [ ] All objects tagged
- [ ] No cross-environment access
- [ ] No prohibited tag combinations
- [ ] Role-to-tag alignment validated
- [ ] Exceptions documented

---

## Failure Modes and Mitigation

| Failure | Impact | Mitigation |
---|---|---|
| Untagged objects | Uncontrolled access | Block deployment |
| Overlapping tags | Excessive privilege | Re-tag + review |
| Tag sprawl | Complexity | Consolidate |
| Manual exceptions | Drift | Time-bound approvals |

---

## Audit Evidence

The following evidence must be retained:

| Artifact | Source |
---|---|
| Scope tag definitions | Intune |
| Tag assignments | Intune |
| Role-to-tag mappings | Access reviews |
| Exception approvals | Change system |

---

## Change Control

Scope tag changes:
- Require security approval
- Must not expand access silently
- Must be documented in Decision Log
- Must include rollback

---

## Summary

Scope tags are the **enforcement layer** of delegated administration.

When implemented correctly:
- Admins only see what they own
- Mistakes are contained
- Security boundaries are real
- Audits are straightforward

When implemented poorly:
- RBAC collapses
- Blast radius explodes
- Trust erodes

---

## Next File

Proceed to:

**`docs/09-governance-and-rbac/27-access-reviews-and-audit-readiness.md`**

This file defines **access recertification, review cadence, and audit alignment**.
