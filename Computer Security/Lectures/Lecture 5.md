date: 30-09-2026
time: 10:00
topic: Firewalls, NAT, and Intrusion De
tags:

# Firewalls

- is a **security measure** to prevent **unauthorised electronic access** to a networked computer system
- creates a boundary with the private network to networks outside of it - means that firewall can't protect the network from malicious insiders
- applies rules called *firewall policies*, denying traffic if it fails to pass the rules
- they can block malicious actions both from inside and outside a network
	- **Blocklist** - Allow-by-default unless something appears from the blocklist in the traffic, then it will be blocked
	- **Allowlist** - Deny-by-default, someone from the nuisance list appears, so by default: block

![[Pasted image 20261005120354.png]]
- rules can be customised by the user

#### Stateless Firewalls
- does not maintain previous interactions nor context whilst processing current packets
- treats packets in isolation
- can be restrictive to prevent most attacks e.g. **drop in-bound SYN packets**
![[Pasted image 20261005121413.png]]
#### Stateful Firewall
- keeps track of where packets are in an ongoing legitimate session (states of the packet)
- maintains tables containing information on each active connection, including **IP addresses, ports, sequence numbers of packets** (important for 3-way handshake)
	- allows **in-bound SYN packets** that have been sent as a response to a connection initiated from within the internal network, otherwise drop
	- ![[Pasted image 20261005122325.png|261]]

![[Pasted image 20261005122808.png|628]]
- need to understand protocols in depth when developing stateful firewalls


> [!NOTE] Port Scans
> A method used to analyse all the applications that are listening on ports. The attacker will contact many ports to see if any respond. That's the first step to mapping a network to then plan the appropriate attack.

#### Application Layer Firewall
- acts as a *proxy* - it simulates the effects of an application
- it **screens** information at the ==application layer==
- inspects payload data and can *sanitise* the data
- allows an administrator to block certain application requests

For example:
- block all web traffic containing certain words
- removes all macros from Microsoft Word files in email
- prevent information leakage

#### Personal Firewall
- firewalls can often be installed via a software but recently it is more common for the firewall to be built into the software of your device
	- provides **basic protection**
	- however, any **rootkit** type software can disable the firewall, which can is usually found in phishing messages

#### Firewall Pros and Cons
- **pro**: prevent straightforward attacks and info leakages
- **con**: may have unintended consequences e.g. incoming traffic which was required may accidentally be blocked
- **con**: increasing effectiveness can increase cost
- **con**: give false sense of security
- therefore, it is important to have a firewall but must be combined with other security measures

# Network Address Translation (NAT)
