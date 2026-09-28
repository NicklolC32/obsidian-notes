date: 23-09-2026
time: 10:07
topic: Network Security
tags:

---
Packet Switching
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
Layers
- upper layers depend on bottom layers to work
- all layers above the bottom-most layer are virtual (abstract)
- bottom layer = physical
- each device implements these layers (so 2 devices communicating with each other has established a communication channel for each layer)
Fragmentation can occur at every layer.

![[Pasted image 20260923192806.png]]

> [!NOTE] Internet Stack
> > - packets just need to know where to go
> > - the principle of layers is applied, where the layer itself knows what to do but doesn't know what lower layers do, just relies on them
> 

---
Encapsulation
- when a packet *p* from protocol *p* is wrapped into another packet *q* from protocol *q*
- contents stay in payload

![[Pasted image 20260923185012.png]] 
                Figure 2: Packet *p* encapsulated into *q*

- can be done across layers:
![[Pasted image 20260923185434.png]]
                       Figure 3: Encapsulation across layers

---
**Local Area Networks**
Network Interfaces - device connecting another device to a network. E.g. Ethernet, Wi-Fi adapter, DSL modem

MAC Address - each network interface has unique pre-defined 48-bit number to define its address.
- the first 3 octets are unique to its manufacturer

Switch - Routes in ==link layer==, in LANs. Learns the MAC of each computer connected to the network interface and sends frames to the correct destination device.
Large trees of switches allow for large-scale forwarding.

Hub - sends data to all devices without learning the MACs.

> [!NOTE] Terminology
> frames - encapsulates packets and transports at the ==Data Link layer==

==Protocols== are a standardised set of rules defining how to format and process data on a network.
**Internet Protocol**
Deals with:
1. Addressing
2. Routing 
3. Fragmentation + Reassembly
4. Data Encapsulation + Packaging (encapsulates TCP or UDP packets into specific form)

IP Addresses and Packets
Unique and are subdivided into network, subnet, host (octets)
Specific prefixes that have specific functions, e.g. broadcast addresses end in .255

**IP Routing**
Works at ==Network Layer==
Connects multiple networks together
Maintain tables to keep track of LAN addresses or gateway routers

Internet Control Message Protocol (ICMP)
Network Layer Protocol
Used for network testing and debugging

Traceroute
Helps to understand way traffic flows

**Network Attacks**
==Standard==: data is sent from source to destination
==Denial of Service (DoS)==: data is stopped during traffic so it doesn't reach destination
==Wiretapping (sniffing)==: data is sent to both destination and attacker
==Wiretapping (passive)==: data is sent to attacker first to read, then destination
==Tampering==: like passive wiretapping but data is edited before reaching destination
==Spoofing==: like tampering but data is sent directly from the attacker, who is pretending to be the source

![[Pasted image 20260923194326.png]] 
                Figure 4: 5 types of network attacks