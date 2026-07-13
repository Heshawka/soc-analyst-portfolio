SOC101 - Phishing Mail Detected
Event ID: 87
2021-04-04 23:00:00 UTC
Alert Priority: Low
Confidence Level: High

MITRE attack techniques: Technique - Reasoning

T1566 (Phishing) - Phishing email disguised as legitimate message to trick user into clicking the attached link.

T1204 (User Execution) - User actively clicks the link.

IOCS INCLUDED IN LETS DEFEND (DONT WORRY ABOUT THESE)	
 
Summary: 

On 2021-04-04 at 23:00:00 UTC, a phishing mail was detected. Sender lethuyan852@gmail.com sent an email to mark@letsdefend.io, with the E-mail subject being: Its a Must have for your Phone. Inside of the email was an HTTP link: hxxp://nuangaybantiep.xyz. After analzying the link in VirusTotal, it is confirmed to be non-malicious, despite the odd extension. After analyzing EDR and logs tied to MarkPRD, no anomalous behavior was found related to the email after Mark opened the link. Although there were no consequences this time around, clicking on unknown links from unknown senders should be avoided in the future. This alert has been deemed a false positive.

Reasoning:

VirusTotal has confirmed the attached link in the email to be non-malicious. Additionally, no anomalous network activity or related telemetry was found after MarkPRD clicked the link. 

Timeline - Time (UTC) | Event

2021-04-04 23:10:00 UTC - HTTP request from 172.16.17.88 (MarkPRD) to 192.64.119.190 (hxxp://nuangaybantiep.xyz).

Attack Detail: 

No attack detail present. Had this been a true positive, the email and attached link would be considered phishing, which could lead to further exploitation once the user clicks the link.

Actions Taken:
-Checked triggering email for signs of phishing. Email contained http link: hxxp://nuangaybantiep.xyz.
-Checked link in email against VirusTotal. VirusTotal confirms it as non-malicious.
-Checked MarkPRD's endpoint using EDR. No telemetry of relevance found due to no agent installed.
-Checked for access to hxxp://nuangaybantiep.xyz in log management. MarkPRD accessed the link at 23:10:XX UTC (Destination Address: 192.64.119.190). No anomalous network activity found after initial request.

Reccommended Next Steps:
-Provide anti-phishing training for MarkPRD and possibly other employees.
-Adjust email filters to filter out spam like this.
