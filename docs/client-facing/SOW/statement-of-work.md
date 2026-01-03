# Statement of Work (SOW)  
**Windows 11 Enterprise Device Lifecycle Implementation (Microsoft Intune)**

---

## 1. Parties

This Statement of Work (“SOW”) is entered into between:

**Client:** [Client Legal Name]  
**Provider:** [Provider Legal Name]

This SOW is governed by the terms and conditions of the applicable Master Services Agreement (“MSA”). In the event of a conflict, the MSA shall control.

---

## 2. Purpose and Objectives

The purpose of this engagement is to design and implement a **production-grade Windows 11 Enterprise Device Lifecycle** using Microsoft Intune and Microsoft Entra ID.

The objectives are to:

- Establish a secure, compliant, and auditable endpoint management architecture
- Enforce device-based access controls and security baselines
- Standardize application delivery and update servicing
- Enable predictable lifecycle operations (reset, reassignment, decommissioning)
- Deliver documentation suitable for audit, operations, and executive review

This engagement prioritizes **risk reduction, operational maturity, and audit readiness**.

---

## 3. Scope of Work

### 3.1 In-Scope Services

The Provider will deliver the following:

#### Architecture and Design
- Enterprise Windows 11 endpoint lifecycle architecture
- Security, compliance, and access enforcement model
- RBAC and delegated administration model
- Non-production and pilot strategy

#### Enrollment and Provisioning
- Windows Autopilot configuration
- Enrollment Status Page (ESP) design
- Corporate-owned device enrollment model

#### Security and Compliance
- BitLocker, Defender, firewall, and hardening baselines
- Compliance policies and grace periods
- Conditional Access dependency mapping

#### Application Lifecycle
- Win32 app packaging standards
- Required vs. available app strategy
- Supersedence and rollback patterns
- ESP-safe application design

#### Update and Servicing
- Windows Update for Business ring design
- Feature update strategy
- Driver and firmware servicing approach

#### Monitoring and Operations
- Endpoint Analytics integration
- Operational and executive reporting
- Evidence retention model

#### Lifecycle Runbooks
- Autopilot Reset
- Device wipe
- Device reassignment
- Incident isolation
- Hardware replacement
- Decommissioning

#### Governance and Compliance
- RBAC and scope tag implementation
- Access review process
- CIS / NIST / ISO control crosswalk
- Evidence mapping matrix

#### Documentation
- GitHub-ready Markdown documentation
- Executive summary and one-page brief
- Client-owned deliverables

---

### 3.2 Out-of-Scope Services

The following are explicitly out of scope unless added via change order:

- End-user training beyond IT administrators
- Ongoing managed services or help desk support
- Licensing procurement or negotiation
- Third-party MDM/EDR platforms
- Non-Windows endpoint platforms
- Custom application development
- Regulatory certification or attestation

---

## 4. Deliverables

The Provider will deliver:

| Deliverable | Format |
---|---|
| Enterprise architecture documentation | Markdown |
| Operational runbooks | Markdown |
| Compliance crosswalk | Markdown |
| Evidence mapping matrix | Markdown |
| Executive summary | Markdown |
| One-page executive brief | Markdown |

All deliverables become the **property of the Client** upon final payment.

---

## 5. Engagement Structure

### 5.1 Delivery Model

- Fixed-scope, fixed-fee engagement
- Remote delivery unless otherwise agreed
- Weekly status updates
- Milestone-based acceptance

### 5.2 Assumptions

- Client provides required tenant access
- Client assigns a technical point of contact
- Client participates in design reviews
- Client environments meet Microsoft support requirements

Delays caused by unmet assumptions may impact timelines.

---

## 6. Timeline (Estimated)

| Phase | Duration |
---|---|
| Discovery and design | 1–2 weeks |
| Core configuration | 2–3 weeks |
| Validation and pilot | 1–2 weeks |
| Documentation and handoff | 1 week |

Actual timelines depend on client readiness and approvals.

---

## 7. Client Responsibilities

The Client is responsible for:

- Providing timely access and approvals
- Supplying device, identity, and business requirements
- Testing in pilot groups
- Approving deliverables
- Retaining and operating delivered configurations

---

## 8. Change Management

Any changes to scope, assumptions, or deliverables require:

- Written change request
- Impact assessment
- Client approval
- Updated pricing and timeline (if applicable)

No out-of-scope work will be performed without approval.

---

## 9. Fees and Payment

Fees for this engagement are defined in the **Pricing Exhibit** attached to this SOW.

Payment terms:
- Fixed-fee
- Milestone- or schedule-based invoicing
- Net payment terms as defined in the MSA

---

## 10. Acceptance Criteria

Deliverables are accepted when:

- Documentation is delivered as specified
- Configurations align with agreed architecture
- Validation steps are completed
- Client provides written acceptance

Acceptance will not be unreasonably withheld.

---

## 11. Confidentiality and Security

The Provider will:
- Follow least-privilege access
- Avoid retention of client credentials
- Not exfiltrate client data
- Comply with confidentiality obligations under the MSA

---

## 12. Warranty and Disclaimer

The Provider warrants that services will be performed in a professional manner consistent with industry standards.

No guarantee is made regarding:
- Regulatory certification
- Absence of all security incidents
- Future Microsoft platform changes

---

## 13. Term and Termination

This SOW remains effective until completion of services or termination per the MSA.

---

## 14. Signatures

**Client:**  
Name: __________________________  
Title: _________________________  
Date: __________________________  

**Provider:**  
Name: __________________________  
Title: _________________________  
Date: __________________________  

---

