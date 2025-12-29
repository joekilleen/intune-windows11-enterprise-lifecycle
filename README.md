# intune-windows11-enterprise-lifecycle
This document defines a production-grade, end-to-end lifecycle model for managing Windows 11 enterprise devices using Microsoft Intune integrated with Microsoft Entra ID. It is written for senior endpoint engineers, security architects, and auditors and aligns with Microsoft MD-102/AZ-104 expectations.

1. Lifecycle Overview (Authoritative Model)
The lifecycle is divided into eight deterministic phases, each with explicit ownership, controls, and exit criteria:

Procurement & Registration
Identity Binding & Trust Establishment
Provisioning (Autopilot)
Configuration & Hardening
Application Lifecycle Management
Compliance, Monitoring & Operations
Change, Repair & Reassignment
Decommissioning & Data Sanitization

This model enforces zero-touch deployment, least privilege, and continuous compliance.

2. Procurement & Registration
Objective: Ensure devices are known, trusted, and governed before first boot.
Controls

OEM or reseller uploads Windows Autopilot hardware hashes

Devices assigned to:
Deployment profile
Enrollment Status Page (ESP)
Group tags (e.g., WIN11-CORP-STD)

Outputs
Device appears in Intune as Autopilot registered
No local user access possible prior to enrollment

Risk Mitigated
Shadow IT
Unauthorized OS provisioning

3. Identity Binding & Trust Establishment
Objective: Bind device identity to corporate identity with cryptographic trust.

Key Decisions
Microsoft Entra ID Join (recommended)
Certificate-based trust via TPM 2.0
Optional Windows Hello for Business (cloud trust)
Security Outcomes
Device object created in Entra ID

Conditional Access evaluates device state, not just user

4. Provisioning (Windows Autopilot)
Objective: Zero-touch deployment with policy-driven outcomes.
Process

User signs in with corporate identity

Autopilot enforces:
Device naming convention
Enrollment Status Page blocking
Required security baselines
Hard Requirements
BitLocker enabled
Defender AV & ASR rules applied
No local admin persistence (except controlled break-glass)
Exit Criteria
Device reports Compliant
ESP completes successfully

5. Configuration & Hardening
Objective: Enforce security, OS, and UX standards consistently.
Policy Domains
Security Baselines (Windows 11)
Endpoint Protection (Defender, Firewall, ASR)
Device Configuration (CSP-based)
Update Rings (WUfB)
Operational Principle

Configuration is immutable by users, auditable by security, and reversible by IT.

6. Application Lifecycle Management
Objective: Deliver, update, and retire software safely.
Application Types
Win32 (LOB)
Microsoft Store (new)
Microsoft 365 Apps
Controls
Detection rules (authoritative)
Dependencies & supersedence
Assignment by Entra ID groups (dynamic where possible)
Operational Standard

All apps are:
Versioned
Detectable
Removable
Logged

7. Compliance, Monitoring & Operations
Objective: Maintain continuous assurance.

Compliance Signals

OS version
Encryption state
Defender health
Secure Boot / TPM
Integrations
Conditional Access (block non-compliant devices)
Endpoint analytics
Audit logs retained per policy
Expected Outcomes
Near-real-time visibility
Automated access revocation on drift

8. Change, Repair & Reassignment
Objective: Safely handle device lifecycle events without data loss or security erosion.

Scenarios
Hardware repair
User change
Role change
Controls
Autopilot Reset (where applicable)
Device reassignment with policy re-evaluation
No manual reconfiguration

9. Decommissioning & Data Sanitization
Objective: Ensure secure exit with zero residual risk.
Approved Actions
Retire – corporate data removed, device remains usable
Wipe – full data destruction, device reset to OOBE
Audit Requirements
Wipe confirmation logged

Device object removed from:
Intune
Entra ID

Autopilot (if disposed)

10. Operational & Audit Considerations
Area	Control
RBAC	Intune roles scoped by function
Logging	Unified Audit Log + Intune logs
Change Mgmt	Version-controlled policy changes
DR	Re-enrollment tested quarterly
Legal Hold	eDiscovery-compatible data handling
