7/14/26

-Did 3 alerts on LetsDefend, all with proper documentation and write-ups. The format and workflow is getting much quicker and efficient.
-Today was network concepts refresher so took a look a few videos by Professor Messer on DHCP, IPv4 addressing, and DNS configuration:

DHCP - https://www.youtube.com/watch?v=b7fiXM3vO18

Notes: 
	• DORA 4 step process:
		1. Discover - Find a DHCP server
		2. Offer - Get an offer for config and IP
		3. Request - Lock in an offer
		4. Ack - Ack to DHCP that we've received config and are using the given IP address
	• Base DHCP has limited communication range in an enterprise environment (uses IPv4 broadcast domain and stops at router)
	• DHCP Relay: router functionality that allows to send DHCP traffic to another subnet even though it's sent originally as broadcast.

DNS Configuration - https://www.youtube.com/watch?v=mWrtfco4dRs

Notes: 

	• Resource Records: records of domain name services
	• IN A = IPv4 internet record; IN AAAA = IPv6 internet record
	• MX record: Mail exchanger record. Determines the host name for the mail server. 
		1. Need MX record AND an A record to get IP address for mail server
			ex/ IN A mail.mydomain.name 
			    jack.mydomain.name IN A 123.12.12.12 ; Windows 10
	• TXT records: public human-readable text info. 
		1. Used for things like verification, DKIM, DMARC, and other email security.
	• SPF: sender policy framework. List of all servers authorized to send emails for this domain. Prevents mail spoofing. Mail servers perform a check to see if incoming mail did come from an authorized host.
		ex/ ; SPF TXT records
		    ; owner class ttl TXT "attribute-name=attribute value"
		      professormesser.com 300 IN TXT "v=spf1 include:mailgun.org ~all"
	• DKIM: Domain keys Identified mail. Digitally sign a domain's outgoing mail. Validated by mail servers, not usually seen by end user. The public key is in the DKIM TXT record.
		ex/ ; DKIM TXT records
		    ; owner class ttl TXT "attribute-name=attribute value"
		      1234123123.professormesser._domainkey.professormesser.com IN TXT 
		       ("v=DKIM1; t=s; p=SDIHJSILXNOIHFOISDFOISJDOIFNSFOISNIOFMO"
			"SDDSDJSODIJSIODSOIHFOIn321319udsDASD")
	• DMARC: Domain-based message authentication, reporting, and conformance: What to do with messages if verification fails -> spam, delete, etc. Extension of SPF and DKIM.

TODO for tomorrow: Clean up draft of resume, github portfolio READMEs, and submit 2 apps. 

=============================================================================================================================================================================================
7/15/26

TODO for today: 

-set up linked in
-fix up resume
-fix up github portfolio readmes and structure
-apply to 2 positions

=============================================================================================================================================================================================
7/15-16 

-was on a family trip, so unable to commit to github. Practice resumes on 7/17

=============================================================================================================================================================================================
7/17/26

-Did 3 LetsDefend alerts and corresponding write-ups. The process only took an hour and a half, which is a signficiant improvement over our usual time (roughly 2+ hours)
The process is getting much better.
-Analyzed a malicious wireshark PCAP. This one involved a RAT and analyzing the infected windows machine. Notes have been taken on it. I may add the notes and analyzed pcaps to the github once I format them and polish a little better.

=============================================================================================================================================================================================
7/18/26

-much needed application day. Created job alerts for SOC analyst postings for several sites. Applied to 1 company listed on application tracker spreadsheet in google drive.
-Polished up resume, all up to date and in the google drive.
-Splunk and Windows Malware analysis VMS are all set up and ready to go for further labs

=============================================================================================================================================================================================
7/20/26

-Did 2 LetsDefend alerts with write-ups. Both were portfolio worthy and quite complex. 
	1. The 2nd alert had to do with two maldocs which had obfuscated code. Got caught up in trying to decode them and it confused me even with using CyberChef. Gotta work through some more example of decoding obfuscated commands.
-Feeling good about networking concepts, so will move towards NIST 800-61 readings. 
-Made new directory for nist notes while reading through them in the upcoming weeks. Started on nist-800-61-rev2-notes.md, notes will not be in this log, but instead in that file. Starting with revision 2, and then moving towards revision 3 in future sessions.

=============================================================================================================================================================================================
7/21/26 

-Today and tomorrow are catch up days. 
-Gonna spend these days getting some more alert drafts into polished ones and portfolio ready
-Planning on applying as well