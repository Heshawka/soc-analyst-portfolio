MITRE section is empty. This is a clear miss given our recent conversations — this alert has a lot to map: T1059.004 (or .003, whichever bash/shell scripting variant fits — need to confirm which interpreter msi.bat actually invokes) for the reverse shell execution, T1071 (Application Layer Protocol) for C2 communication, and potentially T1210 (Exploitation of Remote Services) or T1021 (Remote Services) if lateral movement across three hosts is suspected but unconfirmed — worth adding with the appropriate "suspected, not confirmed" caveat given delivery is unknown.
Confidence Level (Medium) isn't explained, and actually seems slightly low given your evidence. You have two independent sandboxes confirming malicious behavior AND a C2 address with 2000+ abuse reports — that's fairly strong. What's actually uncertain is the delivery method and scope (is this 3 hosts or more?), not the malicious verdict itself. Worth separating those: "Confidence: High that this is a true positive malicious file; Medium/Low confidence in full scope of compromise given unknown delivery method and unconfirmed lateral movement path." Right now one blended "Medium" doesn't capture that nuance.
Alert Priority (Medium) is questionable for this scenario. Confirmed reverse shell malware, active/known-bad C2 infrastructure, three hosts, unknown vector — this reads more like it should be High, not Medium. If there's a specific reason you kept it Medium (e.g., files were already cleaned, no live sessions found), state that reasoning explicitly, because on its face this looks under-prioritized for what's actually a multi-host compromise indicator.

SOC132 - Same Malicious File Found on Multiple Sources
Event ID: 68
2021-03-01 15:16:00 UTC
Alert Priority: Medium. 
Confidence Level: Medium. 
MITRE attack techniques: 
IOCS INCLUDED IN LETS DEFEND (DONT WORRY ABOUT THESE)	
 
Summary: 

On 2021-03-01 at 15:16:00 UTC, a malicious file named msi.bat was found on three devices: MikeComputer, JohnComputer, and Sofia. The files were cleaned off all devices. Msi.bat was analyzed using VirusTotal and Anyrun, confirming its malicious behavior as a reverse shell. The delivery method of msi.bat to these three devices remains unknown. Further investigation into its delivery is advised. Escalation to L2 regarding delivery method to three host devices on our network is advised. This alert has been deemed a true positive.

Reasoning:

VirusTotal and Anyrun sandboxes cofirmed msi.bat as a malicious reverse shell script. Additionally, AbuselPDF confirmed over 2000 reports of abuse by the C2 address (81[.]68[.]99[.]93). These two factors strongly support this alert as a true positive.

Timeline - Time (UTC) | Event

2021-03-01 15:16:00 UTC - msi.bat cleaned from MikeComputer, JohnComputer, and Sofia devices. 

Attack Detail: 

Delivery method of attack chain remains unknown. A malicious file being found on three separate devices in our network indicates a possible deeper foothold that a threat actor could have. There is no evidence of phishing, indicated by no emails tied to the three host devices near the time of incident being found.   

Actions Taken:
-Checked msi.bat against VirusTotal and Anyrun reports. Both sandboxes confirm malicious behavior, specifically creating a reverse shell to control the victim's computer remotely. Additionally, C2 address (81[.]68[.]99[.]93) was found in the code.
-Checked C2 address 81[.]68[.]99[.]93 against AbuselPDB, confirming over 2000 reports of abuse.
-Checked logs tied to MikeComputer, JohnComputer, and Sofia to determine source of msi.bat. No logs found that would explain how msi.bat was placed onto their devices.
-Checked EDR for MikeComputer, JohnComputer, and Sofia. No anomalous network activity, browser history, processes, or terminal history related to the incident was found.
-Checked emails for Mike, John, and Sofia. No anomalous emails related to the incident were found. 
-Escalated to L2 for investigation of delivery method.

Reccommended Next Steps:
-Investigate each individual tied to MikeComputer, JohnComputer, and Sofia to determine the source of msi.bat.
-Depending on how fast msi.bat was cleaned, audit any active sessions on the three host devices. Force password resets, as the reverse shell could have scraped credentials.
-Check for modified registry keys, new scheduled tasks, or malicious startup folder entries that the AV may have missed.