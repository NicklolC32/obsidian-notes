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
![[Pasted image 20260930233304.png]]

#### IP Vulnerabilities
- unencrypted transmission
- no source authentication (sender can spoof address, and can make it hard to trace back to attacker)
- no integrity checking (no checks on actual packet details itself)
- no bandwidth constraints
	- MANY packets can be injected -> network to launch **Denial-of-Service Attack**

#### User Datagram Protocol (UDP)
- ==transport== layer
