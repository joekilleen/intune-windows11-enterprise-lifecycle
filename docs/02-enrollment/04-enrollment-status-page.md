# Enrollment Status Page (ESP)  
**Security Gating and Deterministic Provisioning**

---

## Purpose

The Enrollment Status Page (ESP) is a **critical security control**, not a user-experience feature.

This document defines the **authoritative ESP configuration** used to:
- Block access to Windows until baseline security is applied
- Prevent partially configured devices from entering production
- Ensure deterministic enrollment outcomes

ESP is the **enforcement mechanism** that guarantees devices are secure *before* first use.

---

## ESP Design Objectives

The ESP configuration must ensure:

1. **Fail-closed enrollment**
2. **Security controls apply before user access**
3. **No bypass via reset or retry**
4. **Predictable troubleshooting and recovery**
5. **Clear ownership of failures**

---

## ESP Scope and Enforcement Model

| Dimension | Decision |
|---|---|
| ESP Mode | Blocking |
| Target | Device-based |
| Required Items | Security + critical apps |
| User Bypass | Prohibited |
| Failure Handling | Enrollment failure |
| Recovery | Reset or wipe only |

---

## ESP Configuration  
**Exact UI Click-Path**

## Intune admin center
→ Devices
→ Windows
→ Windows enrollment
→ Enrollment Status Page
→ Create


---

## ESP Profile Configuration  
**Field-by-Field (Authoritative Baseline)**

### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | ESP-W11-Enterprise-Prod | Deterministic naming |
| Description | Blocking ESP for Windows 11 enterprise enrollment | Clarity |

---

### Enrollment Settings

| Setting | Value | Rationale |
---|---|---|
| Show app and profile installation progress | Yes | Transparency |
| Show error when installation fails | Yes | Deterministic failure |
| Allow users to collect logs | Yes | Support efficiency |
| Allow users to retry installation | No | Prevent bypass |
| Allow users to reset device | No | Prevent security evasion |

---

### Device Preparation

| Setting | Value | Rationale |
---|---|---|
| Block device use until required apps installed | Yes | Fail closed |
| Block on required app install failure | Yes | Deterministic state |
| Timeout (minutes) | 60 | Balanced enforcement |

---

### Account Setup

| Setting | Value | Rationale |
---|---|---|
| Block user until account setup complete | Yes | Security-first |
| Skip user status page | No | Visibility |

---

## Required Items During ESP

### Policy Categories (Mandatory)

The following **must complete successfully** during ESP:

- Entra ID Join
- Intune MDM enrollment
- Security baseline policies
- BitLocker enforcement
- Defender AV onboarding
- Defender for Endpoint onboarding
- Firewall policy

---

### Application Categories (ESP-Safe Only)

Only **ESP-safe applications** are allowed as required during ESP.

**Allowed Examples**
- Microsoft 365 Apps
- Company Portal
- VPN bootstrap client (if required for compliance)

**Prohibited During ESP**
- Large line-of-business apps
- Apps requiring user context
- Apps with reboot requirements
- Apps with unreliable detection

> ESP instability is treated as a **security risk**, not a packaging issue.

---

## ESP-Safe Application Criteria

An application is ESP-safe only if it meets **all** criteria:

- System context installation
- Deterministic detection rule
- No user interaction
- No reboot requirement
- Installation time < 10 minutes
- No external dependencies

Apps failing these criteria **must not** be required during ESP.

---

## Failure Modes and Resolution

| Symptom | Root Cause | Resolution |
---|---|---|
| ESP stuck at app install | Bad detection rule | Fix detection; redeploy |
| ESP timeout | App too large/slow | Remove from ESP |
| Device loops OOBE | Policy conflict | Review enrollment logs |
| User sees desktop early | ESP misconfigured | Enforce blocking |
| User resets device | Reset allowed | Disable reset option |

---

## Troubleshooting Workflow

1. Collect ESP logs from device
2. Review Intune device install status
3. Identify failed policy or app
4. Correct root cause (policy/app)
5. Reset device (Autopilot Reset preferred)
6. Re-enroll and validate

**Manual remediation on the device is prohibited.**

---

## Security Considerations

- ESP failures indicate **control failures**
- Bypassing ESP weakens the entire lifecycle
- All ESP changes require pilot validation
- ESP policies are production-critical

---

## Validation Checklist (Required)

- [ ] User blocked until ESP completion
- [ ] Required policies applied successfully
- [ ] Required apps installed successfully
- [ ] BitLocker encryption initiated
- [ ] Defender services running
- [ ] Device marked compliant post-enrollment

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| ESP profile configuration | Intune |
| App install status | Intune app monitoring |
| Enrollment logs | Device + Intune |
| Compliance state | Intune compliance report |

---

## Change Control

Changes to ESP configuration:
- Must be tested in Pilot ring
- Require approval before production
- Must be documented in the Decision Log
- Must include rollback strategy

---

## Summary

The Enrollment Status Page is the **gatekeeper** of the enterprise device lifecycle.  
If ESP is unreliable, the entire security model is compromised.

ESP must remain **strict, predictable, and boring**.

---

## Next File

Proceed to:

**`docs/03-security/05-security-baselines.md`**

This file defines the **baseline security posture** enforced immediately after enrollment.
