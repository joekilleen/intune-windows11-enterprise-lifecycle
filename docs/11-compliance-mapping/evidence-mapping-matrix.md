# Evidence Mapping Matrix  
**Control-to-Evidence Traceability for Audit, Risk, and Client Assurance**

---

## Purpose

This document defines the **authoritative evidence mapping matrix** for the Windows 11 Intune Enterprise Device Lifecycle architecture.

Its purpose is to:
- Provide a single, canonical reference for audit evidence
- Map controls to concrete, retrievable artifacts
- Reduce audit response time and operational friction
- Ensure consistency across CIS, NIST, and ISO inquiries
- Prevent ad-hoc, incomplete, or non-defensible evidence production

If evidence is not mapped here, it is **not considered auditable**.

---

## How to Use This Matrix

This matrix is used during:
- Internal audits
- External audits (SOC 2, ISO 27001, customer security reviews)
- Client due diligence
- Executive assurance reviews
- Incident post-mortems

For each control:
1. Identify the control area
2. Locate the mapped evidence
3. Retrieve from the listed system of record
4. Validate timestamp and scope
5. Deliver using approved audit workflow

---

## Evidence Classification

| Evidence Type | Description |
---|---|
| Configuration | Policy or setting definitions |
| Assignment | Scope and targeting proof |
| Operational | Logs, timelines, reports |
| Procedural | Runbooks, workflows |
| Governance | Reviews, approvals, decisions |

All five classes are required for **full control maturity**.

---

## Identity and Access Controls

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| RBAC design | RBAC matrix | Repository | 2 years |
| Role assignments | Role assignment export | Entra ID | 1 year |
| Privileged access | PIM activation logs | Entra ID | 1 year |
| Least privilege | Access review records | GRC repository | 2 years |
| Break-glass accounts | Account configuration + review | Entra ID | 2 years |

---

## Device Inventory and Ownership

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Device inventory | Device list export | Intune | 180 days |
| Ownership status | Corporate ownership flag | Intune | 180 days |
| Autopilot registration | Autopilot device inventory | Intune | 180 days |
| Decommissioned devices | Asset retirement record | Asset system | 7 years |

---

## Configuration and Baseline Enforcement

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Security baseline | Baseline configuration export | Intune | 1 year |
| Configuration profiles | Profile JSON / export | Intune | 1 year |
| Settings enforcement | Assignment report | Intune | 180 days |
| Drift remediation | Proactive remediation logs | Intune | 180 days |

---

## Compliance and Access Enforcement

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Compliance policies | Policy definition export | Intune | 1 year |
| Compliance evaluation | Device compliance report | Intune | 180 days |
| Grace period handling | Compliance history | Intune | 180 days |
| Access enforcement | CA sign-in logs | Entra ID | 90 days |

---

## Endpoint Security Controls

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| EDR onboarding | Defender onboarding status | Defender | 180 days |
| Malware protection | Alert history | Defender | 180 days |
| ASR rules | Policy configuration | Intune | 1 year |
| Device isolation | Isolation action logs | Defender | 1 year |

---

## Update and Servicing Controls

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Update rings | Ring configuration export | Intune | 1 year |
| Quality updates | Update compliance report | Intune | 180 days |
| Feature updates | Feature update policy | Intune | 1 year |
| Rollback actions | Rollback execution logs | Intune | 1 year |

---

## Application Lifecycle Controls

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| App inventory | App list export | Intune | 180 days |
| Required apps | Assignment report | Intune | 180 days |
| Supersedence | Supersedence chain | Intune | 1 year |
| ESP validation | ESP status reports | Intune | 180 days |

---

## Incident Response and Recovery

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Incident declaration | Incident record | IR system | 2 years |
| Device isolation | Isolation timeline | Defender | 1 year |
| Recovery action | Reset / wipe logs | Intune | 1 year |
| Post-incident review | PIR documentation | GRC repository | 2 years |

---

## Device Lifecycle Operations

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Autopilot Reset | Reset audit log | Intune | 1 year |
| Device wipe | Wipe completion record | Intune | 1 year |
| Autopilot deregistration | Deletion audit log | Intune | 1 year |
| Hardware replacement | Asset replacement record | Asset system | 7 years |

---

## Governance and Change Management

| Control Area | Evidence Artifact | System of Record | Retention |
---|---|---|---|
| Architectural decisions | Decision log | Repository | 5 years |
| Change approvals | Change records | Change system | 2 years |
| Exceptions | Risk acceptance forms | GRC repository | 2 years |
| Access reviews | Review sign-off | GRC repository | 2 years |

---

## Evidence Quality Requirements

All evidence must be:

- Timestamped
- Attributable to a named system or user
- Exportable in native format
- Immutable once archived
- Retained per policy

Screenshots are **supplemental only**, never primary evidence.

---

## Audit Response SLA

| Request Type | SLA |
---|---|
| Standard audit request | ≤ 48 business hours |
| Client security questionnaire | ≤ 3 business days |
| Incident evidence | ≤ 24 hours |
| Regulatory inquiry | As contractually required |

Failure to meet SLA is considered an **operational control gap**.

---

## Maintenance and Review

- This matrix must be reviewed **annually**
- Updates required after:
  - Major architectural changes
  - New regulatory requirements
  - Audit findings
- Changes must be logged in the Decision Log

---

## Summary

This evidence mapping matrix ensures that:

- Every control has proof
- Every proof has an owner
- Every audit request is predictable
- Every response is defensible

Controls without mapped evidence **do not exist** for auditors.

---

## Document Status

- ☐ Draft
- ☐ Approved
- ☐ Operational
- ☐ Reviewed (Annual)

---
