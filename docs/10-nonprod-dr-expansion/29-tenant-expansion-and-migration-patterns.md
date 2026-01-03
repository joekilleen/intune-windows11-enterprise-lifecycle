# Tenant Expansion and Migration Patterns  
**M&A, Carve-Outs, and Controlled Endpoint Growth**

---

## Purpose

This document defines the **authoritative patterns** for expanding, splitting, or migrating Microsoft Intune–managed Windows 11 environments across Microsoft Entra ID tenants.

The objectives are to:
- Support mergers, acquisitions, and divestitures
- Enable clean tenant separation or consolidation
- Preserve security posture during transition
- Minimize user disruption
- Maintain audit and compliance continuity

Tenant expansion is a **governance event**, not a technical afterthought.

---

## Design Objectives

Tenant expansion and migration must ensure:

1. **Clear trust boundaries**
2. **Deterministic migration paths**
3. **No policy contamination**
4. **Minimal downtime**
5. **Evidence continuity**
6. **Explicit risk ownership**

---

## Common Expansion Scenarios

| Scenario | Description |
---|---|
| Merger (Many → One) | Consolidating multiple tenants |
| Acquisition (One → Many) | Maintaining separation |
| Divestiture / Carve-Out | Splitting a tenant |
| Regional expansion | New geography or subsidiary |
| Regulatory isolation | Compliance-driven separation |

Each scenario requires a **different control posture**.

---

## Pattern 1 — Acquisition with Tenant Isolation (Preferred)

### Description
The acquired organization retains its tenant initially.

### Characteristics

- Separate Entra ID tenant
- Separate Intune tenant
- Federated collaboration (B2B)
- No immediate device migration

### Advantages

- Strong security isolation
- Minimal disruption
- Clear rollback path
- Simplified compliance mapping

### Disadvantages

- Duplicate tooling
- Cross-tenant complexity

### When to Use
- Unknown security posture
- High regulatory risk
- Short-term ownership uncertainty

---

## Pattern 2 — Acquisition with Gradual Consolidation

### Description
Devices are migrated into the parent tenant in phases.

### Migration Phases

1. Identity trust established (B2B / cross-tenant sync)
2. Pilot device migration
3. Application and policy parity validation
4. Broad migration
5. Legacy tenant retirement

### Advantages

- Long-term simplicity
- Unified management
- Reduced licensing sprawl

### Risks

- Policy collision
- Identity confusion
- Data migration complexity

Mitigation requires **pilot tenants and staged rollout**.

---

## Pattern 3 — Divestiture / Carve-Out

### Description
A subset of users and devices must exit the tenant.

### Mandatory Principles

- New tenant created first
- Clean identity boundary established
- Devices re-enrolled, not transferred
- Data ownership clarified

### Device Handling Rules

| Item | Rule |
---|---|
| Devices | Full wipe + re-enroll |
| Autopilot | Deregister from source |
| Policies | Recreated, not copied blindly |
| Apps | Repackaged or reassigned |

Trust **does not migrate**.

---

## Pattern 4 — Regional or Regulatory Expansion

### Description
New tenant required due to data residency or regulation.

### Controls

- Region-specific tenant
- Dedicated Autopilot profiles
- Separate compliance baselines
- Limited cross-tenant access

This pattern often applies to:
- GDPR
- Financial regulation
- Government contracts

---

## Identity and Access Considerations

### Cross-Tenant Access

- Use Entra ID B2B for collaboration
- Avoid shared admin accounts
- Enforce Conditional Access per tenant
- Separate break-glass accounts per tenant

### Prohibited Practices

- Sharing Global Admin accounts
- Syncing privileged roles
- Reusing device identities

---

## Device Migration Strategy (Authoritative)

### Supported Method

**Wipe and Re-enroll via Autopilot**

Steps:
1. Remove device from source Intune
2. Deregister Autopilot (if changing ownership)
3. Wipe device
4. Register in target tenant Autopilot
5. Enroll and validate

### Unsupported Methods

- Device-to-device cloning
- Tenant-to-tenant “transfer”
- Manual policy export/import without review

---

## Application and Policy Strategy

### Required Discipline

- Rebuild policies using baseline templates
- Validate settings against target tenant standards
- Do not assume parity
- Treat each tenant as a fresh environment

Migration is an opportunity to **correct legacy debt**.

---

## Evidence and Audit Continuity

During expansion or migration, retain:

| Artifact | Purpose |
---|---|
| Pre-migration inventory | Baseline |
| Migration plan | Risk management |
| Pilot results | Due diligence |
| Cutover approvals | Governance |
| Post-migration validation | Control assurance |

Auditors will ask:
> “How did you ensure security did not degrade during migration?”

---

## Failure Modes and Mitigation

| Failure | Impact | Mitigation |
---|---|---|
| Direct prod migration | Outage | Pilot first |
| Policy sprawl | Inconsistency | Rebuild |
| Identity overlap | Access risk | Hard boundaries |
| Incomplete wipe | Data leakage | Enforce runbooks |
| No evidence | Audit failure | Mandatory artifacts |

---

## Governance and Ownership

| Role | Responsibility |
---|---|
| Enterprise Architecture | Pattern selection |
| Security | Trust validation |
| Endpoint Engineering | Execution |
| GRC | Evidence and audit |
| Management | Risk acceptance |

---

## Change Control

Tenant expansion activities:
- Require executive approval
- Must have rollback strategy
- Must include pilot phase
- Must be documented in the Decision Log

---

## Summary

Tenant expansion and migration are **organizational trust events**.

When executed correctly:
- Risk is contained
- Security posture is preserved
- Growth is predictable
- Audits are defensible

When rushed:
- Trust boundaries blur
- Incidents multiply
- Compliance erodes

---

## Section Completion

With this document, **Section 10 — Non-Production, DR, and Tenant Expansion Patterns** is **complete**.

---

## Next Section

Proceed to:

**`docs/11-client-delivery/31-client-facing-delivery-model.md`**

This section defines **SOW structure, fixed-fee pricing, and engagement delivery models**.
