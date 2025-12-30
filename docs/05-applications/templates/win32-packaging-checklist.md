This checklist is designed to be used as a gating control—it should be completed and retained before any Win32 app reaches production.

# Win32 Packaging Checklist  
**Pre-Production Readiness and Quality Gate**

---

## Purpose

This checklist defines the **mandatory validation steps** required before a Win32 application may be deployed via Microsoft Intune.

Completion of this checklist confirms that the application:
- Meets enterprise packaging standards
- Is safe for ESP (if applicable)
- Can be upgraded, rolled back, and audited
- Will not introduce operational or security risk

An application that fails this checklist **must not be deployed**.

---

## Application Metadata

| Field | Value |
---|---|
| Application Name |  |
| Version |  |
| Publisher |  |
| Intune App Name |  |
| Packaging Engineer |  |
| Date |  |

---

## Intake Verification

| Check | Status |
---|---|
| Win32 Application Intake Form completed | ☐ |
| Business owner identified | ☐ |
| Deployment type approved (Required / Available) | ☐ |
| ESP suitability assessed (if applicable) | ☐ |
| Risk classification completed | ☐ |

---

## Package Structure Validation

| Check | Status |
---|---|
| Source directory organized per standard | ☐ |
| Install.ps1 present and validated | ☐ |
| Uninstall.ps1 present and validated | ☐ |
| Detection logic defined and documented | ☐ |
| Logging implemented | ☐ |
| Scripts UTF-8 encoded | ☐ |

---

## Installation Behavior

| Check | Status |
---|---|
| System-context installation confirmed | ☐ |
| Silent installation verified | ☐ |
| No user prompts | ☐ |
| No reboot required (ESP-safe apps) | ☐ |
| Exit codes handled correctly | ☐ |
| Idempotent install behavior | ☐ |

---

## Detection Rule Validation

| Check | Status |
---|---|
| Detection uniquely identifies version | ☐ |
| Detection survives reboot | ☐ |
| Detection does not rely on user profile | ☐ |
| Detection tested before and after install | ☐ |
| Detection tested after uninstall | ☐ |

---

## Uninstall Validation

| Check | Status |
---|---|
| Uninstall removes all components | ☐ |
| Silent uninstall verified | ☐ |
| Uninstall idempotent | ☐ |
| No orphaned services or scheduled tasks | ☐ |

---

## ESP Safety (If Applicable)

Complete only if the application is marked **ESP-required**.

| Check | Status |
---|---|
| Install completes in < 10 minutes | ☐ |
| No reboot triggered | ☐ |
| No external dependencies beyond vendor CDN | ☐ |
| Detection evaluated during ESP | ☐ |
| Tested during clean Autopilot enrollment | ☐ |

---

## Supersedence Readiness

| Check | Status |
---|---|
| Previous version identified | ☐ |
| Supersedence chain planned | ☐ |
| Uninstall of previous version validated | ☐ |
| New version installs cleanly over old | ☐ |
| Rollback path tested | ☐ |

---

## Assignment Strategy Validation

| Check | Status |
---|---|
| Required vs Available assignment confirmed | ☐ |
| Device vs User targeting validated | ☐ |
| ESP assignments minimized | ☐ |
| Pilot group assignment configured | ☐ |

---

## Monitoring and Reporting

| Check | Status |
---|---|
| Install success tracked in Intune | ☐ |
| Failure reporting validated | ☐ |
| Logs accessible on device | ☐ |
| Alert thresholds reviewed | ☐ |

---

## Security Review (If Required)

| Check | Status |
---|---|
| Security review completed | ☐ |
| No excessive privileges required | ☐ |
| No insecure configurations introduced | ☐ |
| ASR/Defender compatibility validated | ☐ |

---

## Documentation and Evidence

| Check | Status |
---|---|
| Packaging documentation updated | ☐ |
| Detection logic documented | ☐ |
| Supersedence plan documented | ☐ |
| Decision Log updated | ☐ |
| Evidence retained | ☐ |

---

## Final Approval

| Role | Name | Date | Approved |
---|---|---|---|
| Endpoint Engineering |  |  | ☐ |
| Business Owner |  |  | ☐ |
| Security (if applicable) |  |  | ☐ |

---

## Packaging Outcome

| Outcome | Selection |
---|---|
| Approved for Pilot Deployment | ☐ |
| Approved for Production Deployment | ☐ |
| Approved (Post-ESP Only) | ☐ |
| Rejected | ☐ |

**Notes**
<enter final comments or conditions> ```

---

## Governance Notes

This checklist must be completed for every version of an application

Failure of any mandatory check requires remediation before deployment

This document may be requested during audits or incident investigations

Checklists must be retained for the full lifecycle of the application

---

## Status

☐ Checklist Complete

☐ Approved

☐ Archived (Application Retired)


---

### Template Status

- ✔ Production-ready  
- ✔ ESP-aware  
- ✔ Audit-defensible  
- ✔ Change-management aligned  

