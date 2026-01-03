---
name: Change Request
about: Propose a controlled change to scope, configuration, architecture, or operations
title: "[CHANGE] <short description>"
labels: change-request
assignees: ''
---

# Change Request

## Summary

Provide a clear, concise description of the requested change.

- What is changing?
- Why is the change needed?
- What problem does it address?

Avoid implementation detail in this section.

---

## Change Classification

| Field | Selection |
---|---|
| Change Type | ☐ Scope ☐ Configuration ☐ Architecture ☐ Process ☐ Documentation |
| Change Nature | ☐ Planned ☐ Reactive ☐ Corrective ☐ Preventive |
| Urgency | ☐ Low ☐ Medium ☐ High ☐ Emergency |
| Environment | ☐ Non-Production ☐ Production ☐ Both |

---

## Business Justification

Describe the **business driver** for this change.

| Driver | Description |
---|---|
| Risk reduction | ☐ Yes ☐ No |
| Compliance requirement | ☐ Yes ☐ No |
| Operational stability | ☐ Yes ☐ No |
| User experience | ☐ Yes ☐ No |
| Cost impact | ☐ Increase ☐ Decrease ☐ Neutral |

Changes without clear justification may be rejected.

---

## Description of Proposed Change

Describe the change in sufficient detail for review.

- What will be added, removed, or modified?
- Which components are affected?
- What behavior will change?

---

## Scope Impact Assessment

Indicate which areas are impacted.

| Area | Impact |
---|---|
| Enrollment / Autopilot | ☐ None ☐ Minor ☐ Major |
| Security Baselines | ☐ None ☐ Minor ☐ Major |
| Compliance / Conditional Access | ☐ None ☐ Minor ☐ Major |
| Applications | ☐ None ☐ Minor ☐ Major |
| Updates / Servicing | ☐ None ☐ Minor ☐ Major |
| Operations / Runbooks | ☐ None ☐ Minor ☐ Major |
| Governance / RBAC | ☐ None ☐ Minor ☐ Major |

---

## Risk Assessment

| Area | Assessment |
---|---|
| Security risk | ☐ None ☐ Low ☐ Medium ☐ High |
| Compliance risk | ☐ None ☐ Low ☐ Medium ☐ High |
| Availability risk | ☐ None ☐ Low ☐ Medium ☐ High |
| Reversibility | ☐ Easy ☐ Moderate ☐ Difficult |

If any risk is Medium or High, additional review is required.

---

## Dependencies and Constraints

List any dependencies introduced or affected by this change.

- Licensing
- Platform limitations
- Third-party services
- Timing constraints
- Organizational dependencies

---

## Alternatives Considered

List alternatives that were considered and why they were not selected.

| Alternative | Reason Not Selected |
---|---|

---

## Implementation Plan (High-Level)

Provide a **high-level plan only**.

1.  
2.  
3.  

Detailed steps belong in runbooks or pull requests.

---

## Validation and Rollback

### Validation Criteria

- How will success be verified?
- What signals confirm the change worked?

### Rollback Plan

- How will the change be reversed if needed?
- What is the expected rollback time?

Rollback must be feasible unless explicitly accepted as risk.

---

## Governance and Approvals

Check all that apply:

- ☐ Architecture review required
- ☐ Security review required
- ☐ Compliance review required
- ☐ Risk acceptance required
- ☐ Client approval required (SOW)

Changes may not proceed without required approvals.

---

## Related Records

Link related artifacts:

- Incident ID:
- Defect ID:
- Feature Request ID:
- Risk Acceptance ID:
- Client Change Request (if applicable):

---

## Approval Status

| Stage | Status |
---|---|
| Submitted | ☐ |
| Under Review | ☐ |
| Approved | ☐ |
| Rejected | ☐ |
| Implemented | ☐ |
| Closed | ☐ |

---

## Decision Notes

*(Completed by reviewers)*

- Approval or rejection rationale
- Conditions or constraints
- Required follow-up actions

---

## Audit Notes

- This change request is a governance artifact
- All decisions must be documented
- Emergency changes require post-implementation review
- Approved changes must be traceable to implementation evidence

---
