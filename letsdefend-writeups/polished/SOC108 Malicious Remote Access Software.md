SOC108 - Malicious Remote Access Software Detected
Event ID: 38
2021-01-01 17:36:00 UTC
Alert Priority: Medium (per LetsDefend classification). Consistent 
with investigation findings — while confirmed false positive, the 
unencrypted HTTP connection to the AnyDesk relay warrants continued 
attention rather than downgrading to Low.
Confidence Level: High
MITRE attack techniques: T1219 (Remote Access Tools) — alert 
pattern only, not confirmed malicious. This alert triggered based 
on installation/use of remote access tools, which maps to a 
technique commonly abused by attackers for persistence and remote 
control.
IOCS: Included in LetsDefend

Summary: 

On 2021-01-01 at 17:36:00 UTC, a file named AnyDesk.exe triggered an alert on DanielPRD's machine. After investigation, this alert has been deemed a false positive. AnyDesk is a legitimate, popular remote desktop software. Since AnyDesk allows external users to bypass local security controls, the antivirus system flagged this as malicious. A whitelist exemption should be used to prevent false positives like this in the future. 

Reasoning:

AnyDesk.exe was analyzed using VirusTotal and HybridAnalysis. Both sandboxes deemed this file as non-malicious, but had several suspicious indicators mapping to similar remote desktop software. AnyDesk was flagged due to its inherent behavior as a dual-use administrative tool, aligning with MITRE ATT&CK Technique T1219 (Remote Access Tools). Threat actors frequently exploit AnyDesk to bypass traditional perimeter firewalls, establish persistence, and move laterally across networks without deploying custom malware. In regards to the two connections to anydesk domains, these are legitimate connections that are established when direct peer-to-peer connection is blocked. This is within established behavior by AnyDesk. However, it should be taken into consideration that one of these connections was made using HTTP, which is vulnerable to interception and modification. Discretion is advised.

Timeline - Time (UTC) | Event

2021-01-01 17:36:00 UTC - Firewall log shows connection from DanielPRD (172.16.17.33) to boot-01.net.anydesk.com (134.119.217.177).

2021-01-01 17:37:00 UTC - Firewall log shows connection from DanielPRD (172.16.17.33) to relay-61e0b722.net.anydesk.com (146.0.234.85).

Attack Detail: 

No attack chain present - AnyDesk.exe is a legitimate remote desktop software. Execution followed expected remote desktop behavior, with no anomalous network activity, no persistence creation, and no malicious process injection observed. 

Actions Taken:
-Checked AnyDesk.exe against VirusTotal and HybridAnalysis, confirming non-malicious file.
-Checked DanielPRD endpoint. No processes, network actions, terminal history, or browser history was found from the day of the incident.
-Found 2 firewall logs concerning DanielPRD. The first log shows HTTPS connection to boot-01.net.anydesk.com (134.119.217.177). The second log shows HTTP connection to relay-61e0b722.net.anydesk.com (146.0.234.85). After research into AnyDesk, it appears that these two connections are regular behavior for the application. However, a connection from our network to outside by port 80 may be unintentional and therefore reviewed.
-Ruled out any potential malicious emails; no emails tied to Daniel have been found on the day of the incident. 

Recommended Next Steps:
-Review AV detection signature/heuristic that triggered this alert for tuning
-Submit AnyDesk.exe hash to AV vendor as false positive exclusion candidate
-No further action needed for DanielPRD's host - no compromise indicators found
-Investigate why the relay connection used HTTP instead of HTTPS — confirm this is expected AnyDesk fallback behavior rather than a misconfiguration
-Consider firewall rule review to restrict outbound port 80 where not explicitly required, given interception risk

