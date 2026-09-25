VLSM & Static Routing – Multi-Site Network

Overview

This Cisco Packet Tracer lab demonstrates the design and configuration of a multi-site network using VLSM (Variable Length Subnet Masking) and static routing.

The network consists of three sites connected through point-to-point WAN links. Each site has its own LAN subnet, while /30 subnets are used for the WAN connections.

Network Topology

* 3 × Cisco 2911 Routers
* 3 × Cisco 2960 Switches
* 6 × End Devices
* 3 × LAN networks
* Point-to-point /30 WAN links

Technologies Used

* IPv4 Addressing
* VLSM
* Static Routing
* /30 Point-to-Point WAN Subnets
* Switch Virtual Interfaces (SVIs)
* ICMP
* Cisco IOS
* Cisco Packet Tracer

IP Addressing

The network was subnetted from:

192.168.10.0/24

VLSM was used to allocate appropriate subnet sizes for the LANs, while /30 networks were used for the router-to-router WAN links.

Routing

Static routes were configured on each router to provide connectivity between the three sites.

The routing configuration was verified using:

show ip route

Connectivity was tested using:

ping

and Cisco Packet Tracer PDU testing.

Troubleshooting

During the lab, a topology mismatch was identified where one site did not have an appropriate Layer 3 gateway.

The topology was rebuilt to ensure that:

* Each LAN had a valid default gateway.
* WAN links used the correct point-to-point addressing.
* Static routes matched the actual topology.
* Switch SVIs were configured within their local LAN subnets.
* End-to-end connectivity was maintained across all sites.

Verification

After troubleshooting and reconfiguration:

* Routing tables were verified.
* WAN connectivity was tested.
* End-to-end ICMP connectivity was tested.
* Multi-packet PDU testing achieved 100% success.

What I Learned

This lab strengthened my understanding of:

* VLSM subnet planning
* Static route configuration
* WAN addressing
* Layer 3 gateways
* SVI configuration
* Multi-site network troubleshooting
* End-to-end connectivity verification

Lab File

vlsm_static_routing.pkt
