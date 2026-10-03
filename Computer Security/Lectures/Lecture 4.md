date: 28-09-2026
time: 10:00
topic: Network Security: Application Layer and Domain Name System
tags:

# Application Layer

![[Pasted image 20261001192000.png]]

^ remember, ARP connects the physical to virtual hence why it's in between 3 and 2
### Uniform Resource Locators (URLs)
- are standardised format for describing the location and access method of resources via the Internet
![[Pasted image 20261001192429.png|445]]
            Figure 1: Anatomy of a URL

- the host is usually a *domain* but can sometimes be IP address
- the *scheme/protocol* specifies the protocol used to access the resource e.g. https, http, ftp
- after the /, you can specify the path
- query string does an action for you
- if a DNS server with a specific URL goes down, that resource would not be accessible

### Domain Name System (DNS)
- an ==application== layer protocol
- maps domain names to IP addresses
- mapping can be **many-to-many** e.g.
![[Pasted image 20261001193450.png]]
        Figure 2: many-to-many mapping

- DNS is a distributed database (if there was only 1 and it was attacked, all URLs wouldn't be accessible) that stores **resource records**
	- **Address (A) record** - IP address associated with a host name
	- **Mail Exchange (MX) record** - mail server of a domain
	- **Name Server (NS) record** - authoritative DNS server for a domain

### Domains
- **Domain name** - have 2 or more labels separated by dots
- **Top-level domain (TLD)**
	- generic (gTLD) for example .com, .org, .net
	- country-code (ccTLD) for example .ca, .it
	- new top level domains for example .scot, .tirol
![[Pasted image 20261001194550.png]]

#### Who manages TLDs?
**gTLDs** - managed by ICANN (developers pay to create their domain and ICANN checks the domain as well as the person)
**ccTLDs** - managed by government organisations

### DNS Trees

![[Pasted image 20261001195135.png]]
- read from left to right
- top layer is top domain, second is domain, third is subdomain
- layers only know info about their own layer and below
- example shows Address (A) records, which maps IP addresses to the host name

### Name Servers
- keeps *local databases* of DNS records
- answers DNS queries e.g. "what's the IP address of this DNS?"
	- can also ask other name servers

**Authoritative Name Servers**
- stores reference versions of DNS records for **zones** and keeps info about the records, allowing other name servers to update their information

> [!NOTE] Terminology
> Zone - a portion of the DNS namespace (the hierarchical tree) that is managed by a specific organisation or administrator.

**Root Servers**
- are authoritative for top level domains (they're actually hard coded into every device) e.g. ".com", ".edu"
#### Name Resolution
- this is the process where DNS records can be retrieved
- they connect to *Name Servers* and cache the records they receive

**Iterative Name Resolution**
![[Pasted image 20261003164820.png]]
- repeated requesting from different servers and updating the query at each step
- only the local machine caches the response

**Recursive Name Resolution**
![[Pasted image 20261003165312.png]]
- the request gets passed on throughout the call stack and once the answer is found, the answer is recursively sent back until it reaches the local machine
- caching occurs at each server

### DNS Caching
- there would be too much traffic especially for Root and TLD servers so caching is import
- DNS servers cache records that are results of queries for a specified amount of time (Time-to-live, after that time they are dropped from cache)
	- **shared hosting services** have very short TTLs because IP's changing often
- a stale record will be seen by the server, then dropped in all the other servers, then tried again
- can **evict records** once cache is **full**

![[Pasted image 20261003175804.png]]

### Local DNS Cache
- operating systems maintain cache (all users can see)
- private browsing does not clear DNS cache, need to flush which can increase traffic as cache will be empty
- view DNS cache: ipconfig /displaydns
- clear DNS cache: ipconfig /flushdns

### DNS Cache Poisoning
- provide wrong address to DNS and get it cached, then wrong machine is being communicated to
- DNS queries are issued over UDP on port 53 with a 16-bit request identifier in the payload to match answers with queries otherwise will be hard to find within hundreds of queries. This has **no authentication**
- DNS cache may be **poisoned** when: 
	- a resolver query has predictable identifiers and return ports
	- an attacker answers before the authoritative name server does (because could be further away)
	- when an identifier is ignored and unsolicited DNS records are accepted

**Defenses**
- can *randomise* request identifiers and return ports (both 16 bits)
- chances of the attacker succeeding trying to guess both is 1/(2^32)  <  4 billion
- effective against a single guess, but not against **many guesses**

### Subdomain DNS Cache Poisoning (Kaminsky) Attacks
- attacker will cause victim to send many DNS requests for non-existent subdomains of target domain
- attacker then sends victim forged NS responses for the requests containing: random ID, correct NS record, spoofed glue record pointing to the attacker's name server IP (so any resource they want the victim to visit)
	- that fake record will be cached so next time victim visits the correct NS record, it will immediately take them to the fake, corrupt record

### **Defense using DNSSEC**
- authenticity using *DNSSEC* (public key cryptography)
- checks that the DNS answer is from the original and not some fake record
- it has signed DNS replies at each step and by using public-key cryptography
- have to trust that your software has the correct TLD key burned into it (because it should) and that every other NS has the correct key
![[Pasted image 20261003183553.png|420]]