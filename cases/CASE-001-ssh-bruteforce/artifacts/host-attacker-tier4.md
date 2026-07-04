---
artifact_type: host
value: Attacker-Tier4
first_seen: CASE-001
related_cases: [CASE-001]
verdict: internal
---

# Artifact — Attacker-Tier4

## Value
`Attacker-Tier4` (192.168.64.15)

## Context
Kali Linux VM used as the attack source in CASE-001. Ran the SSH
brute-force against the monitored Linux Syslog host.

## Enrichment
| Source             | Result                     | Date |
|--------------------|----------------------------|------|
| Internal inventory | Known lab attacker machine |      |

## Related Cases
- [CASE-001](../case.md)

## Verdict
Internal / attacker VM.
