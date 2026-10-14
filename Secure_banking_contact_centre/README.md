Secure Banking Contact Centre Network

Project Overview

This project simulates a secure banking contact centre network using Cisco Packet Tracer. It demonstrates network segmentation, voice and data VLANs, inter-VLAN routing, centralized DHCP services, and extended Access Control Lists (ACLs).

The lab is designed to reinforce practical networking concepts covered in the Cisco CCNA 200-301 certification blueprint.

Network Topology

The network follows a hierarchical enterprise design consisting of an edge router, a multilayer core switch, an access switch, an IP phone, an agent workstation, and a CRM server.

Device Inventory

Device	Model	Role
Edge Router	Cisco 1941	External network connectivity
Core Switch	Cisco 3560	Inter-VLAN routing and DHCP
Access Switch	Cisco 2960	Endpoint connectivity and VLAN assignment
IP Phone	Cisco 7960	Voice communication
Agent PC	Generic Desktop	Banking agent workstation
CRM Server	Generic Server	Centralized application services

IP Addressing and VLAN Design

The network uses the 172.16.0.0/20 address block.

VLAN	Name	Network	Subnet Mask	Default Gateway
10	Voice	172.16.0.0/24	255.255.255.0	172.16.0.1
20	Banking Agents	172.16.1.0/24	255.255.255.0	172.16.1.1
30	Financial Servers	172.16.2.0/27	255.255.255.224	172.16.2.1
Routed Link	Core-to-Edge	172.16.3.0/30	255.255.255.252	Point-to-point

The VLAN design separates voice traffic, agent workstations, and financial server resources into distinct broadcast domains.

Key Technical Implementations

1. VLAN Segmentation

* VLAN 10 for IP telephony.
* VLAN 20 for banking agent workstations.
* VLAN 30 for financial servers.
* Separate broadcast domains to improve network organization and traffic isolation.

2. Voice and Data Coexistence

Configured an access port to support an IP phone and a connected workstation through a single physical switch port.

The workstation uses the data VLAN, while the IP phone uses the voice VLAN.

3. Inter-VLAN Routing

Configured Switched Virtual Interfaces (SVIs) on the multilayer switch to provide default gateways and enable communication between authorized VLANs.

4. DHCP Automation

Configured DHCP pools on the core switch to allocate IP addresses, subnet masks, and default gateways to network clients.

The voice DHCP pool includes Option 150 for specifying the TFTP server address used by supported IP telephony deployments.

5. Extended Access Control Lists

Implemented extended ACLs to control traffic between banking agent workstations and the CRM server.

The security policy is designed to permit specified web traffic while restricting other traffic directed to the protected server.

ACL effectiveness is evaluated using connectivity tests and access-list match counters.

6. Network Verification

The following Cisco IOS commands are used to inspect the configuration and verify network operation:

* show vlan brief
* show interfaces trunk
* show ip interface brief
* show ip route
* show ip dhcp binding
* show access-lists
* show running-config

Learning Objectives

This project provides practical experience with:

* VLAN configuration and segmentation.
* Voice VLANs and access-port configuration.
* 802.1Q trunking.
* Inter-VLAN routing on a multilayer switch.
* DHCP configuration and address allocation.
* DHCP Option 150 fundamentals.
* Extended IPv4 ACL configuration.
* Network troubleshooting and verification.
* Secure network design principles.

Project Files

secure-banking-contact-centre/
├── README.md
└── secure-banking-contact-centre.pkt

The Packet Tracer file contains the network topology and device configurations.

Scope and Limitations

This is an educational network simulation, not a production banking deployment. The lab demonstrates foundational segmentation and packet filtering but does not implement a complete banking security architecture, stateful firewall inspection, encryption, or enterprise authentication.

The topology contains representative endpoints rather than a full contact centre. The subnet sizes represent planned network capacity.

Certification Alignment

Cisco CCNA 200-301 topics demonstrated in this lab include:

* Network fundamentals and IPv4 addressing.
* VLANs and trunking.
* Inter-VLAN connectivity.
* IP services and DHCP.
* IPv4 ACLs.
* Network verification and troubleshooting.

Author

Umi Siguca
