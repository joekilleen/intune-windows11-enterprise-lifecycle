# Repository Guide — Windows 11 Intune Enterprise Device Lifecycle

## Purpose of This Repository

This repository contains a **production-grade, enterprise-defensible implementation** of a full Windows 11 device lifecycle using Microsoft cloud-native technologies. It is designed to function as:

- A reference architecture for enterprise endpoint platforms
- A delivery artifact for consulting engagements
- An auditable control record for security and compliance
- A senior-engineer portfolio demonstrating ownership-level design maturity

All content is written to withstand review by:
- Security and risk teams
- Enterprise architects
- Auditors and compliance reviewers
- Procurement and legal stakeholders

---

## Design Philosophy

This repository adheres to the following principles:

1. **Deterministic Outcomes**
   - Devices behave predictably across enrollment, operation, and retirement.
   - No reliance on technician intervention or undocumented tribal knowledge.

2. **Least Privilege and Separation of Duties**
   - Administrative authority is intentionally constrained.
   - No single role can design, approve, and bypass controls.

3. **Auditability by Default**
   - Every control maps to evidence.
   - Reports, logs, and configuration states are reproducible.

4. **Cloud-Native Only**
   - No legacy imaging, GPO dependency, or on-prem infrastructure assumptions.
   - Identity-first, Zero Trust enforcement throughout.

5. **Enterprise Safety Over Convenience**
   - Security failures fail closed.
   - Recovery paths are explicit and documented.

---

## Intended Audience

This repository is written for:

- Senior Endpoint Engineers
- Azure / Microsoft 365 Architects
- Security Operations and GRC teams
- Consulting clients and procurement reviewers
- Microsoft certification candidates (MD-102, AZ-104 adjacent)

It is **not** a beginner tutorial.

---

## How to Navigate This Repository

Documentation is organized numerically and should be read **in order**.

### Recommended Reading Path

1. **Architecture Foundations**
   - `docs/01-architecture/01-assumptions-and-constraints.md`
   - `docs/01-architecture/02-reference-architecture-and-lifecycle-flow.md`

2. **Enrollment and Security**
   - `docs/02-enrollment/*`
   - `docs/03-security/*`

3. **Compliance, Apps, and Updates**
   - `docs/04-compliance-and-access/*`
   - `docs/05-applications/*`
   - `docs/06-updates-and-servicing/*`

4. **Operations and Governance**
   - `docs/07-monitoring-and-operations/*`
   - `docs/08-lifecycle-operations/*`
   - `docs/09-governance/*`

5. **Resilience and Scale**
   - `docs/10-nonprod-dr-expansion/*`

6. **Compliance and Executive View**
   - `docs/11-compliance-mapping/*`
   - `docs/12-executive/*`

---

## Repository Structure Overview

| Folder | Purpose |
|---|---|
| `docs/` | Authoritative technical and architectural documentation |
| `client-facing/` | Statements of Work, pricing, procurement artifacts |
| `operations/` | Day-2 runbooks, checklists, and evidence templates |
| `.github/` | Governance artifacts (PR templates, issue templates) |

---

## Change Management Expectations

This repository assumes **controlled change**:

- Production guidance is immutable without review
- New policies are cloned and promoted, not edited in place
- Security-impacting changes require documented justification
- All changes must be reversible

Refer to:
- `docs/09-governance/27-change-management.md`
- `docs/09-governance/26-separation-of-duties-matrix.md`

---

## Evidence and Audit Use

This repository intentionally mirrors how auditors think:

- Controls are mapped to frameworks (CIS, NIST, ISO)
- Evidence sources are explicitly named
- Lifecycle actions produce verifiable logs

Auditors should be directed to:
- `docs/11-compliance-mapping/31-cis-nist-iso-crosswalk.md`
- `docs/07-monitoring-and-operations/22-evidence-retention.md`

---

## Licensing and Reuse

Unless otherwise specified:

- Configuration concepts are client-owned
- Methodology, structure, and templates remain reusable
- No tenant-specific identifiers should ever be committed

See `LICENSE.md` for full terms.

---

## Support and Contributions

This repository is not an open-support project.

If used for:
- Client delivery → follow SOW governance
- Internal platform → assign CODEOWNERS
- Portfolio review → preserve commit history

---

## Start Here

Proceed next to:

**`docs/01-architecture/01-assumptions-and-constraints.md`**

This file defines the operating envelope for **every decision that follows**.
