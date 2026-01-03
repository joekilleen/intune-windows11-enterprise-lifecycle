# Tenant Expansion — Mergers & Acquisitions (M&A)  
**Endpoint, Identity, and Trust Integration Patterns for Corporate Transactions**

---

## Purpose

This document defines the **authoritative M&A-specific patterns** for expanding, integrating, or isolating Microsoft Intune–managed Windows 11 environments during mergers and acquisitions.

M&A activity represents a **high-risk trust boundary event**.  
The objective is to:
- Prevent inherited compromise
- Preserve legal and regulatory compliance
- Enable phased integration
- Maintain operational continuity
- Produce defensible due-diligence evidence

In M&A, **speed without governance creates latent risk**.

---

## M&A Threat Model (Authoritative)

During M&A, assume:

- Unknown security posture in target tenant
- Unknown admin practices and RBAC hygiene
- Unknown endpoint health and compliance
- Unknown device provenance
- Potential historical compromise

**Trust is not assumed — it is established deliberately.**

---

## M&A Integration Principles

1. **Isolate first, integrate later**
2. **Rebuild trust, do not inherit it**
3. **Pilot before scale**
4. **No shared privileged access**
5. **Evidence before promotion**
6. **Explicit risk acceptance**

---

## M&A Integration Options

### Option A — Full Tenant Isolation (Default / Day 0–90)

**Description**
- Acquired company remains in its own tenant
- No endpoint migration initially
- Limited cross-tenant collaboration only

**Controls**
- Entra ID B2B for collaboration
- Separate Intune tenants
- Separate Autopilot registries
- Separate break-glass accounts

**When Required**
- Regulated industries
- Unknown security maturity
- Active remediation required

---

### Option B — Phased Endpoint Integration

**Description**
- Gradual migration of devices into parent tenant
- Begins only after security validation

**Phases**
1. Identity trust establishment
2. Endpoint posture assessment
3. Pilot device migration
4. Controlled scale-out
5. Legacy tenant retirement

**Risk**
- Policy collision
- App compatibility issues
- Identity confusion

Mitigation requires **strict pilot enforcement**.

---

### Option C — Selective Integration (Hybrid)

**Description**
- Some business units integrated
- Others remain isolated indefinitely

**Use Case**
- Multi-brand holding companies
- Regulatory segmentation
- Regional autonomy

Requires **clear operational boundaries**.

---

## Endpoint Due Diligence (Mandatory)

Before any endpoint migration, assess:

| Control Area | Validation |
---|---|
| OS version | Supported Windows 11 builds |
| Device ownership | Corporate-owned only |
| Compliance | Encryption, secure boot, AV |
| Update posture | Patch currency |
| Admin access | Local admin sprawl |
| EDR coverage | Reporting consistency |
| Autopilot status | Device identity control |

Devices failing baseline **must not migrate**.

---

## Device Migration Rules (Non-Negotiable)

| Rule | Requirement |
---|---|
| Trust transfer | Prohibited |
| Device cloning | Prohibited |
| Tenant-to-tenant move | Prohibited |
| Local data migration | Prohibited |
| Re-enrollment | Mandatory |

**Approved method:**  
Full wipe → Autopilot re-enrollment in target tenant.

---

## Identity and Access Controls

### Mandatory Controls

- Separate Global Admins per tenant
- PIM enforced in all tenants
- No shared break-glass accounts
- Conditional Access enforced independently
- Logging retained independently

---

### Prohibited Practices

- Reusing admin credentials
- Syncing privileged roles
- Disabling CA “temporarily”
- Granting blanket exceptions during migration

Shortcuts become **permanent vulnerabilities**.

---

## Application Strategy During M&A

### Required Discipline

- Repackage critical applications
- Validate installers against parent standards
- Recreate assignments deliberately
- Remove legacy or shadow IT apps

M&A is an opportunity to **reduce technical debt**, not import it.

---

## Compliance and Regulatory Considerations

M&A activity must explicitly address:

- Data residency
- Industry regulation (finance, healthcare, gov)
- Retention requirements
- Legal hold obligations
- Regional encryption mandates

Compliance gaps during M&A are **frequent audit findings**.

---

## Evidence and Audit Requirements

The following artifacts **must** be retained:

| Artifact | Purpose |
---|---|
| Pre-acquisition risk assessment | Due diligence |
| Endpoint posture reports | Baseline |
| Migration plan | Risk control |
| Pilot results | Validation |
| Executive approvals | Risk acceptance |
| Post-integration validation | Assurance |

Auditors will expect **proof of isolation and testing**.

---

## Failure Modes and Lessons Learned

| Failure | Consequence |
---|---|
| Direct prod integration | Widespread incident |
| Inherited admin access | Lateral compromise |
| No pilot | Uncontrolled outages |
| Poor evidence | Audit failure |
| Rushed timeline | Long-term instability |

---

## Governance and Decision Authority

| Role | Responsibility |
---|---|
| Executive Sponsor | Risk acceptance |
| Enterprise Architecture | Pattern selection |
| Security | Trust validation |
| Endpoint Engineering | Technical execution |
| Legal / GRC | Compliance oversight |

No single team owns M&A risk alone.

---

## Change Control

M&A integration actions:
- Require executive approval
- Must have rollback strategy
- Must include pilot phase
- Must be documented in the Decision Log
- Must be reviewed post-integration

---

## Summary

M&A is a **trust reconstruction exercise**, not a technical merge.

When executed correctly:
- Risk is contained
- Integration is predictable
- Compliance is preserved
- Audits are defensible

When rushed:
- Legacy risk is imported
- Incidents surface months later
- Remediation cost multiplies

---

## Section Status

- Tenant Expansion — M&A patterns complete  
- Aligns with Section 10 DR and expansion strategy  

---
