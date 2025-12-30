# Win32 Application Intake Form  
**Authoritative Intake and Approval Record**

---

## Purpose

This document serves as the **mandatory intake and approval record** for any Win32 application proposed for deployment via Microsoft Intune.

No application may proceed to packaging, testing, or deployment **without a completed and approved intake form**.

This document establishes:
- Ownership
- Risk classification
- Deployment intent
- ESP suitability
- Audit traceability

---

## Application Identification

| Field | Value |
---|---|
| Application Name |  |
| Publisher / Vendor |  |
| Vendor Website |  |
| Application Category | (Security / Productivity / LOB / Utility / Other) |
| Business Function |  |
| Primary Use Case |  |

---

## Version and Source Details

| Field | Value |
---|---|
| Vendor Version |  |
| Installer Type | (EXE / MSI / ZIP / Other) |
| Installer Source | (Vendor portal / License portal / Other) |
| Installer Hash (SHA256) |  |
| Installer Download Date |  |

---

## Business Ownership

| Field | Value |
---|---|
| Business Owner (Name / Role) |  |
| Technical Owner |  |
| Support Team |  |
| Vendor Support Contract | (Yes / No) |
| End-of-Life Date (if known) |  |

**Rule**  
Applications without a named business owner **must not be deployed**.

---

## Deployment Classification

| Field | Selection |
---|---|
| Deployment Type | Required / Available |
| Target Audience | (All devices / Role-based / Departmental) |
| Assignment Scope | Device-based / User-based |
| ESP Required | Yes / No |
| ESP-Safe Candidate | Yes / No |

---

## ESP Suitability Assessment

Complete **only if ESP Required = Yes**.

| Criterion | Pass / Fail |
---|---|
| Silent installation supported |  |
| System context install |  |
| No reboot required |  |
| Install time < 10 minutes |  |
| Deterministic detection possible |  |
| No user licensing dependency |  |

**Decision**
- ☐ Approved for ESP
- ☐ Rejected for ESP (post-ESP only)

---

## Security Impact Assessment

| Area | Assessment |
---|---|
| Privileged access required | Yes / No |
| Network access required | Yes / No |
| Data sensitivity | Low / Medium / High |
| Known vulnerabilities | Yes / No |
| Third-party services used | Yes / No |

---

## Compliance and Risk Classification

| Field | Value |
---|---|
| Risk Level | Low / Medium / High |
| Compliance Impact | None / Moderate / High |
| Regulatory Considerations | (If applicable) |
| Requires Security Review | Yes / No |

---

## Packaging Requirements (Pre-Approval)

| Requirement | Confirmed |
---|---|
| System-context install | ☐ |
| Silent switches identified | ☐ |
| Deterministic detection method defined | ☐ |
| Clean uninstall supported | ☐ |
| Logging strategy defined | ☐ |
| Supersedence path feasible | ☐ |

---

## Deployment Dependencies

| Dependency | Details |
---|---|
| Required pre-requisites |  |
| Conflicting applications |  |
| OS version constraints |  |
| Licensing dependencies |  |

---

## Testing Requirements

| Test | Required |
---|---|
| Clean Autopilot enrollment test | ☐ |
| ESP test (if applicable) | ☐ |
| Upgrade test | ☐ |
| Uninstall test | ☐ |
| Failure scenario test | ☐ |

---

## Approval Record

### Required Approvals

| Role | Name | Date | Approved |
---|---|---|---|
| Business Owner |  |  | ☐ |
| Endpoint Engineering |  |  | ☐ |
| Security (if required) |  |  | ☐ |

---

## Intake Decision

| Decision | Selection |
---|---|
| Approved for Packaging | ☐ |
| Approved (Post-ESP Only) | ☐ |
| Rejected | ☐ |
| Deferred | ☐ |

**Decision Notes**
<enter justification, conditions, or constraints>


---

## Change and Audit Reference

| Field | Value |
---|---|
| Decision Log Entry ID |  |
| Related Change Request |  |
| Review Date |  |
| Next Review Due |  |

---

## Governance Notes

- This document must be retained for the **entire lifecycle** of the application
- Updates to application versions require **new intake records**
- Intake approval does **not** authorize deployment without successful testing
- This document may be requested during audits or incident reviews

---

## Status

- ☐ Intake Complete
- ☐ Approved for Packaging
- ☐ Archived (Retired Application)

---
