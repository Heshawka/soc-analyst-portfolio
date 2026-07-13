7/7/26

-3 alerts, did 2 without doing the summary, last one did the summary but it got deleted. 
-made template for future summary notes, aim to get down to sub 20 minute total alert time for a true positive.
-watching https://www.youtube.com/watch?v=ueth6WvFVMU&t=6s intro to ip for networking refresher - notes below

NOTES: 

-shipping truck analogy; network topology is the road (ethernet, DSL, cable system); truck is Internet Protocol; boxes inside hold data (TCP and UDP)
-inside of an ethernet frame are lots of things but here is the usual structure
left to right:

ethernet header->IP->TCP->HTTP data->ethernet trailer

-tcp and udp are protocols to move data from place to place; differenmt features
-OSI layer 4 transport layer. 
-tcp or transmission control protocol:

	1. reliable delivery
	2. connection oriented
	3. flow control: receiver can manage how much data is sent

-udp or user datagram Protocol
	1. Connectionless: no setup information is inbound
	2. sends packets without AKCS
	3. unreliabe: no error recovery or reordering of data or retransmissions
	4. no flow control
	
-IP address is destination street address for a building, while port is the specific room number

-watching https://www.youtube.com/watch?v=s_Ntt6eTn94 subnet mask explained

NOTES:

-ip address split into two parts, network address and host address
-subnet mask tells you how many bits in IP address is used for net vs host

example:

192.168.1.0
255.255.255.0 all 8 bits of first 3 octets are 1s, so first 3 octets are used for network, last 4 bits are used for host

TODO for tomorrow or where to start

start with 3 more alerts all documented, timed so we can get lower and lower to around 20 mins average each, finish up 3 way handshake and common ports, then go into wireshark drill 

====================================================================================================================================================================================
7/8/26

-2 alerts, did both with summary

Watching https://www.youtube.com/watch?v=_inkLnDbia0 video on tcp 3 way handshake

NOTES:

-3 way handshake:

	1. step 1: client starts connection by sending SYN packet: contains initial sequence number ISN that will be usedto track data packets
		has SYN flag = 1; initial Sequence Number = 1000 (random); Direction: client -> server
		
	2. step 2: SYN-ACK (sync acknowledge): server responds with synack packet, acking the client's SYN and sending its own sequence number
		has SYN flag = 1; ACK Flag = 1; Seq number = 2000 (server's ISN); ACK number = 1001 (client's ISN + 1); direction
	
	3. step 3: ACK: client sends ACK to acknowledge server's synack. Completes handshake
		has ACK = 1; Seq = 1001; Ack number = 2001 (server's ISN + 1); Direction
		
Watching https://www.youtube.com/watch?v=qTaOZrDnMzQ wireshark tutorial

NOTES:

Statistics -> Conversations useful 

Filtering packets: Apply as filter after clicking on ur IP -> Selected -> A->ANY is from source to/from anything

For phishing/hacked: check for http -> just type http -> follow stream (doesnt work for https

Can change coloring rules -> view -> coloring rules

can remove

TODO: nothing did pretty good today

====================================================================================================================================================================================
7/9/2026

-3 alerts, all documented in letsdefend-writeups

WATCHING https://www.youtube.com/watch?v=AYgXr1dynKU OSI model

NOTES:

Open systems Interconnection Reference model

PEOPLE DONT NEED THOSE STUPID PACKETS ANYWAY

1/Physical:
	• physics of the network
	• singnaling, cabling, connectors
	• not really protocols
	• tests: loopback tests, test/replace cables, swap cards
	ex/ cables, wires, signal
2/Data Link: 
	• basic network language/MAC address layer
	• Data Link Control (DLC) protocol; MAC (media access Control) address on ethernet
	• The "Switching" layer (network switches)
	ex/ frames, MAC address, Extended Unique Identifer EUI, switch
3/Network Layer:
	• Routers use for forwarding traffic
	• IP address 
	• Fragment frames to traverse different networks
	• anything with routing, IP, subnet, etc
	ex/ IP, Router, packets
4/Transport Layer:
	• Transport from 1 device to another "Postoffice"
	• TCP and UDP 
	ex/ TCP, UDP
5/Session layer
	• Communication management between point A and B
	• Start session, stop, restart
	• Control protocols, tunneling protocols
	ex/ Control protocols, tunneling protocols
6/Presentation Layer
	• Character encoding, encryption/dec
	• Putting stuff into stuff we see with eyes
	• Combined with 7
	ex/ Application encryption (SSL/TLS)
7/Application
	• See on screen
	• HTTP, FTP, DNS, POP3
	ex/ Your eyes
	
WATCHING https://www.youtube.com/watch?v=jX1pobYmZdE common ports

FTP: tcp/20 active mode data (file transfer itself) | tcp/21 (control info)
	• authentication
	• list, add, delete, other maintenance
SSH: tcp/22 
	• encrypted 
SFTP: tcp/22 same as SSH
	• uses SSH 
	• secure file transfer with encrypt
Telnet: tcp/23 
	• old ssh not secure/encrypted
SMTP: 	sending mail
	• tcp/25
DNS: domain name system; resolves names to IPS
	• tcp/53
HTTP: web traffic unencrypted
	• tcp/80
HTTPS: encrypted
	• tcp/443
RDP: remote desktop
	• tcp/3389
DHCP: dynamic host config Protocol
	• automated config of IP, subnet mask, and other options
	• udp/67 and udp/67
	• requires dhcp server thats usually on our router
NTP: Network time protocol
	• Switches, routers, firewalls, servers, every device has its own clock
	• Sync time across devices
	• udp/123
SNMP: simple network management Protocol
	• monitor and manage connected devices on an IP network
	• udp/161 
LDAP: Lightweight directory access Protocol
	• query and manage directory services over an ip network
	• tcp/389
	• LDAPS uses tcp/636
SMB: Server message block
	• windows file sharing
	• tcp/445 
Syslog: sends logs to your siem 
	• tcp/514

TODO FOR TOMORROW: nothing you're good
====================================================================================================================================================================================
7/10/26

-Did 3 Letsdefend alerts, all under 2 hours so roughly 40 minutes per alert with in depth summary and writeups, still need some work but getting much faster (started at 1 hour+ per alert)
-Today was a lighter day, already have splunk server set up on Linux from before, so took it a little easy

====================================================================================================================================================================================
7/11/26
-Did 3 LetsDefend alerts, around 2 hours to get through again. This time I had quite an interesting true positive case. It involved around 4 phases of attack, more info about it in the writeup, pretty fun to do but was difficult
-Need to do wireshark pcap, but this can be done on weekend on a catch-up day

====================================================================================================================================================================================
7/12/26
-Couldn't do much today in terms of alertss, but it's okay weekend is for catching up
TODO for tomorrow: 
-checkout a malicious wireshark pcap
-get a few LetsDefend writeups ready for portfolio

WEEKEND PCAP FOR CATCHUP DAY