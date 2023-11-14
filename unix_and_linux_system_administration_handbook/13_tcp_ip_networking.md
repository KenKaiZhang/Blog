# 13 TCP/IP Networking

**Transmission Control Protocol** and **Internet Protocol** is independent of hardware and OS

Major players in running the Internet

- **ICANN (Internet Corpoortation for Assgined Names and Numbers)**: allocates addresses and domain names and assign protocol port numbers
- **ISOC (Internet Society)**: technical development of the Internet
- **IGF (Internet Governance Forum)**: international and policy-oriented discussions related to the Internet

Everything is recorded in **Requests for Comments (RFC)** documents

- Internet standards process is in RFC2026

## Basics

**Internet Protocol (IP)**: routes data packets from one machine to another

**Internet Control Message Protocol (ICMP)**: defines low-level support for IP

- error messages
- routing assistance
- debugging help

**Address Resolution Protocol (ARP)**: translates IP address to hardware address

**User Datagram Protocol (UDP)**: unverified, one-way data delivery

**Transmission Control Protocol (TCP)**: reliable, full duplex, flow-controlled, error-correct conversations

High level protocols do not focus on the hardware

Data travels on a network in the form of **packets** (bursts of data with a max length imposed by the link layer)

- consists of a header and a payload
  - header includes the destination, checksums, protocol information, handling, and more
  - payload is the actual data being sent

Headers contains information on when one packet stops and the next beginning (**framing**)

Link layer is divided into 2 parts:

- **Media Access Control (MAC)**: deals with the media and transmits packets onto the wire
- **Logical Link Control (LLC)**: handles the framing

Size of packets are limited by protocol and hardware specs (**maximum transfer unit**)

**Fragmentation**: the process of breaking down packets into smaller pieces to fit the MTU

- the receiver must recombine the fragments
- could be avoided by setting a "do not fragment" flag but could lead to error if packet size > MTU

Network packets have the following to properly address its destination:

- MAC: used by hardware to identify specific machine in a network and is immutable
- IP address: specific identifier for a mcahine's network destination
- hostname: names associated to an IP
- port: extends the IP address
  - some ports are predefined for specific services (HTTP, SSH, etc.) and cannot be used
- address type: allows the distinction for
  - unicast
  - multicast
  - broadcast
  - anycast

## IP Addresses

Consists of a network portion and a host portion which identifies the logical network (first 8 bytes) and the specific node on the network respectively

There are different classes:

- A (N.H.H.H): very early networks
- B (N.N.H.H): very large sites (usually subnetted)
- C (N.N.N.H): easy to get and obtained in sets
- D: Multicast
- E: Experimental addresses

You can reassign part of the host portion to the network portion with a subnet mask

- at least 8 bits must be network and 2 bits for host
- 192.168.1.10 with a subnet of 255.255.255.0 will have a network of 192.168.1 and host of 10

**/XX** or **CIDR (Classless Inter-Domain Routing)** notation help denote subnet masks that don't end in a byte boundary (not 8, 16, 24)

- 128.138.243.0/26 can accomdate 62 hosts (all 0s and 1s are saved for network and broadcast respectively)
  - indicates that 26 bits are used for network
- borrowing 1 bit from the "host" portion halves the number of original hosts and doubles the number of networks

The number of hosts per network and the value of the last byte in the netmask always add to 256

- `last_netmask_byte = 256 - net_size`

All host on the same network must have the same mask

Private addresses are only used internally (not shown to Internet)

- Translated to public address space assigned by ISP via a border router via **Network Address Translation (NAT)**

One from each class assigned for private addresses:

- A: 10.0.0.0 (just use this for all private networks)
- B: 172.16.0.0
- C: 192.168.0.0

NAT maintains table of mappings between internal and external address/port pairs

NAT will reject connections to site internal machines and interior structure

- implement a externally visible "tunnel" that connect ot specific internal hosts and ports

## Routing

The process of directing a packet from source to destination

Constructed of rules in a table in the kernel

- determining how to route to a address is based on matching the longest subnet mask
- returns ICMP "network unreachable" error if not capable

A host can only route packets to gateway machines reachable

Packets routing to next destination is determined by the gateway it is currently located (gateways are independent)

Most machines in a local area should only have one gateway

**ICMP redirect packet** indicates to sender a more efficient method of sending, thus updating the sender's routing table
