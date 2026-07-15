# SOC147 - SSH Scan Activity  
**Event ID:** 94  
**Date:** 2021-06-13 16:23:00 UTC  
**Alert Priority:**  Low.
**Confidence Level:**  High.
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1595 - Active Scanning| Probing the network infrastructure using Nmap. |

## Summary: 

On 2021-06-13 at 16:23:00 UTC, SSH scan activity was detected from PentestMachine (172.16.20.5) using Nmap. This was confirmed to be planned penetration testing by elli@letsdefend.io in her email 2 days prior to the incident. This alert has been deemed a false positive.

## Reasoning:

An email was received 2 days prior to the alert confirming a planned network scanning using Nmap. This and the source hostname, PentestMachine, indicates a false positive.

## Timeline

| Time (UTC) | Event |
|---|---|
| 2021-06-11 09:11:00 UTC | Email sent from elli@letsdefend.io describing a planned network scanning on June 13. |

## Attack Detail: 

No attack chain present - Ellie is performing a planned network scanning using Nmap.

## Actions Taken:
-Checked has of nmap file against VirusTotal. VirusTotal confirms it is a legitimate instance of the official Nmap security scanner. 
-Checked email security to rule out planned penetration testing. On 2021-06-11 at 09:11:00 UTC, there was an email sent from elli@letsdefend.io to soc@letsdefend.io, with subject "Planned Scanning." The email describes a planned scanning of the LetsDefend netwrok after 12:00 on June 13, specifically from PentestMachine. This confirms planned testing and a false positive alert.  

## Reccommended Next Steps:

- Consider a temporary allowlist/suppression rule for PentestMachine (172.16.20.5) for the duration of announced pentest windows, to reduce alert noise on future authorized scans.
- Confirm with Elli/security team whether a formal pentest notification process exists (e.g., a shared calendar or ticket system SOC can reference), so future scans can be verified faster without relying on searching email history.
- No further action needed — confirmed authorized activity, no compromise indicators present.