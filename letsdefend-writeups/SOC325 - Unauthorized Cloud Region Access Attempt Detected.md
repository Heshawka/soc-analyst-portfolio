SOC325 - Unauthorized Cloud Region Access Attempt Detected
Event ID: 303
2024-09-24 08:21:00 UTC
Alert Priority: High.
Confidence Level: Medium. Only source of low confidence is from the intial access to the compromised test@letsdefend.io account. 
MITRE attack technique: T1110 (Brute Force) - Over 50 failed login attempts with the same username detected. 
IOCS INCLUDED IN LETS DEFEND (DONT WORRY ABOUT THESE)	
 
Summary: 

On 2024-09-24 at 08:21:00 UTC, a brute force attack was detected from source address 134.209.145.73 against 52.15.206.21 (AWS_Services). The source address is based in India and has over 9000 reports of abuse according to AbuselPDB, with 6 security vendors on VirusTotal deeming it malicious. There were 50 different logs indicating login attempts to /accounts/login with the same test@letsdefend.io username. In addition, two days before the login attempts, an email from CTI describes test@letsdefend as a compromised account. Remediation regarding this account is advised, however the threat actor was unable to access the target host at 52.15.206.21 (AWS_Services). The threat actor was blocked due to being in an unsupported cloud region. This alert has been deemed a true positive. Escalation to L2 is advised regarding the compromised account: test@letsdefend.io.

Reasoning:

VirusTotal and AbuselPDB confirmed the source address (134.209.145.73) as malicious. Addtionally, there were 50 login attempts to AWS_Services, which were all blocked due to the source address being in an unsupported cloud region. Escalation to L2 has been advised to remediate the compromised test@letsdefend.io account. 

Timeline - Time (UTC) | Event

2024-09-24 07:25:00 UTC to 08:21:00 UTC - 50 login attempts to AWS_Services using test@letsdefend.io from source address 134.209.145.73.

Attack Detail: 

The initial access to the compromised test@letsdefend.io remains unknown. However, a brute force attack was attempted by the threat actor, but was blocked due to being in an unsupported cloud region.

Actions Taken:
-Checked source address (134[.]209[.]145[.]73) against VirusTotal and AbuselPDB. 6 security vendors on VT flagged the IP as malicious, and over 9000 reports of abuse was confirmed by AbuselPDB. The source address is based in India with hostname 9dot9insights.com and domain name digitalocean.com.
-Checked logs tied to source address, revealing 50 login attempts with the same compromised test@letsdefend.io username. All were blocked due to being in an unsupported cloud region.

Reccommended Next Steps:
-Blacklist 134[.]209[.]145[.]73 source address to prevent future brute force attempts.
-Isolate and reset credentials for the compromised test@letsdefend.io account. 
-Investigate how the threat actor gained initial access to the compromised account.
