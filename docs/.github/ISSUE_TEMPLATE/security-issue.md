---
name: Security Issue
about: Report a suspected or confirmed security issue requiring controlled handling
title: "[SECURITY] <short, non-sensitive description>"
labels: security
assignees: ''
---

# Security Issue Report

> ⚠️ **DO NOT include sensitive details in this issue.**  
> This issue is for **tracking and escalation only**.  
> Technical details must be shared via approved security channels.

---

## Summary

Provide a **high-level, non-sensitive** description of the security concern.

- What type of issue is suspected?
- What systems or scope may be affected?
- How was it detected?

Do **not** include indicators of compromise, credentials, or exploit details.

---

## Classification

| Field | Selection |
---|---|
| Issue Type | ☐ Suspected Incident ☐ Confirmed Incident ☐ Vulnerability ☐ Policy Violation |
| Severity | ☐ Low ☐ Medium ☐ High ☐ Critical |
| Detection Source | ☐ User Report ☐ Monitoring ☐ Alert ☐ Audit ☐ Other |
| Environment | ☐ Production ☐ Non-Production ☐ Unknown |

---

## Initial Impact Assessment (High-Level)

| Area | Assessment |
---|---|
| Users affected | ☐ None ☐ Suspected ☐ Confirmed |
| Devices affected | ☐ None ☐ Suspected ☐ Confirmed |
| Data impact | ☐ None ☐ Suspected ☐ Confirmed |
| Business impact | ☐ Low ☐ Medium ☐ High |

If impact is unclear, state **“Under Investigation.”**

---

## Escalation Status

| Item | Status |
---|---|
| Security Escalation Triggered | ☐ Yes ☐ No |
| Security Team Notified | ☐ Yes ☐ No |
| Incident ID (if assigned) | |
| Time Escalated (UTC) | |

If escalation has **not** occurred, follow the **Security Escalation Runbook immediately**.

---

## Containment Status (If Known)

| Item | Status |
---|---|
| Containment initiated | ☐ Yes ☐ No ☐ Unknown |
| Device isolation | ☐ Yes ☐ No ☐ Unknown |
| Account action taken | ☐ Yes ☐ No ☐ Unknown |

Do not attempt containment unless authorized.

---

## Related Records

Link related artifacts **without sensitive detail**:

- Incident ID:
- Defect ID:
- Change Request ID:
- Risk Acceptance ID:

---

## Next Steps

Describe the **administrative next step only**.

Examples:
- Escalate to Security Operations
- Await security guidance
- Track investigation progress
- Coordinate recovery after clearance

---

## Communication Restrictions

- ☐ No user communication authorized
- ☐ Executive communication pending
- ☐ External communication prohibited

All communications must follow approved templates.

---

## Closure Notes (To Be Completed After Resolution)

- Resolution summary (non-sensitive)
- Reference to AAR / RCA ID
- Confirmation that evidence is archived

---

## Audit and Legal Notes

- This issue intentionally excludes sensitive data
- Detailed findings must remain in secured systems
- GitHub issues may be reviewed by auditors
- Do not upload logs, screenshots, or artifacts here

---

## Closure Checklist

- ☐ Security incident handled via approved process
- ☐ AAR completed (if required)
- ☐ Evidence indexed
- ☐ Issue closed with appropriate references

---
