# Playbook — Brute-Force Response

**Invoked when:** SSH brute-force confirmed as a true positive with successful
authentication.

## Containment
- [ ] Block the source IP at the host/network boundary (if external).
- [ ] Disable or force-reset the compromised account(s).
- [ ] Isolate the target host if hands-on-keyboard activity is suspected.

## Eradication
- [ ] Review authorized keys and sudoers for tampering.
- [ ] Check for persistence (new users, cron, systemd units).

## Recovery
- [ ] Restore account access with new credentials / key rotation.
- [ ] Confirm the host is clean before returning to service.

## Post-incident
- [ ] Confirm the detection rule fired correctly; tune thresholds if needed.
- [ ] Record IOCs in the global artifact index.
- [ ] Finalize the report (see [report template](../templates/template-report.md)).
