# Remediation Workflows  
**Non-Compliance Handling, Automated Recovery, and Escalation Paths**

---

## Purpose

This document defines the **authoritative remediation workflows** for Windows 11 devices that fall out of compliance.

 offering a structured, repeatable response to non-compliance that:

- Restores devices to a trusted state where possible
- Prevents insecure devices from accessing resources
- Eliminates ambiguous “limbo” states
- Produces clear operational and audit evidence

Remediation is **not optional**.  
A device that cannot be remediated **must be removed from production**.

---

## Remediation Design Principles

1. **Automate first**
2. **Limit human intervention**
3. **Fail closed**
4. **Prefer rebuild over repair**
5. **Escalate decisively**
6. **Record evidence at every step**

---

## Compliance Failure Classification

Non-compliance events are categorized to determine the appropriate response.

### Category A — Automatically Remediable

| Example Signal | Cause |
---|---|
| BitLocker disabled | Policy drift |
| Defender real-time protection off | Service stopped |
| Firewall disabled | User or software change |
| OS slightly behind | Update deferral expired |

**Response**
- Automated remediation
- Grace period applies

---

### Category B — Conditionally Remediable

| Example Signal | Cause |
---|---|
| EDR not reporting | Sensor failure |
| ASR rules failing | App conflict |
| Update failures | Driver or disk issue |

**Response**
- Automated remediation attempt
- Limited investigation window
- Escalation if unresolved

---

### Category C — Non-Remediable / High Risk

| Example Signal | Cause |
---|---|
| TPM unavailable | Hardware failure |
| Secure Boot disabled | Firmware change |
| Repeated remediation failure | Persistent drift |
| Active high-risk Defender alert | Suspected compromise |

**Response**
- Immediate access block
- Device reset or wipe
- Possible hardware replacement

---

## Automated Remediation Workflow

### Trigger

- Compliance policy evaluates device as **Non-Compliant**

---

### Workflow Steps

1. Device reports state to Intune
2. Compliance policy flags failure
3. Remediation policies reapply automatically
4. Device attempts self-healing
5. Compliance re-evaluated

---

### Grace Period Handling

| Setting | Value |
---|---|
| Grace period | 3 days (recommended) |
| Access during grace | Allowed |
| User notification | Optional |
| Remediation retries | Continuous |

> Grace periods are a **temporary tolerance**, not an override.

---

## Access Enforcement During Remediation

| Device State | Access |
---|---|
| Compliant | Allowed |
| Non-compliant (within grace) | Allowed |
| Non-compliant (grace expired) | Blocked |
| High-risk / Category C | Immediately blocked |

Access control is enforced exclusively through **Conditional Access**.

---

## Manual Intervention Workflow

Manual intervention is permitted **only after automated remediation fails**.

### Approved Manual Actions

| Action | Purpose |
---|---|
| Device sync | Force policy refresh |
| Log review | Root cause analysis |
| Autopilot Reset | Rebuild without full re-registration |
| Full wipe | Cryptographic reset |

### Prohibited Actions

- Manual registry edits
- Local policy changes
- Disabling security features
- Temporary CA exclusions

---

## Escalation Path

```mermaid
flowchart TD
  A["Device Non-Compliant"] --> B{"Auto-remediable?"}
  B -->|Yes| C["Automated remediation"]
  C --> D{"Compliant?"}
  D -->|Yes| E["Restore access"]
  D -->|No| F{"Grace expired?"}
  F -->|No| C
  F -->|Yes| G["Access blocked"]
  B -->|No| H["Immediate access block"]
  H --> I["Reset or wipe"]
