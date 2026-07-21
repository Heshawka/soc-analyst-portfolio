# SOC134 - Suspicious WMI Activity
**Event ID:** 71
**Date:** 2021-03-07 16:50:00 UTC  
**Alert Priority:**  High. An illegitimate file named services.exe is executed on Desktop-Anderson's device. After further investigation, it appears to be a remote access trojan.
**Confidence Level:**  Medium. Initial access to exec.bat remains unknown and should be investigated.
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1059.005 - Command and Scripting Interpreter: Visual Basic | Executes visual basic scripts. |
| T1036 - Masquerading | Uses file named services.exe to look like legitimate software. |

## IOCs

| Type | Value |
|---|---|
| File | exec.bat |
| Hash (SHA256) | be77e6113a985dc305be15ec419411bb840b69f8652d33fa919ae5c797b3ea85 |

## Summary: 

On 2021-03-07 at 16:50:00 UTC, an alert for suspicious WMI activity was found on host machine Desktop-Anderson. A file named exec.bat was executed. VirusTotal and HybridAnalysis confirmed with low confidence that this file was a trojan. After further investigation into Desktop-Anderson's process list using EDR, a suspicious process named services.exe was executed. The legitimate services.exe process is normally stored in the System32 directory. However, the services.exe process on Desktop-Anderson was stored in the Desktop directory, hinting at masquerading and evasion. Additionally, String9 from the extracted string list of this process reveals that this is a remote access trojan. This alert has been deemed a true positive.

## Reasoning:

VirusTotal and HybridAnalysis confirmed that exec.bat was a trojan, although with low confidence. However, the process list found on host machine Desktop-Anderson confirms this behavior. A string extracted from the binary of services.exe mentions a "rat," which confirms this behavior to be a remote access trojan. Additionally, the attacker used a masquerading technique to attempt evasion. This was done by using the file name for the legitimate services.exe to avoid detection. Lastly, the illegitimate services.exe is stored in the desktop directory, which normally is stored in the System32 directory.

## Timeline

| Time (UTC) | Event |
|---|---|
| 2021-03-07 | EDR process list for Desktop-Anderson shows suspicious services.exe process with the following details: 'Path :
 
c:/users/Anderson/desktop/services.exe
Size :
 
2 MB
String1 :
 
go.buildid
String2 :
 
Go build ID:
String3 :
 
json:"pid"
String4 :
 
json:"key"
String5 :
 
json:"agent_time"
String6 :
 
json:"rid"
String7 :
 
json:"ports"
String8 :
 
json:"agent_platform"
String9 :
 
rat.New'. |

## Attack Detail: 

The attack chain remains unclear. There were no other telemetry found through EDR other than the process list on Desktop-Anderson. Initial access to the exec.bat remains unclear and requires further investigation. Once this file was downloaded, it was executed on host machine Desktop-Anderson. There is evidence of remote access trojan behavior, which is further explained in the Reasoning section.

## Actions Taken:
-Checked exec.bat's hash against VirusTotal and HybridAnalysis. Only 1 security vendor on VirusTotal marked exec.bat as a trojan, and the reports on HybridAnalysis mark it only as suspicious.
-Checked logs tied to Desktop-Anderson (172.16.17.54). No logs were found near the time of the incident.
-Checked Desktop-Anderson endpoint using EDR. Found highly suspicious process named services.exe with the following information:

Path :
 
c:/users/Anderson/desktop/services.exe
Size :
 
2 MB
String1 :
 
go.buildid
String2 :
 
Go build ID:
String3 :
 
json:"pid"
String4 :
 
json:"key"
String5 :
 
json:"agent_time"
String6 :
 
json:"rid"
String7 :
 
json:"ports"
String8 :
 
json:"agent_platform"
String9 :
 
rat.New

Services.exe is normally stored in the System32 folder, meaning this is an attempt at masquerading what appears to a remote access trojan. This lines up with the security vendor on VirusTotal that deemed exec.bat as a trojan.
-Checked email security for emails tied to Desktop-Anderson. No emails near the time of the incident were found.
-Quarantined Desktop-Anderson.
-Escalated to L2.


## Recommended Next Steps:
-Clean exec.bat from host machine Desktop-Anderson. 
-Interview Anderson for the source of exec.bat.
-Once the source of exec.bat is found, use blacklist as needed.
