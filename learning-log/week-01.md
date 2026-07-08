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

TODO: nothing did pretty good today locked in cuh

====================================================================================================================================================================================
7/9/2026

-
