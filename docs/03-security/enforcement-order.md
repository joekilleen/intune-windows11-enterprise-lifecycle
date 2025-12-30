# Security Control Enforcement Order  
**Deterministic Application and Fail-Closed Behavior**

---

## Purpose

This document defines the **authoritative enforcement order** for all endpoint security controls applied to Windows 11 devices.

The enforcement order is critical to ensure:
- Deterministic security posture
- Predictable compliance outcomes
- Clear troubleshooting paths
- Audit defensibility

Controls applied out of order increase risk, create false compliance signals, and complicate recovery.

---

## Enforcement Design Principles

1. **Identity precedes device access**
2. **Baseline before specialization**
3. **Preventive controls before detective controls**
4. **Encryption before access**
5. **Compliance before productivity**
6. **Recovery rebuilds, not repairs**

---

## High-Level Enforcement Sequence

The following order is **non-negotiable** for production devices:

1. Identity establishment
2. Device enrollment
3. Baseline hardening
4. Preventive security controls
5. Compliance evaluation
6. Access enforcement
7. Ongoing monitoring
8. Lifecycle operations

---

## Detailed Enforcement Order

### Step 1 — Identity Establishment

**Controls**
- User authentication via Entra ID
- Device identity creation
- Certificate and trust establishment

**Outcome**
- Device is uniquely identified
- User identity verified

**Failure Result**
- Enrollment cannot proceed

---

### Step 2 — Device Enrollment (Autopilot + MDM)

**Controls**
- Windows Autopilot
- Entra ID Join
- Intune MDM enrollment

**Outcome**
- Device becomes managed
- Intune is authoritative

**Failure Result**
- Device blocked at OOBE

---

### Step 3 — Enrollment Status Page (ESP)

**Controls**
- Blocking ESP
- Required policy and app enforcement

**Outcome**
- Device prevented from use until secure

**Failure Result**
- Enrollment failure; reset required

---

### Step 4 — Security Baseline Application

**Controls**
- Windows 11 Security Baseline
- OS, credential, and kernel hardening

**Outcome**
- Minimum security posture established

**Failure Result**
- Device marked non-compliant

---

### Step 5 — Preventive Security Controls

**Controls**
- BitLocker disk encryption
- Microsoft Defender Antivirus
- Defender for Endpoint (EDR)
- Attack Surface Reduction (ASR)
- Windows Defender Firewall

**Outcome**
- Device protected against common attack vectors

**Failure Result**
- Device remains non-compliant
- Access blocked

---

### Step 6 — Compliance Evaluation

**Controls**
- Intune compliance policies
- Continuous signal evaluation

**Signals Evaluated**
- Encryption status
- Secure Boot and TPM
- Defender health
- OS version
- Firewall state

**Outcome**
- Compliance state published to Entra ID

---

### Step 7 — Conditional Access Enforcement

**Controls**
- Conditional Access policies
- Require compliant device

**Outcome**
- Access granted only to compliant devices

**Failure Result**
- Access denied to corporate resources

---

### Step 8 — Application Enablement

**Controls**
- Required apps (post-ESP)
- Available apps via Company Portal
- Supersedence and version control

**Outcome**
- Productivity enabled on secure foundation

---

### Step 9 — Updates and Servicing

**Controls**
- Windows Update for Business rings
- Feature update targeting
- Driver and firmware governance

**Outcome**
- Security patches applied predictably

---

### Step 10 — Monitoring and Operations

**Controls**
- Endpoint Analytics
- Intune reporting
- Defender telemetry

**Outcome**
- Continuous visibility and evidence

---

### Step 11 — Lifecycle Operations

**Controls**
- Autopilot Reset
- Wipe
- Decommissioning workflows

**Outcome**
- Secure reassignment or destruction

---

## Enforcement Dependencies Matrix

| Control | Depends On |
---|---|
| ESP | Enrollment |
| BitLocker | Security baseline |
| Defender | Baseline + network |
| ASR | Defender AV |
| Firewall | Baseline |
| Compliance | All preventive controls |
| Conditional Access | Compliance |

---

## Failure and Recovery Philosophy

### Fail-Closed Model

- Failures block access
- Devices do not enter production partially secured
- Manual overrides are prohibited

### Recovery Model

| Failure Type | Recovery |
---|---|
| Enrollment failure | Autopilot Reset |
| Security failure | Reset or wipe |
| Compliance failure | Automated remediation |
| Suspected compromise | Wipe + re-enroll |

---

## Troubleshooting Guidance

When troubleshooting:
1. Identify the **earliest failed step**
2. Do not bypass earlier controls
3. Rebuild rather than repair
4. Validate enforcement order after recovery

---

## Evidence and Audit Alignment

Auditors should be able to verify:
- Order of control application
- Dependency enforcement
- Failure handling consistency
- Evidence retention

Relevant evidence sources:
- Intune device timelines
- Compliance reports
- Entra ID sign-in logs
- Defender telemetry

---

## Summary

Security effectiveness depends not just on **which controls exist**, but **when and how they are enforced**.

This enforcement order ensures:
- Predictable security posture
- Clear ownership of failures
- Strong audit defensibility
- Reduced operational ambiguity

Deviation from this order introduces risk and is not permitted without formal exception.

---

## Next Section

Proceed to:

**`docs/04-compliance-and-access/10-compliance-policies.md`**

This file defines the **exact compliance signals and remediation logic** used for Conditional Access enforcement.
