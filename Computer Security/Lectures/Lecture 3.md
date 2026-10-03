date: 25-09-2026
time: 10:02
topic: Network Security: ARP, IP, TCP, UDP
tags:

### **IP and MAC addresses**
- IP ==network layer== - used by **high level** protocols
- MAC ==data link layer== - used by **low level** protocols

---
### **Address Resolution Protocol (ARP)**
- low level protocol
- *stateless* - ARP forgets it has sent a request
- connects ==network== and ==data link== layers (IP to MAC address)
- does not have security measures i.e. authentication, confidentiality, integrity
	- assumes machines are being truthful so are *trusted*
- ARP deals with *broadcasts* (telling everyone) and *caching* (saves stuff)

> [!NOTE] Terminology
> **Stateless protocol** - do not retain information about user's past transactions.

**Broadcasts and Caching**
1. ARP broadcasts asking who has specific IP address
2. corresponding machine responds with its MAC
3. requesting machine caches response
4. network administrator assigns this IP address to the machine so everyone on network knows
(**ARP Cache** stores responses)

**ARP Caching Poisoning (ARP Spoofing)**
- ARP cache is updated whenever an ARP response is received, even if no request sent
- requests aren't tracked so a mal actor-in-the-middle can *spoof* other machines
- machines are all *trusted* but not necessarily *trustworthy*
- malicious user can eavesdrop
To solve the issue, you can make sure ARP cache stores only *static entries* (entries cannot be overwritten once made) but this is very difficult to manage.

---
### **Internet Protocol**
#### LAN to Internet
*Routers* - act as a gateway for machines communicating from a private LAN network to the internet. The IP address from the private network gets dropped at the router then forwards the packets to the internet.
![[Pasted image 20260930233304.png|531]]

#### IP Vulnerabilities
- unencrypted transmission
- no source authentication (sender can spoof address, and can make it hard to trace back to attacker)
- no integrity checking (no checks on actual packet details itself)
- no bandwidth constraints
	- MANY packets can be injected -> network to launch **Denial-of-Service Attack**

---
### **Transport Layer**
#### User Datagram Protocol (UDP)
- *stateless* and unreliable **datagram protocol**
- doesn't provide delivery guarantees, but is efficient
- can distinguish data for multiple concurrent applications on a single host
- applications using UDP must be willing to accept a fair amount of corrupt + lost data
	- many applications use UDP because humans are good at filling in the gaps
	- e.g. voice calls have grainy noise (lost sound) but we can still understand

#### Transmission Control Protocol
- reliable and ***ordered*** deliveries (cares about sequence)
- can distinguish **multiple applications** on same host
- *stateful*: keeps track of states (interactions)
	- marks each packet with **sequence number**
	- sends ACK (acknowledgement) to indicate successful received packet
- uses *checksum* in the header to check data
![[Pasted image 20260930235202.png|547]]
					Figure: TCP Packet Format
#### Ports
- remember, TCP and UDP supports concurrent applications on same server
- are 16-bit numbers
- there are *source* and *destination* ports
- certain port numbers are reserved for known protocols, and are usually standard

#### TCP Data Transfer
- before data transmission between client and server can be confirmed, a three-way handshake must be done
	- *initial sequence numbers* (SYN) are exchanged then a bunch of ACKs are checked to make sure data is ok (SYN/ACK)
	- the *checksum* is also checked (within packet)

#### Establishing TCP Connections
- established using *3-way handshake*
- client requests connection: sends out SYN packet
- server responds with SYN/ACK packet, acknowledging connection
- client responds with an ACK, establishing connection
![[Pasted image 20261001124116.png|700]]

#### SYN Flooding
 - the attacker continuously sends SYN packets to victim, ignoring SYN-ACKs so victim is stuck waiting and their state table runs out of space
 - **effective** against smaller targets
 - **however** attacker's IP can be traced and attacker's bandwidth is unlikely to be comparable to a server's

#### Spoofing: Forged TCP Packets
- same as SYN flooding except the source of the TCP packet has been **forged**
- **effective** because harder to trace and ACKs are actually sent to the computer with the forged address lol
- **however** packets with source addresses outside the victim's origin network will be dropped

---
### **Smurfing**
- exploits ==ICMP== (internet control message protocol) *pings* request, whereby servers/computers respond, to echo packets, to say they are online
- a **broadcast address** sends packets to ALL the machines on a network, so if a ping is sent to this, the echo back would be sent from all the machines connected to that network
	- called a "Smurf amplifier"
	- attacker amplified the amount of bandwidth they had
- the source IP address will be the victim's
- this is a "reflection" attack