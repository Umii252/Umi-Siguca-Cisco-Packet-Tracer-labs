Lab: Access Layer Switch Hardening

Objective

Configure, verify, and troubleshoot Layer 2 security on a Cisco Catalyst 2960 switch using:

* Port Security
* Sticky MAC learning
* DHCP Snooping
* Trusted and untrusted switch ports

The lab demonstrates how to restrict unauthorized devices and prevent rogue DHCP servers from affecting users on the network.

IP Addressing

Device	Interface	IP Address
R1	G0/1	192.168.10.254/24
SW1	VLAN 10	192.168.10.0/24
PC-User	DHCP	Dynamic
Rogue DHCP Server	—	192.168.10.100/24

VLAN: 10
Subnet: 192.168.10.0/24

Lab Tasks

1. Port Security

Configure Fa0/1 and Fa0/2 as access ports.

On Fa0/1:

* Enable Port Security
* Allow a maximum of 1 MAC address
* Enable Sticky MAC learning

On Fa0/2:

* Enable Port Security
* Configure the violation mode as shutdown
* Test the port with an unauthorized device

2. DHCP Snooping

Configure DHCP Snooping on SW1.

* Enable DHCP Snooping globally
* Enable it for VLAN 10
* Configure Gi0/1 as a trusted DHCP port
* Keep access ports untrusted
* Connect a rogue DHCP server to Fa0/24
* Verify that unauthorized DHCP traffic is blocked

Verification Commands

Port Security

show port-security interface fa0/1
show port-security interface fa0/2
show port-security address

DHCP Snooping

show ip dhcp snooping
show ip dhcp snooping binding

Interface Status

show interfaces status
show running-config

Skills Demonstrated

* Cisco switch security
* Port Security
* Sticky MAC addresses
* MAC address violation handling
* DHCP Snooping
* Trusted and untrusted ports
* Layer 2 security troubleshooting
* Cisco IOS verification commands
* Rogue DHCP mitigation
