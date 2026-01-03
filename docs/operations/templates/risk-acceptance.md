# Risk Acceptance Record  
**Formal Risk Acceptance and Time-Bound Exception Authorization**

---

## Purpose

This document records **explicit, time-bound acceptance of risk** where a known security, compliance, or operational control cannot be fully remediated within required timelines.

Its objectives are to:
- Prevent silent or informal risk acceptance
- Ensure risks are owned at the appropriate level
- Document business justification and compensating controls
- Provide audit-ready evidence of informed decision-making
- Enforce expiration and review of accepted risks

Risk acceptance is **an exception**, not a control.

---

## Governing References

This record is governed by and must align with:

- Security Escalation Runbook
- Tier 3 Root Cause Analysis (RCA) Runbook
- After-Action Review (AAR) Runbook
- Change Management Process
- Evidence Index

Verbal approvals are **not valid**.

---

## Risk Acceptance Metadata

| Field | Value |
---|---|
| Risk Acceptance ID | RISK-YYYYMMDD-### |
| Date Submitted | YYYY-MM-DD |
| Submitted By | Name / Role |
| Business Unit | |
| Related Incident ID(s) | INC-YYYYMMDD-### |
| Related AAR / RCA ID(s) | AAR- / RCA- |
| Risk Category | ☐ Security ☐ Compliance ☐ Operational ☐ Availability |
| Risk Status | ☐ Proposed ☐ Approved ☐ Rejected ☐ Expired |

---

## 1. Risk Description

Provide a clear, factual description of the risk.

- What control is not met or degraded?
- What condition creates the risk?
- What systems or users are affected?

Avoid vague or generic language.

---

## 2. Root Cause Summary

Summarize the underlying cause(s) of the risk.

| Category | Description |
---|---|
| Architecture | |
| Configuration | |
| Process | |
| Governance | |
| Monitoring | |
| External Dependency | |

Reference the RCA where applicable.

---

## 3. Impact Assessment

Assess the potential impact **if the risk materializes**.

| Area | Assessment |
---|---|
| Confidentiality | ☐ Low ☐ Medium ☐ High |
| Integrity | ☐ Low ☐ Medium ☐ High |
| Availability | ☐ Low ☐ Medium ☐ High |
| Compliance | ☐ Low ☐ Medium ☐ High |
| Business Impact | Narrative description |

Impact must be stated in business terms where possible.

---

## 4. Likelihood Assessment

Estimate the likelihood of occurrence during the acceptance period.

| Likelihood | Rationale |
---|---|
| ☐ Low ☐ Medium ☐ High | |

Likelihood should consider:
- Historical occurrences
- Exposure window
- Threat environment
- Control maturity

---

## 5. Risk Rating (Pre-Acceptance)

| Dimension | Rating |
---|---|
| Overall Risk Rating | ☐ Low ☐ Medium ☐ High |
| Risk Appetite Alignment | ☐ Within ☐ Exceeds |

If risk exceeds appetite, executive approval is mandatory.

---

## 6. Compensating Controls

List controls implemented to **reduce likelihood or impact** during the acceptance period.

| Control | Description |
---|---|
| | |
| | |

Compensating controls must be active and verifiable.

---

## 7. Justification for Acceptance

Provide the business rationale for accepting the risk.

Common justifications include:
- Temporary vendor limitation
- Phased remediation dependency
- Business continuity requirement
- Regulatory or contractual timing

Cost or convenience alone is **not sufficient**.

---

## 8. Acceptance Scope and Duration

| Item | Value |
---|---|
| Acceptance Start Date | YYYY-MM-DD |
| Acceptance Expiration Date | YYYY-MM-DD |
| Affected Systems | |
| Affected Users / Groups | |
| Geographic Scope | |

Risk acceptance **must be time-bound**.

---

## 9. Remediation Plan

Describe the plan to fully remediate the risk.

| Action | Owner | Target Date |
---|---|---|
| | | |
| | | |

A remediation plan is required for all accepted risks.

---

## 10. Monitoring and Review

Define how the risk will be monitored during the acceptance period.

- Alerts or dashboards reviewed
- Review frequency
- Responsible owner

Failure to monitor invalidates acceptance.

---

## 11. Approval and Authorization

### Required Approvals

| Role | Name | Signature | Date |
---|---|---|---|
| Risk Owner | | | |
| Security | | | |
| Business Owner | | | |
| Executive (if required) | | | |

Approval confirms:
- Risk is understood
- Compensating controls are adequate
- Accountability is accepted

---

## 12. Expiration and Closure

At or before expiration:

- ☐ Risk remediated and closed
- ☐ Risk extended (new approval required)
- ☐ Risk escalated due to change

Extensions require a **new Risk Acceptance Record**.

---

## 13. Evidence References

List supporting evidence.

| Evidence ID | Description | Location |
---|---|---|
| | | |

Evidence must be indexed and retained.

---

## Audit and Compliance Notes

- Undocumented risk acceptance is a control failure
- Expired risk acceptance without remediation is a violation
- This document may be reviewed by auditors and regulators

---

## Summary

Risk acceptance is a **conscious business decision**, not a technical workaround.

When documented correctly:
- Accountability is clear
- Audits are defensible
- Exceptions remain temporary
- Risk is managed, not ignored

---

## Template Status

- ☐ Approved
- ☐ In Use
- ☐ Archived

---
