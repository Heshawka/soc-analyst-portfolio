SOC106 - Found Suspicious File - TI Data
Event ID: 17
2020-9-22 11:10:00 UTC
Add some stuff 
 
Summary: On 2020-9-22 at 11:10:00 UTC, a file marked as malicious named ChromeSetup.exe caused an alert on ChanProd's device. This file is a legitimate installer but was cleaned by the AV, making this a false positive. The specific AV detection signature/heuristic that triggered this alert was not visible in the available logs [confirm — check if detection name is visible in your AV console]. Given the file was confirmed non-malicious across three independent sandboxes, this is consistent with a heuristic/behavioral false-positive rather than a signature match on known-bad content — but without the specific detection name, the root cause of the AV flag can't be conclusively determined here.

Reasoning: ChromeSetup.exe was analysed using VirusTotal, Anyrun, and HybridAnalysis. All sandboxes deemed this file as non-malicious, but had several suspicious indicators. However, these indicators are in line with that of a normal installer. Additionally, no further malicious processes were created, in accordance with EDR. No files have been scheduled to start on startup.

Timeline - Time (UTC) | Event

2020-09-22 11:10:00 UTC - Alert fired, found suspicious ChromeSetup.exe on ChanProd's device.

2020-09-22 11:12:00 UTC - Chrome installer run at 11:12:00 UTC at c:/program files (x86)/google/update/install/85.0.4183.102_chrome_installer.exe.

Attack Detail: 

No attack chain present — ChromeSetup.exe is a legitimate Google Chrome installer. Execution followed expected installer behavior (initial setup executable spawning the versioned installer binary from Program Files), with no anomalous network activity, no persistence mechanism creation, and no process injection observed

Actions Taken:

-Checked ChromeSetup.exe against VirusTotal, HybridAnalysis, and Anyrun, confirmed non-malicious.
-Checked ChanProd endpoint to verify process tree, no malicious processes spawned from ChromSetup.exe found. 
-Queried SIEM for events tied to ChanProd's IP address. No logs have been found.

Reccommended Next Steps:
-Review AV detection signature/heuristic that triggered this alert for tuning
-Submit ChromeSetup.exe hash to AV vendor as a false-positive exclusion candidate
-Whitelist known-good Chrome installer hash/path if this is a recurring pattern across the environment
-No further action needed on ChanProd's host — no compromise indicators found