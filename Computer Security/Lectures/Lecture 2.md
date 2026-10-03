date: 23-09-2026
time: 10:07
topic: Networking Principles
tags:

---
# Packet Switching
- data is split into packets then transported *independently* over network
- handled in a ==*best efforts*== manner
- can follow same or different routes to get to endpoint
- if a packet failed to send, re-send (it is cheap)

> [!NOTE] Terminology
> ==best efforts== - an action is done to the best of its abilities but success is not guaranteed.
> ==packet== - contain header, payload, footer and use IP addresses to transport data through ==Network layer==.

![[Pasted image 20260923184900.png]] 
   Figure 1: Packet *p* abstract example

---
### Layers
- upper layers depend on bottom layers to work
- all layers above the bottom-most layer are virtual (abstract)
- bottom layer = physical
- each device implements these layers (so 2 devices communicating with each other has established a communication channel for each layer)
Fragmentation can occur at every layer.

![[Pasted image 20260923192806.png]]

> [!NOTE] Internet Stack
> > - packets just need to know where to go
> > - packets follow a pattern of up, down, across when sent across internet
> > - the principle of layers is applied, where the layer itself knows what to do but doesn't know what lower layers do, just relies on them
> 

---
### Encapsulation
- when a packet *p* from protocol *p* is wrapped into another packet *q* from protocol *q*
- contents stay in payload

![[Pasted image 20260923185012.png]] 
                Figure 2: Packet *p* encapsulated into *q*

- can be done across layers:
![[Pasted image 20260923185434.png]]
                       Figure 3: Encapsulation across layers

---
### **Local Area Networks**
Network Interfaces - device connecting another device to a network. E.g. Ethernet, Wi-Fi adapter, DSL modem

MAC Address - each network interface has unique pre-defined 48-bit number to define its address.
- the first 3 octets are unique to its manufacturer

Switch - Routes in ==link layer==, in LANs. Learns the MAC of each computer connected to the network interface and sends frames to the correct destination device.
Large trees of switches allow for large-scale forwarding.

Hub - sends data to all devices without learning the MACs.

> [!NOTE] Terminology
> frames - encapsulates packets and transports at the ==Data Link layer==

==Protocols== are a standardised set of rules defining how to format and process data on a network.
### **Internet Protocol**
Deals with:
1. Addressing
2. Routing 
3. Fragmentation + Reassembly
4. Data Encapsulation + Packaging (encapsulates TCP or UDP packets into specific form)

### **IP Addresses and Packets**
- unique
- subdivided into network, subnet, host (octets)
- specific prefixes that have special functions, e.g. broadcast addresses end in .255
- private networks not routed outside of a LAN
- IP header contains source + destination as destination machine only cares about these
![[Pasted image 20260930111806.png]]

> [!NOTE] Terminology
> **TTL** (time to live) - is a counter for the data packet which decrements at every hop when it is travelling. Prevents packet from being transported forever. Max is usually 225
> **prot** - protocol

### **IP Routing**
- works at ==Network Layer==
- a *router* bridges multiple networks
- only looks at destination address (not source)
- maintains tables to forward packets to appropriate network - keeps track of LAN addresses or gateway routers
	- if it can't find the destination in the table, it will have *default route* to send the packets
![[Pasted image 20260930112009.png]]

**Internet Control Message Protocol (ICMP)** report errors and provides info on network communication problems (tests + debugs)
- works at the ==network layer==
- there are several methods of exploring a network (can be used before an attack too)
	- **ping** - sends echo requests messages and finds statistics on *round trip times* and *packet loss*
	- **traceroute** - sends ICMP messages with increasing TTL to discover routes

### **Network Attacks**
==Standard==: data is sent from source to destination
==Denial of Service (DoS)==: data is stopped during traffic so it doesn't reach destination
==Wiretapping (sniffing)==: data is sent to both destination and attacker
==Wiretapping (passive)==: data is sent to attacker first to read, then destination
==Tampering==: like passive wiretapping but data is edited before reaching destination
==Spoofing==: like tampering but data is sent directly from the attacker, who is pretending to be the source

![[Pasted image 20260923194326.png]] 
                Figure 4: 5 types of network attacks

### Wireshark
- captures everything happening in the network it's computer is connected to, and saves it
- can write protocol parsers - decodes messages being sent
- analyses traffic 