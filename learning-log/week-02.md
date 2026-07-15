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