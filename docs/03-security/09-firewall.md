# Windows Defender Firewall  
**Host-Based Network Protection and Isolation**

---

## Purpose

This document defines the **authoritative host-based firewall architecture** for Windows 11 endpoints.

Windows Defender Firewall is a **mandatory security control** that:
- Enforces network isolation at the device level
- Reduces lateral movement risk
- Provides auditable, policy-driven network protection
- Operates independently of network location

A device without an enabled firewall is **not trusted**.

---

## Firewall Design Objectives

The firewall implementation must ensure:

1. **Always-on enforcement**
2. **Consistent behavior across network profiles**
3. **Minimal reliance on user decisions**
4. **Compatibility with modern cloud services**
5. **Auditability and change control**

---

## Firewall Deployment  
**Exact UI Click-Path**

### Intune admin center
→ Endpoint security
→ Firewall
→ Create policy
→ Windows 10 and later
→ Microsoft Defender Firewall


---

## Firewall Policy Configuration  
**Field-by-Field (Authoritative Baseline)**

### Profile Basics

| Setting | Value | Rationale |
---|---|---|
| Name | SEC-W11-Firewall-Prod | Deterministic naming |
| Description | Windows Defender Firewall baseline | Audit clarity |

---

### Domain Profile

| Setting | Value | Rationale |
---|---|---|
| Firewall state | On | Mandatory |
| Inbound connections | Block | Least privilege |
| Outbound connections | Allow | Application-controlled |
| Notifications | Block | Prevent user overrides |
| Logging | Enabled | Evidence |

---

### Private Profile

| Setting | Value | Rationale |
---|---|---|
| Firewall state | On | Mandatory |
| Inbound connections | Block | Zero Trust |
| Outbound connections | Allow | SaaS compatibility |
| Notifications | Block | Governance |
| Logging | Enabled | Audit |

---

### Public Profile

| Setting | Value | Rationale |
---|---|---|
| Firewall state | On | Mandatory |
| Inbound connections | Block | High-risk networks |
| Outbound connections | Allow | Cloud access |
| Notifications | Block | Prevent bypass |
| Logging | Enabled | Forensics |

---

## Logging and Audit Configuration

| Log Type | State | Purpose |
---|---|---|
| Dropped packets | Enabled | Detect blocked attempts |
| Successful connections | Enabled | Traffic visibility |
| Log location | Default | Standardization |
| Log retention | OS-managed | Evidence chain |

---

## Rule Management Strategy

### Inbound Rules

- Default deny
- Only explicitly required inbound rules allowed
- Inbound rules must be:
  - Application-specific
  - Protocol-specific
  - Documented and approved

### Outbound Rules

- Default allow
- Restrictive outbound rules handled via:
  - ASR
  - Application control
  - Network security services

---

## Interaction with Other Security Controls

| Control | Interaction |
---|---|
| Security Baseline | Ensures firewall enabled |
| Defender AV | Detects malicious traffic |
| ASR | Reduces exploit-based connections |
| Compliance | Verifies firewall state |
| Conditional Access | Blocks non-compliant devices |

---

## Assignment Strategy

| Target | Assignment |
---|---|
| Production Devices | Dynamic device group |
| Pilot Devices | Separate pilot policy |
| Exceptions | Break-glass devices only |

**Rule**  
Firewall policies are assigned to **devices**, not users.

---

## Compliance Signals

| Signal | Expected State |
---|---|
| Firewall state | On |
| Profile coverage | Domain, Private, Public |
| Inbound policy | Block |
| Logging | Enabled |

Devices failing any signal are **non-compliant**.

---

## Failure Modes and Remediation

| Issue | Cause | Resolution |
---|---|---|
| Firewall off | Policy conflict | Resolve and reapply |
| App blocked | Missing inbound rule | Add scoped rule |
| Excessive logs | Debugging enabled | Tune logging |
| User prompts | Notifications allowed | Disable notifications |

Manual firewall changes on the device are prohibited.

---

## Validation Checklist

- [ ] Firewall enabled on all profiles
- [ ] Inbound default set to Block
- [ ] Outbound default set to Allow
- [ ] Logging enabled
- [ ] No user override prompts
- [ ] Device marked compliant

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| Firewall policy | Intune |
| Device firewall status | Intune reports |
| Firewall logs | Device (for forensics) |
| Compliance state | Compliance reports |

---

## Change Control

Firewall configuration changes:
- Require security approval
- Must be validated in Pilot
- Must be logged in the Decision Log
- Must include rollback strategy

---

## Summary

Windows Defender Firewall enforces **network-level Zero Trust** directly on the endpoint.

It prevents lateral movement, limits exposure on untrusted networks, and provides auditable protection regardless of location.

A device without a firewall is **not secure**.

---

## Next File

Proceed to:

**`docs/03-security/enforcement-order.md`**

This file defines the **authoritative order in which security controls are applied and enforced**.
