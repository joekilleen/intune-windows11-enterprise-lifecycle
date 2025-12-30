# Windows Autopilot Deployment Profile  
**Zero-Touch Enrollment Architecture (Windows 11)**

---

## Purpose

This document defines the **authoritative Windows Autopilot deployment profile** used to enroll corporate Windows 11 devices into the enterprise lifecycle.

It specifies:
- The enrollment model
- Exact configuration decisions
- Required constraints for security and reliability
- Validation outcomes and failure handling

This profile is the **entry point** to the entire lifecycle described in Section 1.

---

## Enrollment Objectives

The Autopilot deployment profile must ensure:

1. **Zero-touch provisioning**
2. **Entra ID Join only**
3. **Immediate MDM authority**
4. **Blocking enrollment until security controls apply**
5. **No local admin persistence**

---

## Enrollment Model (Authoritative)

| Dimension | Decision |
|---|---|
| Join Type | Entra ID Join |
| Ownership | Corporate-owned |
| Enrollment Method | Windows Autopilot |
| MDM Authority | Microsoft Intune |
| User Privilege | Standard User |
| Technician Interaction | None |

---

## Prerequisites (Mandatory)

### Tenant Prerequisites
- Microsoft Intune enabled
- Entra ID configured as identity authority
- Required licenses assigned
- Conditional Access policies **exclude enrollment endpoints**

### Device Prerequisites
- Windows 11 Enterprise capable hardware
- TPM 2.0 present and enabled
- Secure Boot enabled
- OEM-registered Autopilot hardware hash
- Internet connectivity during OOBE

Failure to meet prerequisites results in **enrollment block**.

---

## Deployment Profile Creation  
**Exact UI Click-Path**

Intune admin center
→ Devices
→ Windows
→ Windows enrollment
→ Deployment profiles
→ Create profile
→ Windows PC


---

## Deployment Profile Configuration  
**Field-by-Field (Authoritative Baseline)**

### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | AP-W11-Enterprise-Prod | Deterministic naming |
| Description | Corporate Windows 11 Autopilot profile | Clarity |
| Platform | Windows PC | Required |

---

### Out-of-Box Experience (OOBE)

| Setting | Value | Rationale |
---|---|---|
| Deployment mode | User-driven | Identity-first |
| Join to Entra ID as | Entra ID joined | No hybrid |
| Microsoft Software License Terms | Hide | Reduce friction |
| Privacy settings | Hide | Standardized |
| Hide change account options | Hide | Prevent misconfiguration |
| User account type | Standard | Least privilege |
| Allow pre-provisioning | No (unless explicitly required) | Reduce complexity |

---

### Enrollment Status Page (ESP)

| Setting | Value | Rationale |
---|---|---|
| Enable ESP | Yes | Security gating |
| Block device use until required apps installed | Yes | Fail closed |
| Allow users to reset device if installation error | No | Prevent bypass |
| Block on app failures | Yes | Deterministic state |
| Timeout (minutes) | 60 | Controlled |

> ESP behavior is further defined in `04-enrollment-status-page.md`.

---

## Group Assignment Strategy

### Device Assignment (Mandatory)

Deployment profiles **must be assigned to devices**, not users.

**Dynamic Device Group Example**

```text
(device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))

Rationale

Ensures profile is applied before first boot

Prevents user-driven enrollment bypass

Enrollment Enforcement Sequence

sequenceDiagram
  participant Device
  participant Autopilot
  participant Entra
  participant Intune

  Device->>Autopilot: First boot / OOBE
  Autopilot->>Device: Deployment profile
  Device->>Entra: User authentication
  Entra->>Device: Join completed
  Device->>Intune: MDM enrollment
  Intune->>Device: ESP starts (blocking)

Failure Modes and Handling

| Failure                 | Cause                 | Resolution                        |
| ----------------------- | --------------------- | --------------------------------- |
| Device not recognized   | Hash not registered   | Register hardware hash            |
| User sees consumer OOBE | Profile not assigned  | Fix group targeting               |
| ESP stuck               | App/policy failure    | Review ESP logs                   |
| Local admin created     | Misconfigured profile | Enforce standard user             |
| Enrollment bypass       | CA misconfiguration   | Exclude only enrollment endpoints |

Security Considerations

Enrollment endpoints must be excluded from Conditional Access only where required

No permanent CA exclusions allowed

Enrollment logs must be retained

ESP failures are treated as security failures, not UX issues

Validation Checklist (Required)

 Device joins Entra ID (not hybrid)

 Device appears in Intune within minutes

 User is standard user

 ESP blocks until required items complete

 Security baseline begins applying immediately

Evidence Artifacts

| Artifact                        | Source               |
| ------------------------------- | -------------------- |
| Autopilot profile configuration | Intune               |
| Device enrollment record        | Intune device object |
| Entra ID join state             | Device properties    |
| ESP status                      | Enrollment logs      |


Change Control

Any change to the Autopilot deployment profile:

Requires pilot validation

Must be documented in the Architecture Decision Log

Cannot be edited in place for production

Summary

This Autopilot deployment profile establishes initial trust between the device, identity platform, and management plane.
Every subsequent security, compliance, and operational control depends on this step succeeding.
