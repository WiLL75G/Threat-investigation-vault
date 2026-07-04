---
case_id: CASE-001
title: SSH Brute-Force Against Linux Syslog Host
status: closed
severity: high
analyst: James (@WilliamInCyber)
opened: 2026-06-XX
closed: 2026-06-XX
mitre_techniques: [T1110.001]
---

# CASE-001 — SSH Brute-Force Against Linux Syslog Host

## Summary
Sustained SSH brute-force from a single internal source against a monitored
Linux host; 8 successful authentications following 88 failed attempts,
indicating a completed credential-guessing attack.

## Alert Source
- Platform: Microsoft Sentinel
- Rule: Custom analytics rule (failed-authentication threshold)
- Pipeline: Linux Syslog -> Azure Arc -> AMA -> DCR -> Log Analytics
- Initial alert time: <!-- fill from lab -->

## Artifacts
| Type | Value          | Enrichment                | Verdict  |
|------|----------------|---------------------------|----------|
| IP   | 192.168.64.15  | Internal / lab (RFC1918)  | Attacker |
| Host | Attacker-Tier4 | Known Kali Linux VM       | Source   |

Linked notes:
- [192.168.64.15](artifacts/ip-192.168.64.15.md)
- [Attacker-Tier4](artifacts/host-attacker-tier4.md)

## Triage Notes
1. Confirmed source IP `192.168.64.15` — internal lab range, maps to the
   Kali attacker VM (`Attacker-Tier4`).
2. Counted authentication outcomes in the alert window via KQL:
   **88 failed**, **8 successful**.
3. Success following a failure spike -> treated as possible compromise, not noise.
4. Verified the target host was the intended lab victim.

## Findings
88 failed SSH logins and 8 successful logins originated from 192.168.64.15
within the alert window. The success burst immediately following sustained
failures is the signature of a completed brute-force with credential
compromise. Confirmed as a controlled lab simulation.

## MITRE ATT&CK
- T1110.001 — Brute Force: Password Guessing

## SOP Followed
[SSH Brute-Force Triage SOP](../../SOPs/sop-ssh-bruteforce-triage.md)

## Actions Taken
- [x] Confirmed source and outcome counts
- [x] Mapped to MITRE T1110.001
- [x] Documented as detection validation
- [x] Produced report

## Outcome
**True positive** (lab-simulated). Detection pipeline and analytics rule
validated end-to-end against real telemetry.

## Report
[Investigation Report](report.md)
