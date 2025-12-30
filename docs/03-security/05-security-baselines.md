# Security Baselines  
**Windows 11 Endpoint Hardening Foundation**

---

## Purpose

This document defines the **authoritative security baseline strategy** for Windows 11 endpoints managed through Microsoft Intune.

Security baselines establish the **minimum acceptable security posture** for all devices and serve as the foundation upon which:
- Compliance policies
- Conditional Access enforcement
- Threat detection
- Audit evidence

are built.

Security baselines are **mandatory** and **non-negotiable** for production devices.

---

## Baseline Design Principles

Security baselines are implemented according to the following principles:

1. **Microsoft-Recommended First**
   - Leverage Microsoft-provided Windows security baselines.
2. **Consistency Over Customization**
   - Deviations require documented justification.
3. **Fail Closed**
   - Devices that cannot apply the baseline are blocked.
4. **Policy-Driven**
   - No manual or ad-hoc configuration.
5. **Audit-Ready**
   - Every setting maps to a measurable state.

---

## Baseline Scope

| Scope | Included |
|---|---|
| OS Hardening | Yes |
| Credential Protection | Yes |
| Network Security | Yes |
| Local Security Policies | Yes |
| Legacy Compatibility Tweaks | No |
| User Preferences | No |

---

## Baseline Source

### Approved Baseline

- **Windows 11 Security Baseline (Microsoft)**

**Rationale**
- Aligns with current Microsoft threat intelligence
- Regularly updated
- Recognized by auditors

---

## Baseline Deployment  
**Exact UI Click-Path**

## Intune admin center
→ Endpoint security
→ Security baselines
→ Windows 11 Security Baseline
→ Create profile


---

## Baseline Profile Configuration

### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | SEC-W11-Baseline-Prod | Deterministic naming |
| Description | Windows 11 enterprise security baseline | Audit clarity |
| Platform | Windows 10 and later | Applies to Windows 11 |

---

## Core Security Domains Enforced

### Account & Credential Security

| Control | Outcome |
---|---|
| Credential Guard | Enabled |
| LSASS Protection | Enabled |
| NTLM Restrictions | Enforced |
| SMB Signing | Required |

---

### OS and Kernel Protections

| Control | Outcome |
---|---|
| Secure Boot | Required |
| Virtualization-Based Security (VBS) | Enabled |
| Hypervisor-Protected Code Integrity (HVCI) | Enabled |
| Driver Signature Enforcement | Required |

---

### Attack Surface Reduction (Baseline Layer)

| Control | Outcome |
---|---|
| Office macro abuse protections | Enforced |
| Script abuse mitigations | Enforced |
| Process injection protections | Enforced |

> Fine-grained ASR tuning is defined separately in `08-asr-rules.md`.

---

### Network Security

| Control | Outcome |
---|---|
| Windows Defender Firewall | Enabled |
| Inbound default | Block |
| Outbound default | Allow (restricted by ASR) |

---

### Local Security Policies

| Control | Outcome |
---|---|
| Local admin restrictions | Enforced |
| Password policies | Enforced |
| Guest account | Disabled |

---

## Assignment Strategy

| Target | Method |
---|---|
| Production Devices | Dynamic device group |
| Pilot Devices | Separate pilot baseline |
| Exclusions | Break-glass devices only (rare) |

**Rule**
- Baselines are assigned to **devices**, not users.

---

## Baseline Versioning and Promotion

### Promotion Model

1. New baseline version assigned to Pilot group
2. Validation period (minimum 7–14 days)
3. Approval
4. Promotion to Production
5. Old baseline retired

**Editing baselines in place in production is prohibited.**

---

## Interaction with Other Security Policies

| Policy Type | Relationship |
---|---|
| BitLocker | Complementary |
| Defender AV | Complementary |
| ASR | Extends baseline |
| Firewall | Reinforces baseline |
| Compliance Policies | Measure baseline success |

---

## Failure Conditions

A device is considered **failed** if:
- Baseline cannot apply
- Secure Boot or VBS fails
- Credential protections fail
- Required services are disabled

**Failure Outcome**
- Device becomes non-compliant
- Conditional Access blocks access
- Device must be remediated or wiped

---

## Validation Checklist

- [ ] Baseline applied successfully
- [ ] No conflicting policies
- [ ] Secure Boot enabled
- [ ] VBS and HVCI enabled
- [ ] Firewall active
- [ ] Device reports compliant

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| Baseline configuration | Intune |
| Device status | Intune device report |
| Compliance status | Compliance report |
| Defender posture | Defender portal |

---

## Change Control

Security baseline changes:
- Require security review
- Must be validated in Pilot
- Must be logged in the Decision Log
- Must include rollback strategy

---

## Summary

Security baselines provide the **bedrock** of endpoint security.  
All other protections **assume** this baseline is correctly and consistently applied.

A device without a baseline is **not trusted**.

---

## Next File

Proceed to:

➡ **`docs/03-security/06-bitlocker-disk-encryption.md`**

This file defines **mandatory encryption enforcement and key management**.

**Exact UI Click-Path**

