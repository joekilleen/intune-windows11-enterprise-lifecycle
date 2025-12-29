# Security Policy

## Purpose

This repository documents a **reference enterprise architecture** for managing Windows 11 endpoints using Microsoft Intune. It does **not** host production services, APIs, or live infrastructure.

This SECURITY.md file exists to:

* Set clear expectations for responsible disclosure
* Prevent misuse or misinterpretation of the repository contents
* Protect both the author and downstream consumers

---

## Scope

### In Scope

* Documentation errors that could materially mislead readers about security posture
* Architectural patterns that are demonstrably unsafe or deprecated
* Accidental inclusion of secrets, credentials, or tenant identifiers

### Out of Scope

* Vulnerabilities in Microsoft products or services
* Security issues in third-party software referenced conceptually
* Hypothetical attack scenarios not tied to this repository’s content

---

## Responsible Disclosure

If you believe you have identified a **security-relevant issue within this repository**, please:

1. **Do not open a public GitHub issue**
2. Contact the repository owner privately with:

   * A clear description of the issue
   * The affected file(s)
   * The potential impact

All reports will be reviewed in good faith.

---

## No Bug Bounty

This repository **does not operate a bug bounty program**. Submissions are voluntary and made without expectation of compensation.

---

## Operational Disclaimer

* This repository contains **documentation only**
* No live endpoints, tenants, or credentials are exposed
* No authorization is granted to test or probe any real systems
* All examples are generic and intentionally anonymized

Attempting to use this material to access systems you do not own or administer is prohibited.

---

## Supported Versions

This repository reflects **current, production-supported Microsoft platforms** at the time of writing. Deprecated or preview-only features are intentionally excluded.

Readers are responsible for validating platform support status in their own environments.

---

## Final Note

Security is treated as a **design constraint**, not a feature. If you believe this repository fails to meet that standard, responsible disclosure is welcomed.
