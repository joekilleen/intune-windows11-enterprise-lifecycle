---
name: Defect
about: Report a defect, failure, or unexpected behavior requiring investigation
title: "[DEFECT] <short description>"
labels: defect
assignees: ''
---

# Defect Report

## Summary

Provide a clear, concise description of the defect.

- What is not working as expected?
- What *should* be happening?
- Who is impacted?

Avoid speculation.

---

## Classification

| Field | Selection |
---|---|
| Defect Type | ☐ Configuration ☐ Process ☐ Documentation ☐ Automation ☐ Other |
| Severity | ☐ Low ☐ Medium ☐ High ☐ Critical |
| Impact Scope | ☐ Single user ☐ Multiple users ☐ Systemic |
| Related Area | ☐ Enrollment ☐ Security ☐ Compliance ☐ Apps ☐ Updates ☐ Operations |

---

## Environment

| Item | Value |
---|---|
| Tenant | Production / Non-Production |
| Platform | Windows 11 |
| Management | Microsoft Intune |
| Device Type | ☐ Corporate ☐ Shared |
| Device Name(s) | |
| User(s) Affected | |
| Date/Time Observed (UTC) | |

---

## Observed Behavior

Describe **what actually happened**.

- Include error messages if present
- Include exact wording where possible
- Include timestamps (UTC)

---

## Expected Behavior

Describe **what should have happened** according to design or documentation.

---

## Reproduction Steps

Provide steps to reliably reproduce the issue.

1.  
2.  
3.  

If not reproducible, state **“Intermittent / Not Reproducible.”**

---

## Initial Triage (If Performed)

| Check | Result |
---|---|
| Device compliance checked | ☐ Yes ☐ No |
| Intune sync attempted | ☐ Yes ☐ No |
| Reboot attempted | ☐ Yes ☐ No |
| Known outage checked | ☐ Yes ☐ No |
| Similar issues identified | ☐ Yes ☐ No |

---

## Impact Assessment

| Area | Assessment |
---|---|
| User productivity | ☐ Low ☐ Medium ☐ High |
| Security risk | ☐ None ☐ Potential ☐ Confirmed |
| Compliance risk | ☐ None ☐ Potential ☐ Confirmed |
| Business impact | Narrative description |

---

## Evidence

Attach or reference relevant evidence.

- Logs
- Screenshots
- Error codes
- Links to monitoring dashboards
- Related incident IDs

Use the **Evidence Index** for reference where applicable.

---

## Related Records

Link related items if known:

- Incident ID:  
- Change Request ID:  
- AAR / RCA ID:  
- Previous Defect(s):  

---

## Escalation Guidance

Check if escalation is required:

- ☐ Tier 2 escalation required
- ☐ Tier 3 (Engineering / RCA) required
- ☐ Security escalation required
- ☐ No escalation at this time

If escalation is required, follow the appropriate runbook.

---

## Temporary Workaround (If Any)

Describe any **approved** workaround.

- Workaround description
- Duration
- Risks introduced (if any)

Unapproved workarounds are not permitted.

---

## Resolution Notes (To Be Completed Upon Closure)

- Root cause summary
- Fix implemented
- Validation performed
- Follow-up actions required

---

## Closure Checklist

- ☐ Defect resolved
- ☐ Validation completed
- ☐ Documentation updated (if required)
- ☐ AAR required ☐ Yes ☐ No
- ☐ Evidence indexed
- ☐ Issue closed with notes

---

## Audit Notes

- This defect record is an operational artifact
- Entries must be factual and timestamped
- Do not delete or rewrite history
- Corrections must be appended

---
