# LetsDefend Write-Ups

Alert triage and documentation from my SOC analyst training on LetsDefend, 
a hands-on platform simulating real SOC alert investigation. Each write-up follows a consistent 
analyst template: priority/confidence assessment, MITRE ATT&CK mapping, timeline, attack chain 
detail, actions taken, and recommended next steps — mirroring how findings would be documented 
and handed off in a real SOC environment.

## Polished Write-Ups

| Alert | Category | Verdict | Priority |
|---|---|---|---|
| [SOC108 - Malicious Remote Access Software](./polished/SOC108 Malicious Remote Access Software.md) | Remote Access Software | False Positive | Medium |
| [SOC153 - Suspicious PowerShell Script](./polished/SOC153 Suspicious Powershell Script Executed.md) | PowerShell / C2 / Data Exfiltration | True Positive | High |

## Drafts

Additional alert write-ups in progress are available in [`drafts/`](./drafts/) — these represent 
earlier work in the documentation process and haven't yet been cleaned up for portfolio 
presentation, but reflect ongoing volume and consistency of practice.

## Template

Every write-up follows this structure:
- **Alert Priority** — stated with reasoning, not just the platform-assigned value
- **Confidence Level** — tied explicitly to supporting evidence
- **MITRE ATT&CK Mapping** — including alerts that were false positives (mapped to the 
  technique the alert pattern resembled, with an explicit caveat)
- **Summary / Reasoning / Timeline / Attack Detail**
- **Actions Taken** — investigative steps performed at L1 scope
- **Recommended Next Steps** — including explicit escalation to L2/IR where appropriate