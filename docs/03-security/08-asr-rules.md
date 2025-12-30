# Attack Surface Reduction (ASR) Rules  
**Exploit Mitigation and Abuse Prevention**

---

## Purpose

This document defines the **authoritative Attack Surface Reduction (ASR) strategy** for Windows 11 endpoints.

ASR rules are a **preventive security control** designed to:
- Block common malware and attacker techniques
- Reduce exploitability of trusted applications
- Enforce least functionality at the process level

ASR complements, but does not replace, antivirus or EDR.

---

## ASR Design Objectives

The ASR implementation must ensure:

1. **Prevention over detection**
2. **Predictable enforcement**
3. **Low false-positive rate**
4. **Progressive rollout**
5. **Auditability and evidence**

---

## ASR Policy Deployment  
**Exact UI Click-Path**

### Intune admin center
→ Endpoint security
→ Attack surface reduction
→ Create policy
→ Attack surface reduction rules
→ Windows 10 and later


---

## ASR Enforcement Strategy

### Phased Rollout Model (Mandatory)

| Phase | Mode | Target |
---|---|---|
| Phase 1 | Audit | Pilot devices |
| Phase 2 | Block | Pilot devices |
| Phase 3 | Block | Production devices |

**Rule**  
No ASR rule moves directly to production **Block** without audit validation.

---

## ASR Rule Baseline (Authoritative)

The following ASR rules are **required** for production unless explicitly documented as exceptions.

### Core Exploit and Abuse Protections

| ASR Rule | Mode | Rationale |
---|---|---|
| Block Office apps from creating child processes | Block | Prevent macro abuse |
| Block Office apps from creating executable content | Block | Prevent payload staging |
| Block Office apps from injecting code | Block | Prevent process injection |
| Block credential stealing from LSASS | Block | Protect credentials |
| Block process creations from PSExec and WMI | Block | Lateral movement prevention |
| Block executable content from email and webmail | Block | Initial access prevention |
| Block untrusted and unsigned processes from USB | Block | Removable media risk |
| Block abuse of exploited vulnerable signed drivers | Block | Kernel protection |

---

### Script and Interpreter Controls

| ASR Rule | Mode | Rationale |
---|---|---|
| Block JavaScript or VBScript from launching executables | Block | Script-based malware |
| Block Win32 API calls from Office macros | Block | Macro abuse |
| Block persistence through WMI event subscriptions | Block | Persistence prevention |

---

## Recommended Audit-First Rules

These rules may require **extended auditing** before enforcement depending on environment maturity.

| ASR Rule | Initial Mode | Notes |
---|---|---|
| Block credential stealing via browser APIs | Audit | Browser compatibility |
| Block process injection via dynamic code | Audit | LOB app impact |
| Block use of remote admin tools | Audit | IT workflows |

---

## Exclusions and Exceptions

### Governance Rules

- Exclusions must be **rare and documented**
- Exclusions require:
  - Business justification
  - Security approval
  - Scope limitation (app-specific)
- Broad path-based exclusions are prohibited

### Acceptable Exclusion Examples

- Digitally signed, vendor-supported LOB applications
- Documented legacy tools under decommission plan

---

## ASR Assignment Strategy

| Target | Assignment |
---|---|
| Pilot Devices | ASR-W11-Pilot |
| Production Devices | ASR-W11-Prod |
| Break-glass Devices | Explicit exclusion (rare) |

**Rule**
ASR policies are assigned to **devices**, not users.

---

## Enforcement Order

1. Security baseline applies
2. Defender AV policy applies
3. ASR policy applies
4. ASR events generated
5. EDR telemetry correlates activity
6. Compliance state updated (where applicable)

---

## Monitoring and Validation

### Where to Monitor

| Signal | Location |
---|---|
| ASR Audit Events | Defender portal |
| ASR Block Events | Defender portal |
| App Impact | Endpoint Analytics |
| False Positives | SOC workflow |

---

### Validation Checklist

- [ ] ASR rules applied successfully
- [ ] Audit events reviewed
- [ ] No widespread false positives
- [ ] Block mode enforced in production
- [ ] Exclusions documented and approved

---

## Failure Modes and Mitigation

| Issue | Cause | Mitigation |
---|---|---|
| App blocked | Legitimate behavior | Review and narrowly exclude |
| High alert volume | Overly aggressive rule | Audit-first rollout |
| User disruption | Legacy workflows | Refactor workflows |
| Policy conflict | Multiple ASR profiles | Consolidate policies |

---

## Evidence Artifacts

| Artifact | Source |
---|---|
| ASR policy configuration | Intune |
| Audit/block events | Defender portal |
| Exception approvals | Change records |
| Compliance impact | Intune reports |

---

## Change Control

ASR rule changes:
- Require security approval
- Must be validated in Audit mode first
- Must be logged in the Decision Log
- Must include rollback plan

---

## Summary

ASR rules dramatically reduce the attack surface by **blocking entire classes of attacks** before they execute.

Correctly implemented ASR makes exploitation **difficult, noisy, and costly** for attackers.

---

## Next File

Proceed to:

**`docs/03-security/09-firewall.md`**

This file defines **host-based firewall enforcement and network isolation controls**.
