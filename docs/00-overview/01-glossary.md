# Glossary — Windows 11 Intune Enterprise Device Lifecycle

This glossary defines **authoritative terminology** used throughout this repository.  
Definitions are written to align with **Microsoft documentation**, **enterprise security language**, and **audit expectations**.

Terms are listed alphabetically.

---

## A

### Autopilot
A Microsoft cloud-based provisioning service that enables zero-touch deployment of Windows devices by applying predefined configuration during first boot.

### Autopilot Reset
An Intune-initiated action that removes user data and settings while preserving device enrollment, allowing rapid reassignment without full re-enrollment.

---

## B

### BitLocker
Microsoft full-disk encryption technology used to protect data at rest. In this architecture, BitLocker is enforced with **XTS-AES-256** and recovery keys are escrowed to Entra ID.

### Break-Glass Account
A highly restricted emergency access account excluded from certain security controls (such as Conditional Access) and used only during critical incidents.

---

## C

### Conditional Access (CA)
An identity-based access control mechanism in Entra ID that evaluates signals (user, device, location, risk) before granting access to cloud resources.

### Compliance Policy
An Intune policy that evaluates device state (e.g., encryption, OS version, Defender health) and assigns a compliant or non-compliant status.

### Corporate-Owned Device
A device owned and managed by the organization, subject to full security and lifecycle controls.

---

## D

### Defender for Endpoint (MDE)
Microsoft’s endpoint detection and response (EDR) platform providing threat detection, investigation, and remediation.

### Device Lifecycle
The complete sequence of states a device passes through: procurement, provisioning, operation, reassignment, and decommissioning.

---

## E

### Enrollment Status Page (ESP)
A Windows setup phase that blocks user access until required policies and applications are successfully installed.

### Entra ID
Microsoft’s cloud identity platform (formerly Azure Active Directory), providing authentication, authorization, and identity governance.

---

## F

### Feature Update
A major Windows release (e.g., Windows 11 23H2) introducing new functionality and lifecycle changes.

### Firewall (Windows Defender Firewall)
Host-based firewall built into Windows, enforced in this architecture across all network profiles.

---

## G

### Grace Period
A limited window during which a non-compliant device may remain operational while automated remediation occurs. After expiration, access is blocked.

---

## I

### Intune
Microsoft cloud service for device management (MDM), application deployment, policy enforcement, and lifecycle actions.

### Intune Management Extension (IME)
A Windows service installed by Intune that enables Win32 application deployment, scripts, and remediation actions.

---

## L

### Least Privilege
A security principle requiring users and administrators to have only the permissions necessary to perform their tasks.

---

## M

### Microsoft Defender Antivirus
Built-in Windows antimalware engine providing real-time protection and cloud-assisted threat detection.

### Monitoring
The continuous collection and analysis of telemetry related to device health, security posture, and operational status.

---

## P

### Pilot Ring
A small subset of devices used to validate changes before broader deployment.

### Production
The live, business-critical environment where stability and security take precedence over experimentation.

---

## R

### RBAC (Role-Based Access Control)
A permissions model that assigns capabilities based on role definitions rather than individual users.

### Refresh
A lifecycle operation that rebuilds a device to a known-good state, typically via wipe and re-enrollment.

---

## S

### Scope Tag
An Intune construct that limits which objects (devices, apps, policies) an administrator can see or manage.

### Security Baseline
A Microsoft-recommended collection of configuration settings designed to harden Windows endpoints.

### Supersedence
An Intune application feature that defines upgrade and replacement relationships between app versions.

---

## T

### Tenant
A dedicated Microsoft Entra ID and Intune environment representing an organization.

### TPM (Trusted Platform Module)
A hardware component providing cryptographic functions and secure storage, required for this architecture.

---

## W

### Windows Update for Business (WUfB)
A cloud-based update management approach that controls Windows updates using Intune policies rather than on-prem servers.

### Wipe
An Intune action that removes all data from a device and destroys encryption keys, ensuring data destruction.

---

## Z

### Zero Trust
A security model that assumes no implicit trust and continuously verifies identity, device, and context before granting access.

---

## Glossary Governance

- This glossary is **authoritative** for this repository.
- New terms must be added here before being used elsewhere.
- Definitions should remain concise, precise, and audit-safe.

---
