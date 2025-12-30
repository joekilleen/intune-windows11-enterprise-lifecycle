# Access Reviews and Audit Readiness  
**Continuous Recertification, Evidence Production, and Control Assurance**

---

## Purpose

This document defines the **authoritative access review and audit readiness framework** for Microsoft Intune, Microsoft Entra ID, and related endpoint administration services.

The objectives are to:
- Prevent privilege creep
- Ensure least-privilege remains enforced over time
- Detect and remediate access misalignment
- Provide immediate, defensible audit evidence
- Demonstrate operational maturity to auditors and regulators

Access that is not periodically reviewed is **implicitly untrusted**.

---

## Design Objectives

The access review framework must ensure:

1. **Regular recertification**
2. **Clear ownership**
3. **Documented decisions**
4. **Time-bound exceptions**
5. **Immediate evidence availability**
6. **Minimal audit disruption**

---

## Scope of Access Reviews

Access reviews **must** cover the following:

| Scope | System |
---|---|
| Privileged roles | Entra ID (PIM) |
| Intune RBAC roles | Intune |
| Custom roles | Intune |
| Scope tag assignments | Intune |
| Break-glass accounts | Entra ID |
| Third-party integrations | As applicable |

No administrative access is exempt.

---

## Review Cadence (Authoritative)

| Access Type | Frequency |
---|---|
| Tier 0 (Identity / Security) | Quarterly |
| Tier 1 (Endpoint Admin) | Quarterly |
| Tier 2 (Service Desk) | Semi-annual |
| Custom roles | Quarterly |
| Break-glass accounts | Monthly |
| External / vendor access | Quarterly |

Missed reviews are treated as **control failures**.

---

## Ownership and Accountability

Every review must have a **named owner**.

| Role | Responsibility |
---|---|
| Security | Tier 0 and security roles |
| Endpoint Leadership | Tier 1 and Intune roles |
| IT Operations | Tier 2 roles |
| GRC | Review oversight and evidence |
| Management | Risk acceptance |

Unowned reviews are invalid.

---

## Review Execution Model

### Step 1 — Inventory

Generate a complete access inventory:

- Role assignments
- Scope tags
- PIM eligible and active assignments
- Service principals and automation identities

Inventory must be **exported and archived**.

---

### Step 2 — Validation

For each assignment, validate:

- Business justification still valid
- Scope remains appropriate
- Least privilege still applies
- Separation of duties preserved
- Access duration appropriate

“Just in case” access is **not acceptable**.

---

### Step 3 — Decision

Each assignment must be explicitly marked as:

| Decision | Action |
---|---|
| Approved | Retain access |
| Modified | Reduce scope or role |
| Revoked | Remove access |
| Exception | Time-bound approval |

Silence is **not approval**.

---

### Step 4 — Remediation

- Remove or modify access immediately
- Validate removal took effect
- Confirm no orphaned permissions remain

Delayed remediation is a **policy violation**.

---

### Step 5 — Documentation

For each review cycle, record:

- Review date
- Review owner
- Scope reviewed
- Decisions made
- Exceptions granted
- Remediation completed

Documentation must be immutable once approved.

---

## Exception Management

### Exception Requirements

Exceptions must:

- Be explicitly documented
- Have a business justification
- Be time-bound (maximum 90 days)
- Have an identified risk owner
- Be reviewed at each cycle

Permanent exceptions are **not permitted**.

---

## Audit Readiness Model

The organization must be able to produce the following **within 48 hours**:

| Evidence | Source |
---|---|
| Current access inventory | Entra ID / Intune |
| Last access review records | GRC repository |
| PIM activation logs | Entra ID |
| Role assignment history | Entra ID audit logs |
| Scope tag mappings | Intune |
| Exception approvals | Change / risk system |

Failure to produce evidence is treated as **control failure**.

---

## Evidence Retention Requirements

| Artifact | Minimum Retention |
---|---|
| Access review records | 2 years |
| PIM activation logs | 1 year |
| Role assignment logs | 1 year |
| Exception approvals | 2 years |
| Audit responses | 2 years |

Retention must align with regulatory requirements where applicable.

---

## Common Audit Findings (Avoid)

| Finding | Root Cause |
---|---|
| Privilege creep | No reviews |
| Orphaned access | Poor offboarding |
| Excessive permissions | No scope tags |
| Missing evidence | Ad-hoc reviews |
| Standing privilege | No PIM enforcement |

---

## Metrics and KPIs

| Metric | Target |
---|---|
| Reviews completed on time | 100% |
| Unjustified access | 0 |
| Exception overruns | 0 |
| Audit evidence SLA | < 48 hours |

---

## Continuous Improvement

After each review cycle:

- Identify recurring issues
- Adjust role definitions
- Refine scope tag taxonomy
- Improve onboarding/offboarding automation

Governance controls must **evolve with the environment**.

---

## Change Control

Changes to the access review process:
- Require security and GRC approval
- Must be documented in the Decision Log
- Must not weaken control frequency or scope

---

## Summary

Access reviews are the **heartbeat of least privilege**.

When executed correctly:
- Privilege creep is eliminated
- Separation of duties is enforced
- Audits are predictable
- Risk decisions are explicit

When skipped or rushed:
- Controls decay silently
- Risk accumulates
- Audits fail unexpectedly

---

## Section Completion

With this document, **Section 9 — Governance, RBAC, and Delegated Administration** is **complete and audit-ready**.

---

## Next Section

Proceed to:

**`docs/10-nonprod-dr-expansion/28-non-production-and-pilot-tenants.md`**

This section defines **pilot environments, test rings, and safe change validation patterns**.
