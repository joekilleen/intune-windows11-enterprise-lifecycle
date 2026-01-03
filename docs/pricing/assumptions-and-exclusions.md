# Assumptions and Exclusions  
**Windows 11 Enterprise Device Lifecycle Implementation (Microsoft Intune)**

---

## 1. Purpose

This document defines the **explicit assumptions and exclusions** governing the Windows 11 Enterprise Device Lifecycle engagement delivered under the associated Statement of Work (“SOW”).

Its purpose is to:
- Establish clear delivery boundaries
- Prevent scope ambiguity
- Protect both Client and Provider from misaligned expectations
- Serve as a reference during change control, acceptance, and dispute resolution

Anything not explicitly included is **assumed excluded**.

---

## 2. Core Delivery Assumptions

The engagement pricing, timeline, and delivery model assume the following conditions are met.

### 2.1 Tenant and Platform Assumptions

- Client operates a **Microsoft Entra ID tenant** in commercial cloud
- Client uses **Microsoft Intune** as the primary endpoint management platform
- Windows endpoints are **Windows 11**, corporate-owned
- Tenant is not in a degraded or unsupported state
- No active tenant-wide security incident at project start

---

### 2.2 Licensing Assumptions

- Client provides and maintains all required Microsoft licenses
- Licensing includes Intune, Entra ID P1/P2 (as required), and Defender for Endpoint
- Licensing sufficiency is validated by Client, not Provider
- Licensing changes during delivery may require scope adjustment

---

### 2.3 Device Assumptions

- Devices are corporate-owned (no BYOD)
- Devices support Windows Autopilot
- Device firmware supports Secure Boot and TPM
- No legacy OS remediation is required
- Hardware refresh is not part of this engagement

---

### 2.4 Organizational Assumptions

- Client assigns a single technical point of contact
- Client provides timely feedback and approvals
- Client participates in design and validation reviews
- Business requirements are stable during delivery
- Executive sponsor is available for escalation

---

### 2.5 Access Assumptions

- Provider receives least-privilege access required for delivery
- Access is provisioned within agreed timelines
- Provider will not retain access post-engagement
- Delays in access provisioning may impact delivery schedule

---

## 3. Operational Assumptions

- Engagement is **design and implementation-focused**, not managed services
- Ongoing operations are the Client’s responsibility post-handoff
- Client teams will operate runbooks provided
- Provider is not responsible for day-to-day endpoint support

---

## 4. Explicit Exclusions

The following items are **explicitly excluded** from this engagement unless added via a written change request.

### 4.1 Technical Exclusions

- Non-Windows platforms (macOS, Linux, iOS, Android)
- Third-party MDM or EDR tools
- Custom PowerShell scripting beyond documented examples
- Application development or code modification
- Application packaging beyond agreed limits
- Legacy OS remediation (Windows 10 or earlier)
- Hardware procurement or replacement

---

### 4.2 Security and Compliance Exclusions

- Regulatory certification or attestation (ISO, SOC, FedRAMP, etc.)
- Penetration testing or red team exercises
- Incident response outside documented runbooks
- Historical forensic investigations
- Legal discovery or eDiscovery support

---

### 4.3 Operational and Support Exclusions

- End-user training beyond IT administrators
- Help desk or managed services
- 24x7 support or on-call coverage
- Post-engagement operational tuning
- SLA-backed support commitments

---

### 4.4 Commercial Exclusions

- Travel or on-site work (unless separately agreed)
- Expenses not explicitly approved in writing
- Licensing costs
- Third-party vendor fees

---

## 5. Impact of Assumption Changes

If any assumption becomes invalid during delivery:

- Provider will notify Client
- Impact will be assessed (scope, timeline, pricing)
- A Change Request may be required
- No out-of-scope work will proceed without approval

---

## 6. Change Control Reference

All changes to assumptions or exclusions are governed by:

- Change Request Template
- Statement of Work
- Master Services Agreement

Verbal agreements are **not binding**.

---

## 7. Risk Allocation

- Provider is responsible for delivery within agreed scope
- Client is responsible for environment readiness and licensing
- Shared risks require explicit, documented acceptance
- Undisclosed constraints may invalidate pricing assumptions

---

## 8. Audit and Legal Use

This document may be used:
- During procurement review
- During legal interpretation of scope
- During audit inquiries
- During dispute resolution

Clarity in assumptions protects **both parties**.

---

## 9. Summary

These assumptions and exclusions:
- Define clear delivery boundaries
- Enable fixed-fee predictability
- Reduce ambiguity and risk
- Support smooth acceptance and closure

Anything not clearly included is **intentionally excluded**.

---

## Document Status

- ☐ Draft
- ☐ Approved
- ☐ In Effect
- ☐ Reviewed (Annual)

---
