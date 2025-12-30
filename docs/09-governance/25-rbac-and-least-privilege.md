# RBAC and Least Privilege  
**Delegated Administration, Scope Tags, and Separation of Duties**

---

## Purpose

This document defines the **authoritative Role-Based Access Control (RBAC) model** for managing Windows 11 endpoints with Microsoft Intune and Microsoft Entra ID.

The RBAC model ensures:
- Least-privilege access by design
- Clear separation of duties
- Reduced blast radius for mistakes or compromise
- Audit-ready accountability
- Scalable delegated administration

RBAC is a **security control**, not an administrative convenience.

---

## Design Objectives

The RBAC strategy must ensure:

1. **Least privilege by default**
2. **Role clarity and accountability**
3. **Operational scalability**
4. **Audit traceability**
5. **Separation of duties**
6. **No shared administrative identities**

---

## Governance Principles

- Access is granted to **roles**, not individuals
- Roles are scoped to **what is required, no more**
- Delegation is **explicit and reviewable**
- Privileged actions are **logged and attributable**
- Temporary elevation is preferred over standing access

---

## Systems in Scope

| Platform | Scope |
---|---|
| Microsoft Intune | Device and app management |
| Microsoft Entra ID | Identity and access |
| Microsoft Defender | Endpoint security |
| Conditional Access | Access enforcement |
| Autopilot | Device provisioning |

---

## Role Taxonomy (Authoritative)

### Tiered Administrative Model

| Tier | Description |
---|---|
| Tier 0 | Identity and security control plane |
| Tier 1 | Endpoint and device management |
| Tier 2 | Service desk and operations |
| Tier 3 | Read-only / audit |

Cross-tier access is **explicitly prohibited**.

---

## Intune RBAC Roles

### Built-in Roles (Preferred)

| Role | Use |
---|---|
| Endpoint Administrator | Full endpoint lifecycle |
| Application Manager | App packaging and deployment |
| Help Desk Operator | User-facing support |
| Read Only Operator | Audit and reporting |

Built-in roles are preferred for **supportability and audit clarity**.

---

### Custom Roles (Exception-Based)

Custom roles may be created only when:
- Built-in roles are insufficient
- Scope can be tightly controlled
- Approval is documented

Custom roles must be reviewed **quarterly**.

---

## Scope Tags (Mandatory)

Scope tags enforce **administrative boundaries**.

### Approved Scope Tag Categories

| Category | Example |
---|---|
| Environment | Prod / NonProd |
| Business Unit | Finance / Engineering |
| Geography | US / EU |
| Device Class | Workstation / Kiosk |

Scope tags must be applied consistently across:
- Devices
- Applications
- Configuration profiles
- Compliance policies

---

## Delegation Model

### Tier 1 — Endpoint Engineering

| Capability | Allowed |
---|---|
| Device configuration | Yes |
| Compliance policies | Yes |
| Security baselines | Yes |
| Conditional Access | No |
| Identity management | No |

---

### Tier 2 — Service Desk

| Capability | Allowed |
---|---|
| Device reset | Yes |
| Device reassignment | Yes |
| Remote assistance | Yes |
| App deployment | No |
| Policy creation | No |

---

### Tier 3 — Audit / GRC

| Capability | Allowed |
---|---|
| Report access | Read-only |
| Log export | Read-only |
| Configuration changes | No |

---

## Entra ID Privileged Roles

### Restricted Roles (Tier 0)

| Role | Restriction |
---|---|
| Global Administrator | Break-glass only |
| Privileged Role Administrator | Security-only |
| Security Administrator | Security team only |

Standing assignment to these roles is **prohibited**.

---

## Privileged Identity Management (PIM)

PIM **must** be used for all privileged roles.

### PIM Requirements

| Control | Requirement |
---|---|
| Approval | Required |
---| MFA | Required |
| Duration | Time-bound |
| Justification | Mandatory |
| Logging | Enabled |

Emergency access uses **break-glass accounts only**.

---

## Separation of Duties (SoD)

### Prohibited Role Combinations

| Combination | Risk |
---|---|
| Policy author + auditor | Control bypass |
| Endpoint admin + security admin | Excessive power |
| App packager + approver | Supply chain risk |

SoD violations require **risk acceptance**.

---

## Operational Workflows and RBAC Mapping

| Workflow | Role |
---|---|
| App packaging | Application Manager |
| App approval | Endpoint Engineering |
| Device wipe | Endpoint Administrator |
| Incident isolation | Security Operations |
| Audit reporting | Read Only Operator |

---

## Access Review and Recertification

| Review Type | Frequency |
---|---|
| Privileged roles | Quarterly |
| Standard roles | Semi-annually |
| Custom roles | Quarterly |
| Break-glass accounts | Monthly |

All reviews must be **documented**.

---

## Logging and Auditability

The following must be logged and retained:

| Action | Source |
---|---|
| Role assignments | Entra ID audit logs |
| Scope tag changes | Intune audit logs |
| Privileged activations | PIM logs |
| Administrative actions | Intune / Entra ID |

Logs must be retained per **evidence retention policy**.

---

## Common RBAC Failure Patterns (Avoid)

| Failure | Impact |
---|---|
| Global admin sprawl | High breach impact |
| Shared admin accounts | No accountability |
| No scope tags | Excessive blast radius |
| No access reviews | Privilege creep |
| Standing privilege | Increased attack surface |

---

## Change Control

RBAC changes:
- Require security approval
- Must be documented in the Decision Log
- Must include rollback plan
- Must be validated post-change

---

## Summary

RBAC is the **control plane for trust**.

When implemented correctly:
- Mistakes are contained
- Attacks are limited
- Accountability is clear
- Audits are straightforward

When implemented poorly:
- Every admin is a single point of failure

---

## Next File

Proceed to:

**`docs/09-governance-and-rbac/26-scope-tags-and-operational-separation.md`**

This file defines **practical scope tag design and operational isolation patterns**.
