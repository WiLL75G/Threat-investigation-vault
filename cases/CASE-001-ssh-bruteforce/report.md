# Investigation Report — CASE-001

**Analyst:** James (@WilliamInCyber)
**Date:** 2026-06-XX
**Severity:** High
**Status:** Closed — True Positive (lab-simulated)

## Executive Summary
A single internal source conducted an SSH brute-force against a monitored
Linux host, producing 88 failed logins followed by 8 successful
authentications. The success burst following sustained failures confirms a
completed credential-guessing attack. Detected end-to-end through the
Sentinel pipeline; used to validate the custom analytics rule.

## Findings
- Source: `192.168.64.15` (`Attacker-Tier4`), internal Kali VM.
- 88 failed and 8 successful SSH authentications in the alert window.
- Pattern consistent with brute-force leading to credential compromise.
- Telemetry path: Linux Syslog -> Azure Arc -> AMA -> DCR -> Log Analytics -> Sentinel.

## Indicators of Compromise
| Type | Value          | Verdict          |
|------|----------------|------------------|
| IP   | 192.168.64.15  | Internal/attacker|
| Host | Attacker-Tier4 | Source           |

## MITRE ATT&CK Mapping
- T1110.001 — Brute Force: Password Guessing

## Recommendations
- Enforce key-based SSH auth and disable password login where possible.
- Rate-limit / lock out repeated failures (e.g. fail2ban).
- Keep the failed-auth threshold rule active; review threshold periodically.

## Detection Notes
The custom analytics rule fired correctly on the failure threshold. The
failures-then-success sequence is the strongest signal — a future tuning
iteration could raise severity specifically when a success follows a
failure spike from the same source.
