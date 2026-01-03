# CIS, NIST, and ISO Control Crosswalk  
**Endpoint Security Controls Mapped to Recognized Frameworks**

---

## Purpose

This document provides a **formal compliance crosswalk** mapping the technical and operational controls implemented in this Windows 11 Intune Enterprise Device Lifecycle architecture to:

- CIS Controls v8
- NIST SP 800-53 Rev. 5
- ISO/IEC 27001:2022

The objective is to:
- Demonstrate control coverage
- Support audit and regulatory inquiries
- Enable client and executive assurance
- Reduce duplication in compliance efforts
- Translate technical controls into governance language

This document does **not** replace formal certification or attestation.  
It provides **evidence-aligned traceability**.

---

## Scope and Assumptions

### In Scope

- Corporate-owned Windows 11 endpoints
- Microsoft Intune–managed devices
- Microsoft Entra ID–based identity and access control
- Microsoft Defender for Endpoint integration
- Conditional Access enforcement
- Centralized monitoring and evidence retention

### Out of Scope

- Non-Windows platforms
- BYOD/mobile-only compliance
- Third-party EDR or MDM tools
- Physical security controls

---

## Control Mapping Methodology

Each framework control is mapped to:

- **Implemented Control** – What is actually enforced
- **Mechanism** – How it is enforced (policy, configuration, process)
- **Evidence** – What can be produced during an audit
- **Coverage Status** – Full / Partial / Supporting

Mappings reflect **operational reality**, not aspirational policy.

---

## CIS Controls v8 Crosswalk

| CIS Control | Description | Implemented Control | Evidence |
---|---|---|---|
| 1 | Inventory and Control of Enterprise Assets | Intune device inventory, Autopilot registration | Intune device reports |
| 2 | Inventory and Control of Software Assets | Intune application inventory | App deployment reports |
| 3 | Data Protection | BitLocker, device wipe, reset runbooks | Encryption status, wipe logs |
| 4 | Secure Configuration of Enterprise Assets | Security baselines, configuration profiles | Profile assignments |
| 5 | Account Management | Entra ID RBAC, PIM, access reviews | Role assignments, PIM logs |
| 6 | Access Control Management | Conditional Access with device compliance | CA policy logs |
| 7 | Continuous Vulnerability Management | Update rings, feature update policies | Update compliance reports |
| 8 | Audit Log Management | Centralized audit logging, retention policy | Audit log exports |
| 10 | Malware Defenses | Defender for Endpoint | Defender alerts |
| 12 | Network Infrastructure Management | Device firewall, isolation controls | Policy assignments |
| 17 | Incident Response | IR runbooks, device isolation | Incident records |

**Coverage Status:**  
CIS v8 controls relevant to endpoint management are **fully or substantively covered**.

---

## NIST SP 800-53 Rev. 5 Crosswalk

### Access Control (AC)

| NIST Control | Implemented Control | Evidence |
---|---|---|
| AC-2 | Account management via Entra ID | Role assignments |
| AC-3 | Access enforcement via Conditional Access | CA sign-in logs |
| AC-6 | Least privilege via RBAC and scope tags | RBAC matrix |
| AC-7 | Failed login controls | Sign-in logs |

---

### Configuration Management (CM)

| NIST Control | Implemented Control | Evidence |
---|---|---|
| CM-2 | Baseline configuration enforcement | Intune profiles |
| CM-3 | Change control and promotion model | Decision log |
| CM-6 | Secure configuration settings | Security baselines |

---

### Identification and Authentication (IA)

| NIST Control | Implemented Control | Evidence |
---|---|---|
| IA-2 | MFA enforcement | Conditional Access policies |
| IA-5 | Credential management | Entra ID policies |

---

### Incident Response (IR)

| NIST Control | Implemented Control | Evidence |
---|---|---|
| IR-4 | Incident handling | IR runbooks |
| IR-6 | Incident reporting | Incident records |
| IR-8 | Incident response plan | IR documentation |

---

### System and Communications Protection (SC)

| NIST Control | Implemented Control | Evidence |
---|---|---|
| SC-7 | Boundary protection | Firewall policies |
| SC-12 | Cryptographic key management | BitLocker key handling |

**Coverage Status:**  
NIST SP 800-53 endpoint-related controls are **fully supported** through technical enforcement and documented process.

---

## ISO/IEC 27001:2022 Crosswalk

### Annex A Controls

| ISO Control | Description | Implemented Control | Evidence |
---|---|---|---|
| A.5.15 | Access control | RBAC, Conditional Access | Access review records |
| A.5.16 | Identity management | Entra ID, PIM | Role assignments |
| A.8.1 | Endpoint security | Intune device management | Device compliance reports |
| A.8.7 | Malware protection | Defender for Endpoint | Alert history |
| A.8.9 | Configuration management | Security baselines | Profile assignments |
| A.8.15 | Logging and monitoring | Centralized audit logs | Log exports |
| A.5.30 | ICT readiness for continuity | DR configuration backups | DR packages |

**Coverage Status:**  
ISO 27001 Annex A technical controls related to endpoint security are **operationally implemented**.

---

## Control Coverage Summary

| Framework | Coverage |
---|---|
| CIS v8 | High |
| NIST SP 800-53 | High |
| ISO/IEC 27001 | High |

Gaps outside scope are **explicit and intentional**, not accidental.

---

## Evidence Production Model

For any mapped control, the organization can produce:

- Policy configuration (Intune / Entra ID)
- Assignment and scope data
- Audit logs
- Operational runbooks
- Review and decision records

Evidence is:
- Timestamped
- Attributable
- Retained per policy

---

## Common Audit Questions (Answered)

**Q: How do you ensure devices remain compliant?**  
A: Continuous compliance evaluation with Conditional Access enforcement.

**Q: How is least privilege enforced?**  
A: RBAC + scope tags + PIM + access reviews.

**Q: How are incidents handled?**  
A: Documented IR runbooks with Defender isolation and evidence retention.

**Q: How do you prove controls operate continuously?**  
A: Monitoring dashboards, reports, and retained logs.

---

## Limitations and Disclaimers

- This crosswalk does not constitute certification.
- Regulatory attestation requires independent assessment.
- Control effectiveness depends on continuous operation.

This document supports **audit readiness**, not regulatory substitution.

---

## Change Control

Updates to this crosswalk:
- Must align with architecture changes
- Require security and GRC approval
- Must be versioned and retained
- Must reference updated evidence sources

---

## Summary

This crosswalk demonstrates that the Intune Windows 11 Enterprise Device Lifecycle architecture:

- Aligns with recognized security frameworks
- Implements enforceable technical controls
- Produces defensible audit evidence
- Supports enterprise and regulated environments

Compliance is **designed in**, not retrofitted.

---

## Section Completion

With this document, **Section 11 — Compliance Mapping** is **complete**.

---


