# SOC127 - SQL Injection Detected
**Event ID:** 60
**Date:** 2021-02-14 04:36:00 UTC  
**Alert Priority:**  
**Confidence Level:**  
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1105 (Ingress Tool Transfer) | Download of external payload (payload_1.ps1) over the network. |
| T1059.001 (Command and Scripting Interpreter: PowerShell) | Target file is a .ps1 script. |

## IOCs

| Type | Value |
|---|---|
| File | AnyDesk.exe |
| Hash (SHA256) | 6f4a78da5c19afba57637bd344213d5ff55fb69dc343d6a6c79b0696ce53eaa0 |
| Domain | boot-01.net.anydesk.com |
| Domain | relay-61e0b722.net.anydesk.com |
| IP | 134.119.217.177 |
| IP | 146.0.234.85 |
 
## Summary: 

## Reasoning:

## Timeline

| Time (UTC) | Event |
|---|---|
| 2021-01-01 17:36:00 | Firewall log shows connection from DanielPRD (172.16.17.33) to boot-01.net.anydesk.com (134.119.217.177). |
| 2021-01-01 17:37:00 | Firewall log shows connection from DanielPRD (172.16.17.33) to relay-61e0b722.net.anydesk.com (146.0.234.85). |
 

## Attack Detail: 

## Actions Taken:
-reviewed

## Recommended Next Steps:
