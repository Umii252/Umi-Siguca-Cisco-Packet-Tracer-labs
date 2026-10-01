Lab: IPv6 Architecture (Global Unicast Addressing & Static Routing)

Objective

Configure and verify a native IPv6 network across multiple routing domains.

This lab focuses on:

* Global Unicast Addressing (GUA)
* Link-Local Addressing (LLA)
* IPv6 forwarding
* IPv6 static routing
* IPv6 default routing
* End-to-end IPv6 connectivity and verification

Topology Diagram

[ Site A User LAN ]             [ WAN Link ]                 [ External Server LAN ]
2001:db8:a::/64                 2001:db8:wan::/64             2001:db8:srv::/64
       │                                │                              │
 [ PC-Client ]                    ┌─────┴─────┐                 [ Internet-SRV ]
       │                           │           │                       │
    Fa0/1                       Gig0/0      Gig0/1                    Fa0
       │                           │           │                       │
┌──────┴──────┐                    │           │                ┌──────┴──────┐
│ SW1-Access  │────────────────────┘           └────────────────│ R2-Internet │
└─────────────┘                                                 └─────────────┘
                         R1-Gateway

IPv6 Addressing Plan

Site A LAN

Network: 2001:db8:a::/64

Device	Interface	Global Unicast Address	Link-Local Address
PC-Client	NIC	2001:db8:a::10/64	Auto-generated
R1-Gateway	Gig0/0	2001:db8:a::254/64	fe80::1

PC-Client Default Gateway: 2001:db8:a::254

WAN Link

Network: 2001:db8:wan::/64

Device	Interface	Global Unicast Address	Link-Local Address
R1-Gateway	Gig0/1	2001:db8:wan::1/64	fe80::1
R2-Internet	Gig0/1	2001:db8:wan::2/64	fe80::2

External Server Network

Network: 2001:db8:srv::/64

Device	Interface	Global Unicast Address	Link-Local Address
R2-Internet	Gig0/0	2001:db8:srv::254/64	fe80::2
Internet-SRV	NIC	2001:db8:srv::8/64	Auto-generated

Internet-SRV Default Gateway: 2001:db8:srv::254

CCNA Lab Tasks

Task 1: Enable IPv6 Routing

Enable the IPv6 forwarding engine on both routers.

ipv6 unicast-routing

Configure the designated Global Unicast Addresses and custom Link-Local Addresses on all active router interfaces.

Example:

interface gigabitEthernet0/0
 ipv6 address 2001:db8:a::254/64
 ipv6 address fe80::1 link-local
 no shutdown

Task 2: Configure End Devices

Configure PC-Client with:

* IPv6 Address: 2001:db8:a::10
* Prefix Length: /64
* Default Gateway: 2001:db8:a::254

Configure Internet-SRV with:

* IPv6 Address: 2001:db8:srv::8
* Prefix Length: /64
* Default Gateway: 2001:db8:srv::254

Task 3: Configure IPv6 Static Default Route on R1

Configure R1 to forward unknown IPv6 destinations toward R2.

ipv6 route ::/0 2001:db8:wan::2

This creates an IPv6 default route for destinations not already present in R1’s routing table.

Task 4: Configure IPv6 Static Return Route on R2

Configure R2 with a specific route back to the Site A LAN.

ipv6 route 2001:db8:a::/64 2001:db8:wan::1

This allows R2 to return traffic destined for the 2001:db8:a::/64 network through R1.

Core Verification Commands

Verify IPv6 Interfaces

show ipv6 interface brief

Used to verify:

* Interface status
* Global Unicast Addresses
* Link-Local Addresses

View the IPv6 Routing Table

show ipv6 route

Verify Static IPv6 Routes

show ipv6 route static

Verify the IPv6 Default Route

show ipv6 route ::/0

Test IPv6 Connectivity

ping ipv6 2001:db8:wan::2

From PC-Client, test connectivity to the external server:

ping 2001:db8:srv::8

Expected Outcome

Successful completion of this lab should demonstrate:

* Correct IPv6 Global Unicast Address configuration
* Correct Link-Local Address configuration
* IPv6 forwarding between routers
* A functional IPv6 static default route on R1
* A functional IPv6 return route on R2
* Successful end-to-end IPv6 connectivity between the Site A client and external server

Skills Demonstrated

* IPv6 Addressing
* Global Unicast Addresses (GUA)
* Link-Local Addresses (LLA)
* IPv6 Routing
* Static Routing
* Default Routing
* IPv6 Troubleshooting
* Cisco IOS CLI
* Network Verification
* End-to-End Connectivity Testing
