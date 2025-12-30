# BitLocker Disk Encryption  
**Mandatory Data-at-Rest Protection**

---

## Purpose

This document defines the **authoritative BitLocker encryption architecture** for Windows 11 endpoints.

BitLocker is a **non-negotiable control** that provides:
- Cryptographic protection of data at rest
- Assurance of data destruction during wipe
- Compliance alignment with enterprise security standards

Devices that cannot encrypt **must not** access corporate resources.

---

## Encryption Objectives

The BitLocker implementation must ensure:

1. **Automatic, silent encryption**
2. **Hardware-backed key protection**
3. **Centralized recovery key escrow**
4. **Compliance signal generation**
5. **Verifiable destruction during decommissioning**

---

## Prerequisites (Mandatory)

| Requirement | State |
---|---|
| TPM | TPM 2.0 present and enabled |
| Secure Boot | Enabled |
| UEFI | Required |
| OS | Windows 11 Enterprise |
| Local Admin | Not required for encryption |

Failure to meet prerequisites results in **enrollment failure or non-compliance**.

---

## Encryption Standard (Authoritative)

| Setting | Value | Rationale |
---|---|---|
| Encryption method | XTS-AES-256 | Enterprise-grade |
| OS drive encryption | Required | Data protection |
| Fixed drives | Required | Secondary disks |
| Removable drives | Optional (policy-driven) | Risk-based |

---

## BitLocker Policy Deployment  
**Exact UI Click-Path**

## Intune admin center
→ Endpoint security
→ Disk encryption
→ Create policy
→ Windows 10 and later

---


---

## BitLocker Policy Configuration  
**Field-by-Field (Authoritative Baseline)**

### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | SEC-W11-BitLocker-Prod | Deterministic naming |
| Description | Mandatory BitLocker encryption | Audit clarity |

---

### OS Drive Settings

| Setting | Value | Rationale |
---|---|---|
| Require BitLocker | Yes | Mandatory |
| Encryption method | XTS-AES-256 | Strong encryption |
| TPM required | Yes | Hardware-backed |
| Allow standard users to enable encryption | Yes | Silent enablement |
| Startup authentication | TPM only | User transparency |

---

### Recovery Key Management

| Setting | Value | Rationale |
---|---|---|
| Store recovery keys | Microsoft Entra ID | Central escrow |
| Rotate recovery key | On use | Reduce exposure |
| Hide recovery options | Yes | Prevent misuse |

---

### Fixed Data Drives

| Setting | Value | Rationale |
---|---|---|
| Require encryption | Yes | Data protection |
| Encryption method | XTS-AES-256 | Consistency |
| Auto-unlock | Allowed | Usability |

---

### Removable Data Drives (Optional)

| Setting | Value | Rationale |
---|---|---|
| Control use | Optional / Restricted | Risk-based |
| Encryption required | Optional | Business decision |

---

## Enforcement Order

1. Security baseline applied
2. BitLocker policy applied
3. Encryption initiates silently
4. Recovery key escrowed
5. Compliance signal updated

**User interaction is not permitted or required.**

---

## Compliance Evaluation

| Signal | Expected State |
---|---|
| Encryption | Enabled |
| Recovery key | Escrowed |
| Encryption strength | XTS-AES-256 |
| Protection status | On |

Devices failing any signal become **non-compliant**.

---

## Failure Modes and Remediation

| Failure | Cause | Resolution |
---|---|---|
| Encryption does not start | TPM not ready | Verify firmware/BIOS |
| Recovery key missing | Policy misapplied | Reassign policy |
| User prompted | Startup auth misconfigured | Enforce TPM-only |
| Device non-compliant | Encryption failed | Reset or wipe |

Manual remediation on the device is prohibited.

---

## Validation Checklist

- [ ] BitLocker enabled on OS drive
- [ ] Encryption method is XTS-AES-256
- [ ] Recovery key visible in Entra ID
- [ ] No user prompts during encryption
- [ ] Device marked compliant

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| BitLocker policy | Intune |
| Encryption status | Intune device report |
| Recovery keys | Entra ID device record |
| Compliance state | Compliance report |

---

## Decommissioning Assurance

During device wipe:
- BitLocker keys are destroyed
- Data becomes irrecoverable
- Wipe confirmation serves as cryptographic destruction evidence

---

## Change Control

BitLocker configuration changes:
- Require security approval
- Must be tested in Pilot
- Must be logged in the Decision Log
- Must include rollback considerations

---

## Summary

BitLocker ensures that **loss of a device does not equal loss of data**.  
It is foundational to compliance, security, and trust.

A device without BitLocker is **not trusted**.

---

## Next File

Proceed to:

**`docs/03-security/07-defender-antivirus-edr.md`**

This file defines **malware protection and endpoint detection and response (EDR)**.
