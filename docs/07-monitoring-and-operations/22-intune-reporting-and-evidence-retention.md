# Intune Reporting and Evidence Retention  
**Operational Reporting, Audit Readiness, and Chain-of-Custody**

---

## Purpose

This document defines the **authoritative reporting and evidence retention model** for Windows 11 endpoints managed with Microsoft Intune and Microsoft Entra ID.

The objective is to ensure that:
- Operational decisions are data-driven
- Security enforcement is provable
- Audit requests can be satisfied without ad-hoc work
- Evidence integrity and chain-of-custody are maintained

If evidence cannot be produced on demand, **the control is considered ineffective**.

---

## Reporting Design Objectives

The reporting strategy must ensure:

1. **Single source of truth**
2. **Consistent metrics**
3. **Sufficient retention**
4. **Controlled access**
5. **Exportability**
6. **Audit defensibility**

---

## Systems of Record (Authoritative)

| Domain | System of Record |
---|---|
| Device state and compliance | Intune |
| Application deployment | Intune |
| Update compliance | Intune |
| Access enforcement | Entra ID |
| Threat detection | Microsoft Defender |
| Audit trail | Entra ID / Intune |

Reports from other tools are **supplemental only**.

---

## Standard Operational Reports

### Device Compliance Reporting

| Report | Purpose | Frequency |
---|---|---|
| Device compliance status | Trust posture | Weekly |
| Non-compliance reasons | Root cause analysis | Weekly |
| Grace period expirations | Enforcement validation | Weekly |

---

### Application Reporting

| Report | Purpose | Frequency |
---|---|---|
| App install success/failure | Reliability | Weekly |
| Supersedence success | Version control | Per release |
| ESP app success | Enrollment integrity | Monthly |

---

### Update and Servicing Reporting

| Report | Purpose | Frequency |
---|---|---|
| Quality update compliance | Security SLA | Weekly |
| Feature update adoption | Platform governance | Monthly |
| Rollback events | Stability validation | As needed |

---

### Access and Enforcement Reporting

| Report | Purpose | Frequency |
---|---|---|
| Conditional Access outcomes | Enforcement proof | Weekly |
| Blocked sign-in attempts | Risk validation | Weekly |
| Legacy auth blocks | Control effectiveness | Monthly |

---

## Evidence Retention Requirements

### Minimum Retention Periods (Authoritative)

| Evidence Type | Minimum | Recommended |
---|---|---|
| Device compliance history | 90 days | 180 days |
| App deployment logs | 90 days | 180 days |
| Update compliance | 90 days | 180 days |
| Conditional Access logs | 30 days | 90 days |
| Audit logs (changes) | 90 days | 1 year |
| Incident evidence | Case lifetime | +1 year |

Retention must meet **regulatory and contractual obligations**.

---

## Evidence Export and Preservation

### Approved Export Methods

- Native Intune export
- Entra ID log export
- Defender alert export
- Secure storage in evidence repository

**Prohibited**
- Manual copy/paste without metadata
- Screenshots as primary evidence
- Untracked local storage

---

## Chain-of-Custody Requirements

All exported evidence must include:

| Attribute | Requirement |
---|---|
| Export date/time | Mandatory |
| Exported by | Named individual |
| Source system | Explicit |
| Scope | Defined |
| Storage location | Documented |

Evidence must be **read-only** once archived.

---

## Access Control for Evidence

| Role | Access |
---|---|
| Endpoint Engineering | Operational reports |
| Security Operations | Full security evidence |
| GRC / Audit | Read-only evidence |
| Management | Summary reports |

Least-privilege access **must be enforced**.

---

## Audit Response Workflow

1. Receive audit request
2. Identify required evidence artifacts
3. Export from system of record
4. Validate completeness
5. Deliver via approved channel
6. Log request and response

Ad-hoc or verbal responses are **not acceptable**.

---

## Common Audit Failures (Avoid)

| Failure | Impact |
---|---|
| Insufficient log retention | Control invalidated |
| Screenshots only | Evidence rejected |
| Inconsistent metrics | Credibility loss |
| Missing timestamps | Chain broken |
| No access controls | Integrity risk |

---

## Reporting Quality Controls

- Reports reviewed for accuracy
- Metrics definitions documented
- Changes tracked in Decision Log
- Sampling validated quarterly

---

## Metrics for Operational Maturity

| Metric | Target |
---|---|
| Evidence availability on request | 100% |
| Audit response time | < 2 business days |
| Report accuracy | 100% |
| Evidence integrity issues | 0 |

---

## Change Control

Reporting or retention changes:
- Require security approval
- Must not reduce retention below minimums
- Must be documented in the Decision Log
- Must be validated after change

---

## Summary

Reporting and evidence retention are the **proof layer** of endpoint security.

They demonstrate that:
- Controls exist
- Controls operate continuously
- Enforcement is real
- Recovery is traceable
- Risk is managed deliberately

If it is not reported and retained, **it cannot be defended**.

---

## Section Completion

With this document, **Section 7 — Monitoring & Operations** is **complete and audit-ready**.

---

## Next Section

Proceed to:

**`docs/08-device-lifecycle-operations/23-device-reset-reassignment.md`**

This section defines **device lifecycle actions: reset, reassignment, refresh, and decommissioning**.
