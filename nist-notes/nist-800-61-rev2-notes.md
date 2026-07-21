Session 1

-Planning on going through the four-phase lifecycle (Preparation->Detection/Analysis->Containment/Eradication/Recovery->Post-Incident Activity).

-4 Main phases

Phase 1: Preparation
	• Incident response team (L1, L2, etc)
	• Select and implement controls based on risk assessment

The following are some useful tools/resources or things of value when it comes to preparation

1. Incident Handler Communications and Facilities
	• Contact info, on-call info, reporting mechanisms (phone numbers, emails, online forms, etc), smartphones.
	• Anything to do with communication and encryption for communication.
	• Secure storage facility
	• War room
2. Incident Analysis Hardware and Software
	• Digital forensic workstations, laptops, printers.
	• Packet sniffers, protocol analyzers, evidence gathering accessories.
3. Incident Analysis Resources
	• Port lists, documentation (for OSs apps, protocols, etc)
	• Network diagrams and lists of critical assets
	• Baselines of expected network/system/app activity
	• Hashes of files to speed incident analysis, verification, and eradication
4. Incident Mitigation Software
	• Clean OS and app installations for restoration/recovery (like a jump kit)

It's important to prevent incidents as well. The following are some good practices:

1. Risk assessments 
2. Host/network security
3. Malware prevention (AVS, IPS, etc)
4. User training

Phase 2: Detection and Analysis
	• Should be prepared to handle common attack vectors such as:
		1. External/removable media
		2. Web
		3. Email
		4. Impersonation
		5. Loss/theft of equipment
	• Assessing and detecting remains difficult due to different means of attack, high volume of potential incidents, and deep technical knowledge requirements.
	•  Signs of an incident usually fall into 2 categories: precursors and indicators. 
		Precursor: sign of future incident
		Indicator: sign of incident that may occur or is occurring now
	• Many sources of precursors and indicators:
		a. IDPS, SIEM, AV, OS logs, net logs, net flows, OSINT, people
	• Incident analysis is often difficult because of sheer amount of false positives. Also human error is huge.

Here are some ways to make analysis a little easier:

1. Profile networks and systems
2. Understand the norm
3. Log retention policy
4. Perform event correlation
5. Keep all host clocks synced (NTP)
6. internet search engines for research 
7. Data filtering to get only the good info
8. Seek assistance from others

Documentation is just as important as analysis
	• Use a SIEM/ticket system to document every aspect of an alert 

Make sure to prioritizer based on factors like impact and recoverability.

Phase 3: Containment, Eradication, and Recovery
	• Create different containment strategies for different types of attacks
	• Sometimes not sandboxing an attacker can lead to legal action if they attack other systems
	• Gather evidence for the incident but also for legal proceedings: things like identifying info (MAC, IP, etc), names and numbers of involved people, time/data, locations where evidence is stored
	• identifying attacking hosts is important, but should maintain priority on containment, eradication, and recovery

Phase 4: Post-Incident Activity
	• Lessons learned: achieve closure and evolve as a team
	• identify weakpoints, what info was needed sooner, what did we do that wasn't as important as other, etc
	• Gather some metrics that are actually useful: number of incidents handled, time per incident
	• Maintain evidence for months or years after an incident ends. When it comes to a policy for evidence retention, consider the following factors: prosecution of the attacker, data retention policies, and cost.