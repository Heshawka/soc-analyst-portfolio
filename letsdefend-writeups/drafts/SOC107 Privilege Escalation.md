SOC107 - Privilege Escalation Detected
Event ID: 19
2020-9-22 15:40:00 UTC
 
Summary: 

On 2020-9-22 at 15:40:00 UTC, a file named "creditcard" found on KatherinePRD's machine triggerered an alert for privilege escalation. After analyzing the file in VirusTotal, it has been confirmed to be a Linux kernel privilege escalation exploit targeting eBPF (CVE-2017-16995). 

Reasoning:

I initially checked the reputation of the 'creditcard' attachment found in KatharinePRD's email. VirusTotal and HybridAnalysis both confirmed that this was a malicious attachment exploiting CVE-2017-16995. Second, I checked the reputation of cashbank.com (email sender), and Abusel confirmed it had over 180 reports of abuse. Based on this, I assessed this as a true positive tied to a Linux kernel prvilege escalation exploit.

Timeline - Time (UTC) | Event

2020-09-22 15:35:XX UTC - Email with malicious "creditcard" attachment sent from david@cashbank.com to katharine@letsdefend.io. 

2020-09-22 15:40:XX UTC - creditcard attachment ran on KatharinePRD's machine. 


Attack Detail: 

The initial threat was the phishing email sent to katharine@letsdefend.io
by david@cashbank.com. The email attempts persuades the recipient into clicking the attachment by lying about suspicious activities on their credit card account. Once the attachment was downloaded, it was able to take advantage of CVE-2017-16995, using a bpf syscall to load a malicious BPF program. It then used the pwn function to leak kernel pointers (task_struct), locate the process's cred structure, and perform an arbitrary write to overwrite UIDs to 0 (root). Finally, it verifies elevation with getuid() and executes '/bin/bash' to provide the attacker with a shell. 

Actions Taken:

-Reviewed KatharinePRD's emails to determine the source of 'creditcard' attachment (received from david@cashbank.com).
-Checked cashbank.com against Abusel, confirming several reports of abuse including hacking, port scanning, phishing, etc.
-Queried the SIEM for any logs tied to KatharinePRD, but found none related to this incident.
-Quarantined KatharinePRD
-Documented findings and escalated to L2.

Reccommended Next Steps:
-Clean 'creditcard' attachment from KatharinePRD's machine
-Avoid standard reboots to avoid any installed rootkits
-Kill malicious eBPF/BPF tasks
-Block unprivileged eBPF execution
-revoke and change credentials 