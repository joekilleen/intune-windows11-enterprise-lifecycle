# Sample Audit Requests  
**Compliance, Conditional Access, and Remediation Evidence**

---

## Purpose

This document provides **representative audit request scenarios** and the **expected evidence responses** for Windows 11 device compliance and access enforcement.

It is intended to:
- Reduce audit friction
- Standardize responses across teams
- Demonstrate mature, repeatable controls
- Align technical evidence with audit language

All examples assume **production enforcement** and **fail-closed behavior**.

---

## How to Use This Document

- Auditors may submit requests similar to those below
- Engineering and security teams should respond using the mapped evidence
- Responses should reference **system-generated artifacts**, not narrative assurances

If a requested artifact cannot be produced, the control should be considered **ineffective**.

---

## Audit Request 1 — Device Compliance Enforcement

### Sample Auditor Request

> Demonstrate how the organization ensures that only compliant Windows devices can access corporate cloud resources.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Compliance policy configuration | Intune |
| Compliance state for sample devices | Intune |
| Conditional Access policy requiring compliant device | Entra ID |
| Sign-in logs showing blocked access from non-compliant device | Entra ID |

---

### Auditor Validation Focus

- Compliance criteria are explicit
- Compliance state is evaluated continuously
- Access is denied when devices are non-compliant

---

## Audit Request 2 — Non-Compliance Grace Periods

### Sample Auditor Request

> Describe and demonstrate any grace periods applied to non-compliant devices and how enforcement occurs after expiration.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Grace period configuration | Intune compliance policy |
| Device compliance timeline | Intune device record |
| Sign-in logs before grace expiration | Entra ID |
| Sign-in logs after grace expiration (blocked) | Entra ID |

---

### Auditor Validation Focus

- Grace periods are time-bound
- Enforcement occurs automatically after expiration
- No manual overrides are required

---

## Audit Request 3 — Conditional Access Policy Effectiveness

### Sample Auditor Request

> Provide evidence that Conditional Access policies are actively enforcing security requirements for Windows devices.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Conditional Access policy definitions | Entra ID |
| Policy evaluation results | Entra ID sign-in logs |
| Blocked sign-in events | Entra ID |
| Policy change history | Entra ID audit logs |

---

### Auditor Validation Focus

- Policies are enabled
- Policies apply broadly (not over-excluded)
- Enforcement outcomes are visible in logs

---

## Audit Request 4 — Handling of Non-Remediable Devices

### Sample Auditor Request

> Explain how devices that cannot meet security requirements are handled and removed from production.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Non-compliance reason (e.g., TPM failure) | Intune |
| Access block event | Entra ID |
| Wipe or reset action | Intune audit logs |
| Post-wipe device state | Intune |

---

### Auditor Validation Focus

- Devices are not left in limbo
- Access is blocked before remediation
- Rebuild or removal is decisive shows data protection

---

## Audit Request 5 — Suspected Device Compromise

### Sample Auditor Request

> Demonstrate how the organization responds to a suspected endpoint compromise.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Defender alert details | Defender portal |
| Device isolation or containment action | Defender portal |
| Access denial following risk signal | Entra ID |
| Wipe confirmation | Intune |
| Post-remediation enrollment record | Intune |

---

### Auditor Validation Focus

- Detection is timely
- Response is automated where possible
- Compromised devices do not retain access

---

## Audit Request 6 — Exception Management

### Sample Auditor Request

> Identify any exceptions to compliance or Conditional Access policies and explain how they are governed.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| List of excluded devices or users | Intune / Entra ID |
| Business justification | Change record |
| Approval documentation | Governance records |
| Expiration or review date | Change record |

---

### Auditor Validation Focus

- Exceptions are rare
- Exceptions are documented
- Exceptions are time-bound and reviewed

---

## Audit Request 7 — Evidence Retention and Integrity

### Sample Auditor Request

> Describe how compliance and access enforcement evidence is retained and protected from tampering.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Log retention settings | Entra ID / Intune |
| Exported sample reports | Intune / Entra ID |
| Role-based access controls | Entra ID RBAC |
| Audit trail for policy changes | Entra ID audit logs |

---

### Auditor Validation Focus

- Evidence is retained for defined periods
- Access to evidence is restricted
- Evidence is system-generated

---

## Audit Request 8 — Repeat Offender Analysis

### Sample Auditor Request

> Provide insight into devices that meansure repeatedly fail compliance and how this risk is addressed.

---

### Expected Evidence Response

| Evidence | Source |
---|---|
| Historical compliance reports | Intune |
| Device timelines | Intune |
| Remediation actions taken | Intune audit logs |
| Device replacement or decommissioning records | Asset management |

---

### Auditor Validation Focus

- Patterns are identified
- Root causes are addressed
- Risk is reduced over time

---

## Common Audit Red Flags (Avoid These)

| Red Flag | Why It Fails |
---|---|
| “Policy exists” without enforcement proof | No operational evidence |
| Screenshots without logs | Not authoritative |
| Manual approval claims | Not scalable or provable |
| Broad Conditional Access exclusions | Weak control |
| No remediation evidence | Incomplete lifecycle |

---

## Summary

These sample audit requests demonstrate that:

- Compliance is **measured**
- Enforcement is **automatic**
- Access decisions are **logged**
- Failures are **contained**
- Recovery is **decisive**

Well-prepared organizations do not scramble for evidence — they **already have it**.

---

## Section Completion

With this document, **Section 4 — Compliance & Conditional Access** includes:
- Control definitions
- Enforcement logic
- Remediation workflows
- Evidence requirements
- Audit-ready request handling

---

## Next Section

Proceed to:

➡ **`docs/05-applications/12-application-lifecycle-architecture.md`**

This section defines **Win32 application lifecycle management for Windows 11 endpoints**.
