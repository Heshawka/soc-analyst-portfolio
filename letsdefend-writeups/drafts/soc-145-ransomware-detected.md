# SOC145 - Ransomware Detected
**Event ID:** 92
**Date:** 2021-05-23 19:32:00 UTC  
**Alert Priority:**  High. Ransomware has been executed on MarkPRD's machine. Initial access to ab.exe is unknown and further investigation is required.
**Confidence Level:**  Medium. The only source of low confidence is the initial access to ab.exe. Interview Mark to find the source of initial access.
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1490 - Inhibit System Recovery | Deleting of Windows Volume shadow copies observed in VirusTotal sample [1228d0f04f0ba82569fc1c0609f9fd6c377a91b9ea44c1e7f9f84b2b90552da2] |
| T1140 - Deobfuscate/Decode Files or Information | Decodes data using Base64 via WinAPI. |
| T1562.001 - Disable or Modify Tools | Disables user access control. |
| T1486 - Data Encrypted for Impact | Renames 127 files by appending the extension '.cbcaaeacad,' modifies user documents, and writes a ransom note. |

## IOCs

| Type | Value |
|---|---|
| File | ab.exe |
| Hash (SHA256) | 1228d0f04f0ba82569fc1c0609f9fd6c377a91b9ea44c1e7f9f84b2b90552da2 |
 
## Summary: 

On 2021-05-23 at 19:32:00 UTC, a ransomware file named ab.exe was detected on MarkPRD's endpoint. EDR indicates that the file was executed, but with no event time or other EDR telemetry present due to no agent being installed. After analyzing ab.exe on VirusTotal and HybridAnalysis, it was confirmed that ab.exe is indeed ransomware with high confidence. After checking logs and emails to find the source of ab.exe, no anomalous activity was found, thus initial access remains unclear. This alert has been deemed a true positive.

## Reasoning:

VirusTotal and HybridAnalysis confirmed ab.exe to be ransomware with high confidence. Additionally, EDR has confirmed execution of the ransomware and thus encryption of MarkPRD's files. Further investigation of the source of ab.exe is advised. Remediation of ransomware and its effects on MarkPRD's endpoint is advised. 

## Timeline

| Time (UTC) | Event |
|---|---|
| 2021-05-23 19:XX:00 UTC | EDR indicates ab.exe was executed on MarkPRD's machine. |
| 2021-05-23 19:32:00 UTC | Ransomware detected on MarkPRD's endpoint - ab.exe. |
 

## Attack Detail: 

The attack chain remains unclear. No logs or events tied to MarkPRD's endpoint were found due to no agent being installed. No anomalous emails were found near the time of the incident. Thus, initial access to ab.exe remains unclear and should be investigated. Once the file was downloaded on MarkPRD's endpoint, it was executed. No logs or events indicate contact with a C2 address.

## Actions Taken:
-Checked ab.exe's hash against VirusTotal and HybridAnalysis. 59 security vendors on VirusTotal confirm malicious intent, specifically as a ransomeware-as-a-service in the avaddon/delshad malware families. HybridAnalysis confirms detection of ransomware with high confidence.
-Checked MarkPRD's endpoint (172.16.17.88) using EDR. No agents were installed for network actions, terminal history, or browser history. However, process history indicates execution of ab.exe on MarkPRD's endpoint with no event times present.
-Checked logs tied to MarkPRD's endpoint. No anomalous network activity was found near the time of the incident. 
-Checked emails tied to Mark's account. No emails related to the incident were found.
-Contained and isolated MarkPRD endpoint.
-Escalated to L2.

## Recommended Next Steps:
-Do not power MarkPRD's machine in order to preserve volatile memory needed for investigation. 
-Investigate the source of ab.exe by interviewing Mark.
-Interview Mark to see if ransom was paid.