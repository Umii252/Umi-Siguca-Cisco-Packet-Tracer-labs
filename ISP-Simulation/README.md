ISP Broadband Edge Simulation: Multi-Subscriber Traffic Isolation & Layer 3 Core Switching

Project Overview

This repository documents a two-part Broadband Aggregation & Customer Edge Lab designed and simulated in Cisco Packet Tracer.

The project was created to move beyond traditional enterprise LAN topologies and explore how traffic can flow from a residential subscriber network, through a Customer Edge (CE) gateway, across a simulated Fiber Network Operator (FNO) infrastructure network, and toward an Internet Service Provider (ISP) aggregation node.

The project also demonstrates practical network troubleshooting by documenting the initial connectivity failure in Part 1 and the corrected, verified implementation in Part 2.


Part 1 — Initial Broadband Edge Simulation

Objective

The first phase focused on building a simulated ISP broadband environment consisting of:

* Residential subscriber LANs
* Customer Edge gateways
* VLAN-based subscriber separation
* A Layer 3 core switch
* An ISP aggregation node
* NAT/PAT for private subscriber addresses
* Default routing toward the provider network

The objective was to understand how a subscriber’s traffic could move from a private home network toward the provider edge.

Initial Network Architecture

The topology was divided into three main operational areas.

1. Subscriber Home Network

Each subscriber represents an independent residential customer network.

Private addressing was used inside the home network:

192.168.1.0/24

The Customer Edge router provided:

* DHCP
* Default gateway services
* NAT/PAT
* WAN connectivity

2. FNO Infrastructure

A Cisco multilayer switch was used to simulate the infrastructure aggregation layer.

Separate VLANs were created to represent different subscriber connections:

* VLAN 10 — Client Home A
* VLAN 20 — Client Home B

This provided logical Layer 2 separation between subscriber networks.

3. ISP Aggregation

The ISP aggregation router (ISP-BRAS) represented the provider-side gateway.

The ISP node provided the upstream destination for subscriber traffic.

Initial Physical Connections

PC-A
  |
  | Fa0
  |
Client-Home-A
  |
  | Gi0/0
  |
Core-L3-Switch
  |
  | Gi0/1
  |
ISP-BRAS

A second subscriber connection was also represented through the Layer 3 core switch:

Client-Home-B
      |
      | Gi0/0
      |
Core-L3-Switch

Initial Connectivity Issue

During the first implementation, the topology did not initially achieve the expected end-to-end connectivity.

The connectivity test from PC-A resulted in:

Request timed out.

This became an important troubleshooting stage of the project.

Instead of treating the failed ping as the final result, the configuration and traffic path were reviewed to identify where connectivity was breaking.

The troubleshooting process involved checking:

* Interface status
* VLAN assignments
* IP addressing
* Default gateways
* Routing
* NAT configuration
* Core switch configuration
* Subscriber-to-provider traffic flow

Part 2 — Corrected and Verified Implementation

Objective

Part 2 focused on correcting the connectivity issues identified during Part 1 and validating the subscriber-to-provider path.

The corrected implementation maintained:

* Subscriber isolation
* Layer 3 switching
* Customer Edge NAT/PAT
* Default routing
* ISP aggregation

The final topology was successfully tested using ICMP connectivity checks.

Final Network Architecture

The final implementation consists of three logical layers.

Subscriber Layer

Residential networks using private IPv4 addressing and Customer Edge gateways.

FNO Aggregation Layer

A Cisco 3560 multilayer switch provides:

* VLAN segmentation
* Layer 3 switching
* Subscriber gateway interfaces
* Traffic forwarding between network segments

ISP Provider Layer

The ISP-BRAS router represents the ISP aggregation point and provides the upstream provider-side connection.

Final Physical Interconnections

Device	Interface	Connected To
PC-A	Fa0	Client-Home-A Gi0/1
Client-Home-A	Gi0/0	Core-L3-Switch Fa0/1
Client-Home-B	Gi0/0	Core-L3-Switch Fa0/2
Core-L3-Switch	Gi0/1	ISP-BRAS Gi0/0


VLAN and IP Architecture

VLAN	Subscriber	Network	Core Gateway
VLAN 10	Client A	198.51.100.0/24	198.51.100.1
VLAN 20	Client B	198.52.100.0/24	198.52.100.1

The VLANs provide logical separation between subscriber traffic while allowing the same physical infrastructure to support multiple customers.

Core Multilayer Switch Configuration

enable
configure terminal
hostname Core-L3-Switch

! Enable Layer 3 routing
ip routing

! Create subscriber VLANs
vlan 10
 name Client-A-VLAN
exit
vlan 20
 name Client-B-VLAN
exit

! VLAN 10 SVI
interface vlan 10
 ip address 198.51.100.1 255.255.255.0
 no shutdown
exit

! VLAN 20 SVI
interface vlan 20
 ip address 198.52.100.1 255.255.255.0
 no shutdown
exit

! Client A access port
interface FastEthernet 0/1
 switchport mode access
 switchport access vlan 10
 no shutdown
exit

! Client B access port
interface FastEthernet 0/2
 switchport mode access
 switchport access vlan 20
 no shutdown
exit

! Upstream ISP connection
interface GigabitEthernet 0/1
 switchport mode access
 switchport access vlan 10
 no shutdown
exit


Customer Edge — Client Home A

The Customer Edge router separates the private home LAN from the provider-facing WAN.

WAN

198.51.100.10/24

LAN

192.168.1.1/24

The router performs NAT overload so that private subscriber addresses can use the WAN interface address when communicating outside the home network.

Customer Edge Configuration

enable
configure terminal
hostname Client-Home-A

! WAN interface
interface GigabitEthernet 0/0
 ip address 198.51.100.10 255.255.255.0
 ip nat outside
 no shutdown
exit

! LAN interface
interface GigabitEthernet 0/1
 ip address 192.168.1.1 255.255.255.0
 ip nat inside
 no shutdown
exit

! DHCP pool
ip dhcp pool HOME-POOL-A
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
exit

! NAT source network
access-list 1 permit 192.168.1.0 0.0.0.255
! NAT overload
ip nat inside source list 1 interface GigabitEthernet 0/0 overload
! Default route
ip route 0.0.0.0 0.0.0.0 198.51.100.1


ISP Aggregation Node

The ISP-BRAS represents the provider-side aggregation point.

enable
configure terminal
hostname ISP-BRAS
interface GigabitEthernet 0/0
 ip address 198.51.100.2 255.255.255.0
 no shutdown
exit

Subscriber Traffic Flow

The intended traffic path is:

PC-A
  |
  | Private IP
  v
Client-Home-A
  |
  | NAT/PAT
  v
Core-L3-Switch
  |
  | VLAN 10
  v
ISP-BRAS

The lab demonstrates how private subscriber traffic is translated at the Customer Edge before proceeding toward the provider-facing network.


Verification and Troubleshooting

1. Verify Interface Status

On the Customer Edge router:

show ip interface brief

The relevant interfaces should show:

GigabitEthernet0/0    up    up
GigabitEthernet0/1    up    up

This confirms that both the WAN and LAN interfaces are operational.

2. Verify VLAN Configuration

On the Core Layer 3 switch:

show vlan brief

Confirm that the subscriber access ports are assigned to their intended VLANs.

3. Verify Layer 3 Interfaces

show ip interface brief

The SVIs should be operational:

Vlan10    198.51.100.1    up    up
Vlan20    198.52.100.1    up    up

4. Verify Routing

On the Customer Edge router:

show ip route

The default route should point toward:

198.51.100.1

5. Verify NAT

After generating traffic from the subscriber LAN:

show ip nat translations

This allows the translated sessions to be inspected and confirms whether NAT/PAT is being triggered.

Connectivity Testing

From PC-A:

PC-A> ping 198.51.100.1

Part 1 Result

Request timed out.

This indicated that the initial configuration required further troubleshooting.

Part 2 Result

100% successful
0% packet loss

The corrected implementation successfully established connectivity between the subscriber network and the Layer 3 core gateway.


Troubleshooting Lessons

The main lesson from this project was that successful network implementation is not only about entering configuration commands.

The troubleshooting process required checking the complete traffic path:

End Device
   ↓
Customer Edge
   ↓
NAT
   ↓
VLAN
   ↓
Layer 3 Core
   ↓
Provider Network

A failure at any stage can prevent end-to-end connectivity.

The Part 1 failure provided an opportunity to practice structured fault isolation rather than simply rebuilding the topology.

Key Technologies Demonstrated

* Cisco Packet Tracer
* IPv4 addressing
* VLAN segmentation
* Layer 3 switching
* Switch Virtual Interfaces (SVIs)
* Inter-VLAN routing
* DHCP
* NAT
* PAT / NAT overload
* Static default routing
* ICMP troubleshooting
* Interface verification
* Network fault isolation


Professional Competencies

This project demonstrates practical experience with:

* Troubleshooting network connectivity
* Identifying Layer 2 and Layer 3 issues
* Subscriber traffic segmentation
* Customer Edge configuration
* NAT/PAT implementation
* Layer 3 switching
* VLAN-based traffic isolation
* Provider-edge concepts
* Structured network verification
* Translating network theory into a practical lab environment

Evidence

The repository includes Cisco Packet Tracer topology screenshots and/or .pkt files demonstrating the implementation and verification of the lab.

The screenshots document both the initial troubleshooting stage and the final successful configuration.

Project Outcome

This two-part project provided a practical simulation of how residential subscriber traffic can be carried through an access and aggregation infrastructure toward an ISP edge.

Part 1 focused on building the initial environment and identifying a connectivity failure.

Part 2 focused on correcting the implementation, validating the configuration, and achieving successful connectivity.

The project strengthened my understanding of VLAN segmentation, Layer 3 switching, NAT/PAT, default routing, and systematic network troubleshooting within a simulated ISP environment.
