# Security Policy

## Supported Scope

This repository documents a **production-grade Windows 11 enterprise device lifecycle** using Microsoft cloud-native services. It is intended for **reference, architecture, and controlled delivery**, not as executable software.

### In Scope
- Documentation accuracy and integrity
- Security architecture guidance
- Governance, RBAC, and compliance mappings
- Operational runbooks and lifecycle procedures

### Out of Scope
- Live tenant configurations
- Customer-specific implementations
- Custom scripts, secrets, or credentials
- Zero-day vulnerability research

---

## Security Design Principles

All guidance in this repository is built on the following principles:

1. **Zero Trust by Default**
   - Identity-first access enforcement
   - No implicit trust based on network or location

2. **Least Privilege**
   - Role-based access control
   - No standing administrative privileges

3. **Fail Closed**
   - Security failures result in access denial
   - No “best-effort” or permissive fallbacks

4. **Auditability**
   - Every control maps to evidence
   - Lifecycle actions are provable and repeatable

5. **No Secrets in Source Control**
   - This repository must never contain credentials, tokens, keys, or tenant identifiers

---

## Prohibited Content

The following **must never be committed** to this repository:

- Tenant IDs, subscription IDs, or domain names
- User principal names (UPNs) or email addresses
- Device serial numbers or hardware hashes
- API keys, certificates, secrets, or passwords
- Screenshots containing sensitive information
- Exported logs from real environments

Violations must be removed immediately.

---

## Responsible Disclosure

If you identify a **security concern in the architecture, guidance, or governance model** described in this repository:

1. **Do not** open a public GitHub issue describing the vulnerability.
2. **Do not** attempt to exploit the issue in a live environment.
3. Contact the repository owner directly using a private channel.

### Disclosure Guidelines
- Provide a clear description of the issue
- Identify the affected document(s)
- Explain potential risk and impact
- Include recommended mitigations if available

All disclosures will be reviewed and addressed in a controlled manner.

---

## Change Control for Security-Sensitive Content

Security-impacting changes are subject to enhanced governance:

- Changes to identity, compliance, encryption, or access controls **require peer review**
- Production guidance must not be modified without a documented rollback plan
- Emergency changes must be reviewed post-implementation

Refer to:
- `docs/09-governance/27-change-management.md`
- `docs/09-governance/26-separation-of-duties-matrix.md`

---

## Audit and Compliance Considerations

This repository is designed to support alignment with:
- CIS Controls and Benchmarks
- NIST SP 800-53
- ISO/IEC 27001

Security reviewers should reference:
- `docs/11-compliance-mapping/31-cis-nist-iso-crosswalk.md`
- `docs/07-monitoring-and-operations/22-evidence-retention.md`

---

## Reporting Inaccuracies or Risks

If guidance becomes outdated due to platform changes or deprecations:

- Open a **documentation update** issue (non-sensitive)
- Clearly reference the impacted section
- Provide source documentation where possible

Platform freshness is a security requirement.

---

## Final Statement

This repository prioritizes **defensible security architecture over convenience**.  
Any deviation from its principles must be **intentional, documented, and approved**.

Security is not optional, implied, or assumed.

---
