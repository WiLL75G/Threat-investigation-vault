# Evidence — KQL Queries (CASE-001)

Queries run against Log Analytics (Syslog table) during the investigation.

## Failed vs. successful SSH authentications by source
```kql
Syslog
| where Facility == "auth" or ProcessName == "sshd"
| where SyslogMessage has "192.168.64.15"
| extend Outcome = case(
    SyslogMessage has "Failed password", "Failed",
    SyslogMessage has "Accepted password", "Success",
    "Other")
| summarize Count = count() by Outcome
```

**Result:** Failed = 88, Success = 8

> Note: adapt table/column names to match your actual DCR schema and the
> exact query used in the Day 5 hunt. Paste the real query here and drop the
> Sentinel screenshot alongside it.
