# SOC170 - Passwd Found in Requested URL 
**Event ID:** 120
**Date:** 2022-03-01 10:10:00 UTC  
**Alert Priority:**  Medium. The LFI attack was unsuccessful, but a service code of 500 was returned. It is best practice to return 4XX codes in order to discourage further attack attempts.
**Confidence Level:**  High.
## MITRE ATT&CK Techniques

| Technique | Reasoning |
|---|---|
| T1190 - Exploit Public-Facing Application | Attack target was WebServer1006. |
| T1083 - File and Directory Discovery | Using an LFI attack to access etc/passwd. |

## IOCs

| Type | Value |
|---|---|
| Requested URL | hxxps://172.16.17.13/?file=../../../../etc/passwd |
| IP | 106.55.45.162 |
 
## Summary: 

On 2022-03-01 at 10:10:00 UTC, an LFI attack against WebServer1006 (172.16.17.13) was detected from source address 106[.]55[.]45[.]162. The attacker requested the following URL: 
hxxps://172.16.17.13/?file=../../../../etc/passwd. This is a telltale sign of an LFI attack; the attacker is attempting to access the local passwd file. AbuseIPDB was used to confirm that the source address has over 3,000 reports of abuse made against them. One firewall log was found tied to the attacker, confirming a server status code of 500 and size of 0. This indicates an unsuccessful attack. However, a status code of 500 indicates possible vulnerability to these kinds of attacks. Input should be validated and a 4XX code is better suited for attack attempts like these to discourage further attempts. This alert has been deemed a true positive and an unsuccessful attack.
 
## Reasoning:

The requested URL is a telltale sign of an LFI attack; the attacker is attempting to access the local passwd file. Additionally, AbuseIPDB has confirmed over 3000 attempts of abuse by the source address. WebServer1006 responds with a status code of 500 and response size of 0, which indicates an unsuccessful attack. However, a response code of 500 indicates that the server encountered an internal error with the given payload. This opens up opportunity for the attacker to refine their request in order to find vulnerabilities that may lead to a successful attack attempt.

## Timeline

| Time (UTC) | Event |
|---|---|
| 2022-03-01 10:10:00 | Firewall log shows request to hxxps://172.16.17.13/?file=../../../../etc/passwd. Server responds with status code 500 and size 0. |

## Attack Detail: 

The attacker attemps an LFI attack against WebServer1006. The requested URL was hxxps://172.16.17.13/?file=../../../../etc/passwd, which is an attempt to access the local passwd file. This may be the first part of a longer attack process, since a status code of 500 may encourage further refining of the attack payload.

## Actions Taken:
-Analyzed requested URL (hxxps://172.16.17.13/?file=../../../../etc/passwd). The requested URL shows signs of an LFI attack and is attempting to access the local passwd file.
-Checked source address (106[.]55[.]45[.]162) on AbuseIPDB for signs of abuse. There were over 3,000 signs of abuse found related to the source address. The address is accociated with tencentcloud.com and Guangzhou, Guangdong, China.
-Checked logs tied to the source address. Only one firewall log was found, with an HTTP response status of 500 and size of 0. This indicates an unsuccessful attack. However, a response code of 500 indicates an Internal Server error. In the case of an LFI attack, it is better to respond with an explicit 4XX code to indicate client error over server error.
-Checked WebServer1006's endpoint using EDR. No IOCS were found.

## Recommended Next Steps:
-Ensure proper input validation to return 4XX codes instead of 5XX codes.
-Add the source address to the blacklist, given that they are well known for abuse attempts.
-Ensure no further attacks were attempted after the date of the incident.