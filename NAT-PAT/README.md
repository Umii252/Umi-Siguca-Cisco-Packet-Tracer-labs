NAT & PAT Lab

Objective

Configure and verify Port Address Translation (PAT/NAT Overload) on a Cisco IOS gateway router.

The goal is to allow private LAN hosts to access a simulated public network using a single public IPv4 address.

Topology

Private LAN
192.168.10.0/26
      |
     SW1
      |
   R1-Gateway
      |
203.0.113.0/30
      |
   R2-Internet
      |
 Public Server
   8.8.8.8/24

IP Addressing

Device	Interface	IP Address
R1	G0/0	192.168.10.62/26
R1	G0/1	203.0.113.1/30
R2	G0/1	203.0.113.2/30
Server	G0	8.8.8.8/24

Lab Tasks

1. Configure NAT Zones

* Configure R1 G0/0 as ip nat inside
* Configure R1 G0/1 as ip nat outside

2. Configure NAT ACL

Permit the internal network:

192.168.10.0/26

3. Configure PAT

Configure NAT Overload using R1’s outside interface.

Verification

show ip nat translations
show ip nat statistics
show access-lists
show ip interface brief

Expected Result

Internal private IP addresses are translated to R1’s public IP address, allowing multiple LAN hosts to access the simulated public server through PAT.
