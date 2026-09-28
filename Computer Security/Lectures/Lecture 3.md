date: 25-09-2026
time: 10:02
topic: Network Security: ARP, IP, TCP, UDP
tags:

IP and MAC addresses
- IP ==network layer==
- MAC ==data link layer==

**Address Resolution Protocol (ARP)**
- connects ==network== and ==data link== layers (IP to MAC address)
- does not have security measures i.e. authentication, confidentiality, integrity
	- assumes machines are being truthful so are *trusted*
- ARP deals with *broadcasts* and *caching*

Broadcasts and Caching
ARP broadcasts asking who has <\IP address>
                v
     corresponding machine responds
                v
        machine caches response

ARP Caching Poisoning (ARP Spoofing)
A mal actor-in-the-middle can pretend to be the requested machine and instead of sending the correct machine's IP address, they send their own

IP Vulnerabilities
- unencrypted transmission
- no source authentication (sender can spoof address)

User Datagram Protocol (UDP)
- ==transport== layer
