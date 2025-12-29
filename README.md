# Microsoft Intune Enterprise Device Lifecycle (Windows 11)

Production-grade, audit-defensible implementation of an end-to-end Windows 11 device lifecycle using:
- Microsoft Entra ID (identity and Conditional Access)
- Microsoft Intune (enrollment, policy, apps, lifecycle actions)
- Microsoft Defender for Endpoint (EDR)

## What This Repository Provides
- Reference architecture and lifecycle flow (Mermaid diagrams included)
- Exact Intune/Entra UI click-paths and field-by-field configuration tables
- Security baseline and hardening architecture (BitLocker, Defender, ASR, Firewall)
- Compliance + Conditional Access enforcement model
- Application lifecycle model (Win32, ESP-safe design, supersedence)
- Update & servicing strategy (WUfB rings, feature updates, drivers/firmware)
- Monitoring, reporting, and evidence retention guidance
- Device lifecycle operations (reset, reassignment, decommissioning)
- Governance (RBAC, scope tags, separation of duties)
- Non-production, DR, and tenant expansion patterns
- Client-facing SOW, pricing exhibit, and procurement artifacts

## Intended Audience
Senior Azure/Endpoint engineers, enterprise architects, security reviewers, auditors, and MD-102 candidates.

## How to Use
Start here:
1. `docs/01-architecture/01-assumptions-and-constraints.md`
2. `docs/01-architecture/02-reference-architecture-and-lifecycle-flow.md`
3. Follow the docs in numeric order.

Client delivery artifacts:
- `client-facing/SOW/statement-of-work.md`
- `client-facing/pricing/pricing-exhibit.md`

## Governance
Changes must follow:
- `docs/09-governance/27-change-management.md`
- Separation of duties: `docs/09-governance/26-separation-of-duties-matrix.md`

## License
See `LICENSE`.
