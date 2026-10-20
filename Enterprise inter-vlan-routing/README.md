### Enterprise Inter-VLAN Routing Lab | Cisco Packet Tracer

### Project Overview

This project demonstrates VLAN segmentation and inter-VLAN routing using a Cisco 2911 router and Cisco 2960 switches in Cisco Packet Tracer. 

The network uses a Router-on-a-Stick (RoaS) topology, allowing multiple VLANs to communicate through a single physical router interface configured with 802.1Q subinterfaces. 

The lab focuses on VLAN configuration, trunk security, IP addressing, and network connectivity verification in preparation for the Cisco CCNA 200-301 certification. 

### Network Topology

* **Router:** Cisco 2911 ISR
* **Switches:** Cisco 2960 Layer 2
* **Routing method:** Router-on-a-Stick
* **Trunking protocol:** IEEE 802.1Q
* **Simulation software:** Cisco Packet Tracer

### IP Addressing and VLAN Design

VLAN IDDepartment / PurposeNetworkDefault Gateway
**10**
Sales172.17.10.0/24172.17.10.1
**20**
Marketing172.17.20.0/24172.17.20.1
**30**
Engineering172.17.30.0/24172.17.30.1
**99**
Native VLAN172.17.99.0/24172.17.99.1
**150**
VoIP172.17.150.0/24172.17.150.1

*Note: The default gateways are the planned router subinterface addresses. VLAN 99 and VLAN 150 require appropriate interface and endpoint configurations if they are to provide Layer 3 connectivity.* 

### Key Configurations

### 1. VLAN Segmentation

* Created separate VLANs for Sales, Marketing, Engineering, native traffic, and VoIP.
* Assigned access ports to the appropriate VLANs.
* Used separate IP subnets to organise network traffic.

### 2. Trunk Configuration

* Configured trunk links using switchport mode trunk.
* Disabled Dynamic Trunking Protocol negotiation with switchport nonegotiate.
* Configured VLAN 99 as the native VLAN on trunk links.

### 3. Inter-VLAN Routing

* Configured router subinterfaces for the required VLANs.
* Used 802.1Q encapsulation to identify VLAN traffic.
* Assigned IP addresses to router subinterfaces to provide default gateways for connected VLANs.

### 4. Network Security

* Used VLAN segmentation to separate departmental traffic.
* Avoided using VLAN 1 as the native VLAN on configured trunks.
* Applied explicit trunk configuration to reduce reliance on dynamic negotiation.

### Verification Commands

The following Cisco IOS commands can be used to inspect and troubleshoot the configuration. 

CommandPurpose
**show vlan brief**
Displays VLANs and access-port assignments
**show interfaces trunk**
Displays operational trunk links and native VLANs
**show ip interface brief**
Displays interface status and IP addresses
**show running-config**
Reviews the active device configuration
**show interfaces switchport**
Displays switchport mode and VLAN information
**ping**
Tests IP connectivity between network devices

### CCNA 200-301 Skills Demonstrated

* VLAN configuration and segmentation
* Access ports and 802.1Q trunking
* Native VLAN configuration
* Router-on-a-Stick inter-VLAN routing
* IPv4 addressing and subnetting
* Basic Layer 2 security practices
* Cisco IOS configuration and verification
* Network troubleshooting

### Project Files

* enterprise-inter-vlan-routing.pkt — Cisco Packet Tracer project file
* README.md — Project documentation
* <img width="1363" height="714" alt="Screenshot 2026-10-20 181417" src="https://github.com/user-attachments/assets/63b03600-900f-4bb5-9488-4ce0f3974829" />


### Learning Objectives

The objective of this lab is to develop practical experience configuring and troubleshooting a segmented enterprise network using Cisco networking technologies. 

This project forms part of my ongoing preparation for the Cisco CCNA 200-301 certification and my development toward entry-level network support and network engineering roles.
