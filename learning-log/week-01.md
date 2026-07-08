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
-

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