# SOC137 - Malicious File/Script Download Attempt
 
**Event ID:** 76
**Date:** 2021-03-14 19:15:00 UTC
**Alert Priority:** High
**Confidence Level:** High
 
---
 
## MITRE ATT&CK Techniques
 
| Technique | Reasoning |
|---|---|
| T1566.001 - Phishing: Spearphishing Attachment | Malicious document delivered via email from aaronluo@cmail.carleton.ca to nicolas@letsdefend.io. |
| T1204.002 - User Execution: Malicious File | Nicolas opens the `ALLEGATO_FT_del_20-06-2019.xls` attachment, triggering the malicious macro chain. |
| T1059.005 - Command and Scripting Interpreter: Visual Basic | VBA macros embedded in `ALLEGATO_FT_del_20-06-2019.xls` used to obfuscate, attempt persistence, disable alerts, manipulate macro security settings, and execute external applications. |
| T1027 - Obfuscated Files or Information | Heavily obfuscated PowerShell command (mixed case, string concatenation, character codes, Base64-encoded/compressed payload) executed via the macro. |
| T1059.001 - Command and Scripting Interpreter: PowerShell | Obfuscated PowerShell command executed with `-ExecutionPolicy Bypass`, `-NoProfile`, and `-WindowStyle Hidden` flags to decode and run an in-memory payload. |
| T1218.011 - System Binary Proxy Execution: Rundll32 | `rundll32.exe` used to execute `oo2ofzo5.dll` via `DllRegisterServer`, likely to register/load the dropped payload while evading detection. |
| T1071.001 - Application Layer Protocol: Web Protocols | HTTPS/HTTP beaconing from the host to `iluuryeqa.info` and `ueba6ka.club` via `powershell.exe`. |
| T1105 - Ingress Tool Transfer | `INVOICE PACKAGE LINK TO DOWNLOAD.docm` (opened a week later) attempts to use PowerShell to download an additional file from a remote location; download was blocked by AV. |
 
---
 
## IOCs
 
| Type | Value |
|---|---|
| File | `INVOICE PACKAGE LINK TO DOWNLOAD.docm` |
| Hash (SHA256) | `08d4fd5032b8b24072bdff43932630d4200f68404d7e12ffeeda2364c8158873` |
| File | `ALLEGATO_FT_del_20-06-2019.xls` |
| Hash (SHA256) | `8b84bbf5fee07dd41cfaecbc527da1fed3bcf4adab2541a00f55422093f216fb` |
| File | `oo2ofzo5.dll` |
| Path | `C:\Users\Nicolas\AppData\Local\Temp\oo2ofzo5.dll` |
| Domain | `iluuryeqa.info` |
| URL | `hxxp://ueba6ka.club/favicon.ico` |
| URL | `hxxp://ueba6ka.club/images/DVeUkINudhi79z0c_2Bv/hcMjSPUhHNICgDZ2eJc/uPkHWXvBmVjikkuyor3cnx/gi3BCr71LrlRP/OOmOS8_2/Bl7A_2Fjz2BM4Pth4RZbBKn/1OVxs19bE9/6wtE2QLgVO1DP1TCF/SoIEOJUXIYbo/RtuJbNDFWW5/V.avi` |
| IP | `49.51.12.195` |
| IP | `31.214.157.60` |
| Sender Email | `aaronluo@cmail.carleton.ca` |
| Recipient Email | `nicolas@letsdefend.io` |
| Hostname | `NicolasPRD` |
| Internal IP | `172.16.17.37` |
 
---
 
## Summary
 
On 2021-03-14 at 19:15:00 UTC, a malicious file/script download attempt was detected and blocked on host **NicolasPRD**. The blocked file, `INVOICE PACKAGE LINK TO DOWNLOAD.docm`, exhibits signs of a maldoc containing malicious macros. 39 security vendors on VirusTotal flagged the file as malicious, and HybridAnalysis confirms detection by CrowdStrike Static Analysis and ML with high confidence.
 
Investigation into the source of this alert identified a related, earlier compromise on the same host. On 2021-03-07 at 15:45:00 UTC, an email with the subject "Invoice" was sent from `aaronluo@cmail.carleton.ca` to `nicolas@letsdefend.io`, containing the attachment `ALLEGATO_FT_del_20-06-2019.xls`. This file is also a confirmed maldoc using VBA macros to obfuscate code, attempt persistence, disable security alerts, manipulate macro security settings, and execute external applications.
 
When Nicolas opened this attachment, the embedded macro launched a heavily obfuscated PowerShell command that decoded and executed an in-memory payload, followed by execution of a dropped DLL (`oo2ofzo5.dll`) via `rundll32.exe`. The host then beaconed out to two external domains/IPs over HTTPS and HTTP. One week later, on 2021-03-14, a second malicious document (`INVOICE PACKAGE LINK TO DOWNLOAD.docm`) attempted to download an additional file via PowerShell but was successfully blocked by AV before execution.
 
Given the one-week gap between the initial macro-based compromise and the second download attempt on the same host, this activity is assessed as a likely continuation of the same intrusion/campaign rather than two unrelated events, possibly an attacker returning to deploy a secondary payload or maintain access.
 
---
 
## Reasoning
 
- The initial email and attached `.xls` maldoc match a classic macro-based delivery chain: phishing → user execution → obfuscated VBA → obfuscated PowerShell → payload execution → C2 beaconing.
- The use of `-ExecutionPolicy Bypass`, `-WindowStyle Hidden`, and `-NonInteractive` flags, along with heavy string obfuscation and a Base64/DEFLATE-compressed payload, is consistent with known maldoc-to-PowerShell delivery techniques (e.g., Emotet/TrickBot-style loaders).
- `rundll32.exe` executing a DLL from a user's `Temp` directory via `DllRegisterServer` is a common technique to proxy execution through a trusted system binary and evade basic detections.
- The recurrence of malicious document activity on the same host one week later, this time blocked, suggests either persistence from the initial compromise or a repeat targeting attempt against the same user/machine.
- Lack of EDR telemetry on NicolasPRD (agent error) limited visibility into process execution and network activity for the initial incident, and increases the likelihood that additional undetected activity may have occurred between 2021-03-07 and 2021-03-14.
---
 
## Timeline
 
| Time (UTC) | Event |
|---|---|
| 2021-03-07 15:45:00 | Phishing email sent from `aaronluo@cmail.carleton.ca` to `nicolas@letsdefend.io`, subject "Invoice," with attachment `ALLEGATO_FT_del_20-06-2019.xls` (SHA256: `8b84bbf5fee07dd41cfaecbc527da1fed3bcf4adab2541a00f55422093f216fb`). |
| 2021-03-07 16:12:00 | Obfuscated PowerShell command executed via WMI (`wmic process call create`) using `-ExecutionPolicy Bypass`, `-NoProfile`, `-WindowStyle Hidden` to decode and run a Base64/DEFLATE-compressed in-memory payload. |
| 2021-03-07 16:13:00 | Follow-up execution of the decoded PowerShell payload. |
| 2021-03-07 16:14:00 | `rundll32.exe` executes `C:\Users\Nicolas\AppData\Local\Temp\oo2ofzo5.dll` via `DllRegisterServer`. |
| 2021-03-07 16:50:00 | Proxy logs show an HTTPS connection from Nicolas (`172.16.17.37`) to `iluuryeqa.info` (`49.51.12.195`) via `powershell.exe`. |
| 2021-03-07 16:54:00 | Proxy logs show an HTTP connection from Nicolas (`172.16.17.37`) to `hxxp://ueba6ka.club/images/.../V.avi` at `31.214.157.60`. |
| 2021-03-07 16:54:00 | Proxy logs show an HTTP connection from Nicolas (`172.16.17.37`) to `hxxp://ueba6ka.club/favicon.ico` at `49.51.12.195`. |
| 2021-03-14 19:15:00 | `INVOICE PACKAGE LINK TO DOWNLOAD.docm` (SHA256: `08d4fd5032b8b24072bdff43932630d4200f68404d7e12ffeeda2364c8158873`) attempts to run a PowerShell command to download a remote file; download blocked by AV. |
 
---
 
## Attack Detail
 
The attack began with a phishing email delivering a macro-enabled Excel document. Upon opening, the VBA macro invoked an obfuscated PowerShell one-liner via WMI process creation, bypassing execution policy and hiding the window from the user. This command decoded a compressed, Base64-encoded payload directly in memory (a common technique to avoid writing an easily-scannable script to disk) and executed it. Shortly after, `rundll32.exe` was used to load a dropped DLL, likely as a means of establishing the next stage of the payload or a proxy-execution technique to blend in with legitimate system activity. The infected host then communicated with two external domains over HTTPS and HTTP, consistent with C2 check-in or secondary payload staging.
 
One week later, a second malicious Word document (`.docm`) landed on the same host and attempted to use PowerShell to download an additional file from a remote location. This attempt was blocked by AV before the download or execution could complete, preventing a potential reinfection or delivery of a new payload.
 
---
 
## Actions Taken
 
- Checked `INVOICE PACKAGE LINK TO DOWNLOAD.docm` against VirusTotal and HybridAnalysis; both confirmed malicious intent to execute a PowerShell command to download a file from a remote location.
- Investigated email security logs to identify the source of the maldoc; identified the 2021-03-07 phishing email from `aaronluo@cmail.carleton.ca` with attachment `ALLEGATO_FT_del_20-06-2019.xls`, confirmed malicious via VirusTotal (VBA used to obfuscate, execute external applications, disable alerts/screen updating, and manipulate macro security settings).
- Reviewed logs on NicolasPRD related to both the March 7th email and the `.docm` file; no host logs were found for the `.docm` file, but 3 relevant proxy log entries were identified for March 7th (see Timeline).
- Reviewed NicolasPRD via EDR; no process or network telemetry was available due to an agent error, though suspicious commands were recovered from terminal history (see Timeline).
- Quarantined hostname NicolasPRD to contain further activity.
- Escalated to L2 for further investigation and remediation.
---
 
## Recommended Next Steps
 
1. **Full forensic imaging/triage** of NicolasPRD to recover process execution history, memory artifacts, and any additional dropped files, given the EDR agent failure during the initial incident.
2. **Investigate and remediate the EDR agent error** on NicolasPRD to restore telemetry and confirm no other hosts are similarly blind.
3. **Block IOCs** (`iluuryeqa.info`, `ueba6ka.club`, `49.51.12.195`, `31.214.157.60`) at the firewall/proxy and email gateway, and hunt across the environment for any other hosts communicating with these indicators.
4. **Search the environment** for the file hash of `oo2ofzo5.dll` and the two document hashes to identify any other affected hosts.
5. **Review mailbox rules and sent-mail activity** for `nicolas@letsdefend.io` to rule out lateral phishing or account compromise.
6. **Block/flag the sender domain** `cmail.carleton.ca` pending further review, and search for other emails from this sender across the organization.
7. **User awareness follow-up** with Nicolas regarding macro-enabled attachment risks, given two separate malicious documents were opened/received within a week.
8. **Reimage NicolasPRD** if forensic findings confirm successful payload execution and persistence beyond what's currently documented.