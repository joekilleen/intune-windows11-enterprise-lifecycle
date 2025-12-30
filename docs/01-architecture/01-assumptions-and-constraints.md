# Assumptions and Design Constraints  
**Windows 11 Intune Enterprise Device Lifecycle**

---

## Purpose of This Document

This document defines the **explicit assumptions** and **hard design constraints** governing the Windows 11 enterprise device lifecycle described in this repository.

These assumptions are intentional. They exist to ensure:
- Predictable outcomes
- Strong security posture
- Audit defensibility
- Operational scalability
- Clear accountability

Any deviation from these assumptions **must be documented as an exception** and approved through formal change management.

---

## Architectural Scope

### In Scope
- Corporate-owned Windows 11 endpoints
- Cloud-native identity and device management
- Zero-touch provisioning and lifecycle operations
- Security-first, compliance-enforced access

### Out of Scope
- Server workloads
- Non-Windows endpoints (unless explicitly extended)
- Legacy imaging or domain-based management
- Consumer/BYOD device models

---

## Organizational Assumptions

| Area | Assumption |
|---|---|
| Organization Size | Mid-market to large enterprise (≈500–50,000 devices) |
| Operating Model | Centralized IT with delegated regional support |
| Workforce | Hybrid and/or remote-first |
| Security Posture | Zero Trust aligned |
| Compliance | Subject to internal or external audits |
| Procurement | Standardized hardware models |

---

## Identity and Access Assumptions

| Area | Assumption |
|---|---|
| Identity Provider | Microsoft Entra ID is authoritative |
| Authentication | Modern authentication only |
| Legacy Protocols | Disabled or blocked |
| MFA | Enforced for all users; mandatory for admins |
| Device Trust | Required for application access |
| Privileged Access | No standing administrative rights |

**Rationale**  
Identity is the primary control plane. Device and user trust must be verifiable before access is granted.

---

## Device Management Assumptions

| Area | Assumption |
|---|---|
| MDM Authority | Microsoft Intune |
| Join Model | Entra ID Join only |
| Enrollment Method | Windows Autopilot |
| Ownership | Corporate-owned |
| Co-Management | Not used |
| Manual Builds | Prohibited |

**Explicit Exclusions**
- Hybrid Entra ID Join (unless approved exception)
- Configuration Manager (SCCM)
- MDT or image-based provisioning

---

## Hardware and OEM Constraints

| Constraint | Requirement |
|---|---|
| Operating System | Windows 11 Enterprise |
| TPM | TPM 2.0 required |
| Secure Boot | Enabled |
| Firmware | UEFI only |
| OEM Registration | Autopilot hardware hash pre-registered |
| Lifecycle | 3–4 year refresh cycle |

**Rationale**  
Hardware-rooted trust is mandatory for silent encryption, compliance signaling, and secure provisioning.

---

## Security Constraints (Non-Negotiable)

| Domain | Constraint |
|---|---|
| Encryption | BitLocker enforced on OS drive |
| Key Management | Recovery keys escrowed |
| Malware Protection | Microsoft Defender required |
| EDR | Defender for Endpoint onboarded |
| Firewall | Enabled on all profiles |
| ASR | Attack surface reduction enforced |
| Secure Boot | Required and monitored |

**Failure Mode**  
A device that cannot meet security prerequisites **must not** access corporate resources.

---

## Compliance and Access Constraints

| Area | Constraint |
|---|---|
| Compliance Evaluation | Continuous |
| Access Enforcement | Conditional Access |
| Non-Compliance | Results in access denial |
| Grace Periods | Limited and time-bound |
| Exceptions | Rare, documented, reviewed |

**Design Rule**  
Compliance without enforcement is informational only and therefore insufficient.

---

## Configuration Management Constraints

| Area | Constraint |
|---|---|
| Configuration Method | Policy-driven (CSP-based) |
| Baselines | Microsoft security baselines |
| Scripts | Limited to remediation only |
| Drift | Automatically remediated |
| Change Control | Required for production |

**Anti-Patterns Prohibited**
- Manual local configuration
- Untracked registry changes
- Ad-hoc scripting without governance

---

## Application Lifecycle Constraints

| Area | Constraint |
|---|---|
| App Type | Win32 for LOB apps |
| Install Context | System |
| Detection | Deterministic and version-aware |
| Dependencies | Explicitly declared |
| Version Control | Supersedence required |
| ESP Safety | Required apps must be ESP-safe |

---

## Update and Servicing Constraints

| Area | Constraint |
|---|---|
| Update Control | Windows Update for Business |
| Deployment Model | Ring-based |
| Feature Updates | Explicitly targeted |
| Driver Updates | Governed and approved |
| User Deferrals | Limited |
| Restart Enforcement | Mandatory deadlines |

---

## Operational Constraints

| Area | Constraint |
|---|---|
| Tier-1 Support | No admin access |
| Recovery | Reset or wipe only |
| Repair-in-Place | Prohibited |
| Monitoring | Mandatory |
| Evidence | Retained and exportable |

---

## Governance Constraints

| Area | Constraint |
|---|---|
| RBAC | Least privilege |
| Scope Tags | Mandatory |
| Separation of Duties | Enforced |
| Privileged Access | Time-bound (PIM) |
| Change Approval | Required for production |

---

## Decommissioning and Data Protection Constraints

| Area | Constraint |
|---|---|
| Data Destruction | Cryptographic wipe |
| Autopilot Records | Deregistered |
| Device Records | Removed post-wipe |
| Evidence | Logged and retained |

**Failure Condition**  
A device is not considered decommissioned until wipe confirmation is recorded.

---

## Certification and Review Alignment

These assumptions align with:
- MD-102 (Endpoint Administrator)
- AZ-104 (Identity and access adjacency)
- Enterprise audit expectations (CIS, NIST, ISO)

---

## Summary

These assumptions and constraints define a **controlled, secure, and auditable operating environment**. They intentionally favor:

- Security over convenience
- Automation over manual effort
- Evidence over intuition

All subsequent architecture, policy, and operational guidance **derives from this document**.

---

## Change Control

Any exception to these assumptions requires:
- Documented rationale
- Risk acceptance
- Time-bound approval
- Inclusion in the Architecture Decision Log

Refer to:
- `docs/00-overview/02-decision-log.md`
- `docs/09-governance/27-change-management.md`

---
