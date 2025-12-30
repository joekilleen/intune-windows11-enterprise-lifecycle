# Compliance Policies  
**Device Health Signals, Grace Periods, and Remediation Logic**

---

## Purpose

This document defines the **authoritative device compliance policy model** for Windows 11 endpoints.

Compliance policies transform security configuration into **enforceable access decisions** by:
- Continuously evaluating device health
- Publishing compliance state to Entra ID
- Driving Conditional Access outcomes

Compliance without enforcement is informational only and **not sufficient**.

---

## Compliance Design Objectives

The compliance model must ensure:

1. **Continuous evaluation**
2. **Clear pass/fail signals**
3. **Limited and explicit grace periods**
4. **Automated remediation where possible**
5. **Deterministic access enforcement**

---

## Compliance Scope

| Scope | Included |
|---|---|
| OS security posture | Yes |
| Encryption state | Yes |
| Malware protection | Yes |
| OS version currency | Yes |
| Firewall state | Yes |
| User behavior | No |
| Application inventory | No |

Compliance policies are **device-based**, not user-based.

---

## Compliance Policy Creation  
**Exact UI Click-Path**

### Intune admin center
→ Devices
→ Windows
→ Compliance policies
→ Create policy
→ Windows 10 and later


---

## Compliance Policy Configuration  
**Field-by-Field (Authoritative Baseline)**

### Policy Basics

| Setting | Value | Rationale |
---|---|---|
| Name | CMP-W11-Enterprise-Prod | Deterministic naming |
| Description | Windows 11 enterprise compliance baseline | Audit clarity |
| Platform | Windows 10 and later | Applies to Windows 11 |

---

### Device Health

| Setting | Required State | Rationale |
---|---|---|
| Require BitLocker | Yes | Data protection |
| Require Secure Boot | Yes | Boot integrity |
| Require code integrity | Yes | Kernel trust |
| Require TPM | Yes | Hardware trust |

---

### System Security

| Setting | Required State | Rationale |
---|---|---|
| Antivirus | Enabled | Malware prevention |
| Antispyware | Enabled | Threat coverage |
| Real-time protection | Enabled | Active defense |

---

### Microsoft Defender for Endpoint

| Setting | Required State | Rationale |
---|---|---|
| Defender for Endpoint | Enabled | EDR visibility |
| Risk score | Low or below | Threat containment |

---

### Firewall

| Setting | Required State | Rationale |
---|---|---|
| Firewall | Enabled | Network isolation |

---

### OS Version

| Setting | Required State | Rationale |
---|---|---|
| Minimum OS version | Defined per servicing baseline | Patch hygiene |
| Maximum OS version | Optional | Version pinning |

---

### Password / Account (Minimal)

| Setting | Required State | Rationale |
---|---|---|
| Password required | Yes | Basic control |
| Simple passwords | Blocked | Baseline hygiene |

---

## Compliance Grace Period

### Grace Period Configuration

| Setting | Value | Rationale |
---|---|---|
| Mark device non-compliant | Immediately | Accurate signal |
| Grace period | 3 days (recommended) | Limited remediation window |

**Rule**
Grace periods are a **temporary allowance**, not a bypass.

---

## Remediation Model

### Automated Remediation

The following issues are remediated automatically:

| Signal | Remediation |
---|---|
| Encryption off | BitLocker policy reapplies |
| Defender disabled | AV/EDR policy reapplies |
| Firewall off | Firewall policy reapplies |
| OS out of date | Update policies enforce |

---

### Manual Intervention Triggers

Manual intervention is required when:
- Hardware prerequisites fail
- Secure Boot or TPM unavailable
- Repeated remediation failures occur
- Device is suspected compromised

**Approved Action**
- Autopilot Reset or Wipe

---

## Assignment Strategy

| Target | Assignment |
---|---|
| Production Devices | Dynamic device group |
| Pilot Devices | Separate pilot compliance policy |
| Exceptions | Break-glass devices only |

**Rule**
Compliance policies are assigned to **devices**, not users.

---

## Compliance Evaluation Flow

```mermaid
flowchart LR
  A["Device reports state"] --> B["Compliance policy evaluation"]
  B -->|Compliant| C["Publish compliant state"]
  B -->|Non-compliant| D["Publish non-compliant state"]
  D --> E["Grace period (if applicable)"]
  E -->|Resolved| C
  E -->|Expired| F["Access blocked via CA"]
