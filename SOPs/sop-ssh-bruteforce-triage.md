# SOP — SSH Brute-Force Triage

**Applies to:** Failed-authentication threshold alerts on Linux hosts.
**Related MITRE:** T1110.001 — Brute Force: Password Guessing.

## Steps
1. **Identify the source.** Extract the source IP. Determine internal vs.
   external and resolve it against inventory.
2. **Count outcomes.** In the alert window, count failed vs. successful
   authentications (KQL / SPL).
3. **Assess pattern.** Successful auth following a failure spike -> treat as
   possible compromise. Failures only -> likely blocked attempt.
4. **Enrich the source.** Internal inventory for internal IPs; reputation
   sources (VirusTotal, AbuseIPDB) for external.
5. **Check post-auth activity.** If any success, review subsequent activity on
   the target host for signs of hands-on-keyboard.
6. **Decide and record.** Assign verdict, map to MITRE, and invoke
   [[playbook-bruteforce-response]] if confirmed true positive.

## Decision quick-reference
| Observation                        | Likely verdict        |
|------------------------------------|-----------------------|
| Failures only                      | Attempt / blocked     |
| Failures then success (same IP)    | Possible compromise   |
| External IP + success              | Escalate immediately  |
