# Architecture Decision Log (ADL)

This document records **key architectural and governance decisions** made in the design of the Windows 11 Intune Enterprise Device Lifecycle.

The intent is to provide:
- Transparency for reviewers and auditors
- Historical context for future maintainers
- Justification for design trade-offs

---

## Decision Log Format

Each decision is recorded using the following structure:

- **Decision ID**
- **Decision**
- **Rationale**
- **Alternatives Considered**
- **Consequences**

---

## ADL-001 — Cloud-Native Device Management Only

**Decision**  
Use Microsoft Intune as the sole device management authority; exclude SCCM, MDT, and GPO-based management.

**Rationale**  
Cloud-native management aligns with Zero Trust principles, reduces infrastructure overhead, and enables deterministic enrollment and compliance enforcement.

**Alternatives Considered**
- Co-management with SCCM
- Hybrid GPO + MDM model

**Consequences**
- Simplified architecture
- Legacy workflows unsupported
- Requires Windows 11–capable hardware

---

## ADL-002 — Entra ID Join as Default Join Model

**Decision**  
All corporate Windows 11 devices must be Entra ID joined.

**Rationale**  
Entra ID Join enables Conditional Access enforcement, removes on-prem dependencies, and simplifies identity governance.

**Alternatives Considered**
- Hybrid Entra ID Join

**Consequences**
- No reliance on on-prem AD
- Legacy line-of-business apps may require remediation

---

## ADL-003 — Mandatory ESP Blocking During Enrollment

**Decision**  
Enrollment Status Page must block user access until required policies and applications are installed.

**Rationale**  
Prevents partially configured or insecure devices from entering production.

**Alternatives Considered**
- Non-blocking ESP
- Post-login remediation

**Consequences**
- Slightly longer first-login time
- Significantly improved security posture

---

## ADL-004 — BitLocker XTS-AES-256 Encryption

**Decision**  
Enforce BitLocker with XTS-AES-256 encryption on all OS drives.

**Rationale**  
Provides strong data-at-rest protection and aligns with enterprise security benchmarks.

**Alternatives Considered**
- XTS-AES-128
- User-driven encryption enablement

**Consequences**
- Stronger cryptographic assurance
- Requires TPM 2.0 and compatible hardware

---

## ADL-005 — Compliance-Enforced Conditional Access

**Decision**  
Require devices to be marked compliant before accessing Microsoft 365 resources.

**Rationale**  
Transforms compliance from a reporting function into an enforcement control.

**Alternatives Considered**
- Reporting-only compliance
- Network-based access controls

**Consequences**
- Non-compliant devices are blocked
- Requires robust remediation workflows

---

## ADL-006 — Win32-Only Application Packaging

**Decision**  
Package all line-of-business applications as Win32 apps.

**Rationale**  
Win32 packaging provides full control over detection, dependencies, and supersedence.

**Alternatives Considered**
- MSI-only deployments
- Store-only apps

**Consequences**
- Higher packaging discipline
- Predictable installation outcomes

---

## ADL-007 — Ring-Based Update Strategy

**Decision**  
Deploy updates using Pilot → Broad → Enterprise rings.

**Rationale**  
Reduces blast radius and enables controlled validation before full rollout.

**Alternatives Considered**
- Tenant-wide updates
- User-controlled updates

**Consequences**
- Slower full rollout
- Significantly reduced outage risk

---

## ADL-008 — Wipe Over Repair for Recovery

**Decision**  
Recover failed or compromised devices via wipe and re-enrollment rather than in-place repair.

**Rationale**  
Ensures cryptographic data destruction and eliminates configuration drift.

**Alternatives Considered**
- Manual repair
- Selective reset

**Consequences**
- Faster, cleaner recovery
- Requires Autopilot readiness

---

## ADL-009 — Least-Privilege RBAC with Scope Tags

**Decision**  
Implement custom RBAC roles with mandatory scope tags.

**Rationale**  
Limits administrative blast radius and enforces separation of duties.

**Alternatives Considered**
- Built-in roles only
- Global admin model

**Consequences**
- Slightly higher setup effort
- Strong governance and auditability

---

## ADL-010 — Fixed-Fee Client Delivery Model

**Decision**  
Deliver this architecture as a fixed-fee consulting engagement.

**Rationale**  
Aligns incentives toward outcomes, simplifies procurement, and reduces scope creep.

**Alternatives Considered**
- Time and materials
- Retainer-only model

**Consequences**
- Clear scope boundaries
- Requires disciplined change management

---

## Governance of This Log

- All material architectural changes must be recorded here
- Decisions should not be deleted—only superseded
- Auditors may treat this log as formal evidence

---
