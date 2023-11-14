# 14 Physical Networking

**Ethernet** is the main link layer technology covering 95% of the world wide local area network (LAN)

**CSMA/CD**: the model used by Ethernet

- Carrier Sense: tell whether anyone is talking or not
- Multiple Access: everyone can talk
- Collision Detection: know when you interrupt someone else

Three types of packets can be exchanged on a **segment** (small groups of networks)

1. Unicast: address to one host
2. Multicast: address to multiple/group of hosts
3. Broadcast: all hosts on a segment

One broadcast domain per Ethernet segment

Switches are responsible for fowarding multicast and unicast packets to the physical segments intended and broadcast gets forwarded to all ports
