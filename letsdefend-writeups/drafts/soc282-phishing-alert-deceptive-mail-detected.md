# SOC282 - Phishing Alert - Deceptive Mail Detected  
**Event ID:** 257  
**Date:** 2024-05-13 09:22:00 UTC  
**Alert Priority:**  High. Attacker has installed malicious file onto Felix's endpoint, and is performing system and network reconnaissance.
**Confidence Level:**  High.
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1566 – Phishing | Phishing email was used to get user to download Coffee.zip. |
| T1566.001 – Spearphishing Attachment | Email contains malicious attachment. |
| T1204.002 – User Execution: Malicious File | User executes Coffee.exe after extracting it. |

## IOCs

| Type | Value |
|---|---|
| Source Address | free@coffeeshooop.com |
| File | Coffee.exe |
| Hash (SHA256) | cd903ad2211cf7d166646d75e57fb866000f4a3b870b5ec759929be2fd81d334 |
| URL | https://files-ld.s3.us-east-2.amazonaws.com/59cbd215-76ea-434d-93ca-4d6aec3bac98-free-coffee.zip |
| C2 IP |  37.120.233.226 |
| SMTP IP |  103.80.134.63 |
 
## Summary: 

On 2024-05-13 at 09:22:00 UTC, a phishing email was sent from free@coffeeshooop.com to Felix@letsdefend.io, with the subject "Free Coffee Voucher." After further investigation into the email, a malicious attachment named free-coffee.zip was included. The file Coffee.exe inside the zip file was analyzed by VirusTotal and Hybrid, which confirmed malicious intent as a remote access trojan. Log management and EDR confirmed that Felix extracted the file and executed it (See Timeline). Felix's endpoint also confirmed system and network reconnaissance (See Timeline - 13:01:00). This alert has been deemed a true positive. This has been escalated to L2. 

## Reasoning:

The attached file in the email was analyzed using VirusTotal and HybridAnalysis, with high confidence of a remote access trojan. Logs and EDR have indicated that Felix executed the file, leading to system and network reconnaissance led by the attacker. 

## Timeline

| Time (UTC) | Event |
|---|---|

| 2024-05-13 09:22:00 | Email sent from free@coffeeshooop.com to Felix@letsdefend.io. |
| 2024-05-13 12:59:44 | Proxy log shows Felix clicks free-coffee.zip and downloads it. |
| 2024-05-13 13:00:00 | Firewall log shows TCP connection from Felix host machine to 37[.]120[.]233[.]226[.]. |
| 2024-05-13 13:00:38 | EDR process list indicates Coffee.exe was executed at 13:00:38 |
| 2024-05-13 13:01:00 to 13:01:30| EDR shows terminal history indicating system and network reconnaissance. |
 

## Attack Detail: 

There are three main parts to the attack chain. First, phishing/initial access to the payload. A phishing email was sent from free@coffeeshooop.com to Felix@letsdefend.io with an attached free-coffee-zip file. This zip file contains a RAT. Second, user execution. Felix executed Coffee.exe after extracting it from the zip file. Third, reconnaissance. After Coffee.exe was executed, signs of system and network reconnaissance were found on Felix's endpoint through EDR.

## Actions Taken:

-Checked SMTP address (103[.]80[.]134[.]63) against VirusTotal. There were 9 security vendors on VirusTotal confirming phishing and malicious intent. AbuseIPDB was used to determine origin. This IP's ISP is HDTIDC LIMITED and is based in Korea. Its domain name is allcloud[.]cc.  
-Checked domain name of source address (free@coffeeshooop.com) against VirusTotal. No security vendors have marked this domain as malicious.  
-Checked email that triggered alert. Found an attachment named free-coffee.zip.  
-Used LetsDefend sandbox to get SHA256 hash of Coffee.exe and checked it against VirusTotal and HybridAnalyis. Both sandboxes confirm malicious intent as a trojan/downloader.
-Checked logs tied to recipient Felix@letsdefend.io (172.16.20.151). There was evidence of execution of Coffee.exe.
-Checked Felix's endpoint using EDR. Signs of system reconnaisasance found in terminal history. Timespan is from 13:01:00 to 13:01:30. EDR also confirms Coffee.exe has been run at 13:00:38.

## Recommended Next Steps:

-Clean Coffee.exe and related files from Felix's endpoint.
-Blacklist the C2 address: 37.120.233.226.
-Blacklist the SMTP address: 103.80.134.63.
-
