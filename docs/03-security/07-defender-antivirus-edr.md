# Microsoft Defender Antivirus & Endpoint Detection and Response (EDR)  
**Malware Protection, Threat Detection, and Response**

---

## Purpose

This document defines the **authoritative malware protection and endpoint detection and response (EDR) architecture** for Windows 11 devices.

Microsoft Defender Antivirus and Defender for Endpoint are mandatory controls that provide:
- Real-time malware prevention
- Behavioral threat detection
- Post-breach visibility and response
- Continuous security telemetry for enforcement and audit

Devices not onboarded to Defender for Endpoint **must not** be considered trusted.

---

## Protection Objectives

The Defender implementation must ensure:

1. **Always-on real-time protection**
2. **Cloud-assisted threat intelligence**
3. **Tamper-resistant configuration**
4. **Centralized visibility and response**
5. **Compliance signaling for access control**

---

## Prerequisites (Mandatory)

| Requirement | State |
---|---|
| OS | Windows 11 Enterprise |
| Security Baseline | Applied successfully |
| Network Access | Internet access for cloud protection |
| User Privilege | Standard user |
| Third-Party AV | Not installed |

**Constraint**  
Third-party antivirus solutions are not supported in this architecture.

---

## Defender Antivirus Configuration

### Policy Deployment  
**Exact UI Click-Path**

### Intune admin center
→ Endpoint security
→ Antivirus
→ Create policy
→ Microsoft Defender Antivirus

---


---

### Defender AV Policy Configuration  
**Field-by-Field (Authoritative Baseline)**

#### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | SEC-W11-DefenderAV-Prod | Deterministic naming |
| Description | Defender Antivirus baseline policy | Audit clarity |

---

#### Real-Time Protection

| Setting | Value | Rationale |
---|---|---|
| Real-time protection | Enabled | Core protection |
| Behavior monitoring | Enabled | Behavioral detection |
| Cloud-delivered protection | Enabled | Threat intelligence |
| Sample submission | Automatic | Detection accuracy |

---

#### Scan Configuration

| Setting | Value | Rationale |
---|---|---|
| Scheduled scan | Enabled | Hygiene |
| Scan type | Quick scan | Performance balance |
| Scan day | Daily | Continuous coverage |
| Scan time | Off-hours | Minimal disruption |

---

#### Threat Response

| Setting | Value | Rationale |
---|---|---|
| Threat actions | Automatic remediation | Speed |
| PUAs | Block | Reduce risk |
| Exclusions | Minimal and documented | Risk control |

---

#### Tamper Protection

| Setting | Value | Rationale |
---|---|---|
| Tamper protection | Enabled | Prevent bypass |

---

## Defender for Endpoint (EDR) Onboarding

### EDR Purpose

Defender for Endpoint extends antivirus with:
- Behavioral analytics
- Incident correlation
- Automated investigation
- Threat and vulnerability management (TVM)

---

### EDR Onboarding Policy  
**Exact UI Click-Path**

### Intune admin center
→ Endpoint security
→ Microsoft Defender for Endpoint
→ Open the Microsoft Defender Security Center

---


**Note**  
EDR onboarding is enforced via Intune and completed in the Defender portal.

---

### EDR Configuration Requirements

| Setting | Required State |
---|---|
| EDR Sensor | Onboarded |
| Automatic investigation | Enabled |
| Response actions | Allowed |
| Tamper protection | Enabled |

---

## Enforcement Order

1. Security baseline applies
2. Defender AV policy applies
3. Tamper protection enabled
4. EDR sensor onboarded
5. Device begins reporting telemetry
6. Compliance evaluation updated

---

## Compliance Signals

| Signal | Expected State |
---|---|
| Defender AV | Enabled |
| Real-time protection | On |
| Tamper protection | On |
| EDR status | Onboarded |
| Threat status | No active high-risk alerts |

Devices failing any signal are marked **non-compliant**.

---

## Operational Response Model

| Event | Action |
---|---|
| Malware detected | Automatic remediation |
| High-severity alert | SOC investigation |
| Persistent threat | Device isolation |
| Compromise suspected | Wipe and re-enroll |

**Rule**  
Manual remediation on compromised devices is prohibited.

---

## Failure Modes and Remediation

| Failure | Cause | Resolution |
---|---|---|
| Defender disabled | Tamper protection off | Reapply policy |
| EDR not reporting | Onboarding failure | Reassign policy |
| Excessive exclusions | Poor governance | Remove exclusions |
| Performance issues | Over-scanning | Adjust scan schedule |

---

## Validation Checklist

- [ ] Defender Antivirus enabled
- [ ] Real-time protection active
- [ ] Tamper protection enabled
- [ ] Device onboarded to EDR
- [ ] Device visible in Defender portal
- [ ] No conflicting AV present

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| AV policy configuration | Intune |
| EDR onboarding status | Defender portal |
| Threat alerts | Defender portal |
| Compliance state | Intune compliance reports |

---

## Change Control

Defender configuration changes:
- Require security team approval
- Must be tested in Pilot
- Must be documented in the Decision Log
- Must not reduce protection coverage

---

## Summary

Microsoft Defender provides **continuous protection before, during, and after compromise**.  
It is a cornerstone of Zero Trust enforcement and operational visibility.

A device without Defender is **not secure**.

---

## Next File

Proceed to:

**`docs/03-security/08-asr-rules.md`**

This file defines **Attack Surface Reduction (ASR) rule enforcement and tuning**.

