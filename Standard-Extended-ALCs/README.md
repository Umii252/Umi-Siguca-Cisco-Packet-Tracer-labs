Standard and Extended Access Control Lists (ACLs)

Objective

Configure and verify Standard and Extended IPv4 Access Control Lists (ACLs) on Cisco IOS routers to:

* Enforce security boundaries
* Restrict administrative access
* Filter traffic based on source, destination, and protocol ports

IP Addressing Plan

Network	Address	Gateway
Site A LAN	192.168.10.0/26	192.168.10.62
DMZ Network	192.168.10.128/28	192.168.10.142
WAN Link	192.168.10.144/30	—

DMZ Servers

* Web/HTTP Server: 192.168.10.130
* Secure FTP Server: 192.168.10.131

WAN Interfaces

* R1 Gig0/1: 192.168.10.145
* R2 Gig0/1: 192.168.10.146

Lab Tasks

Task 1: Standard ACL — VTY Line Hardening

* Create a numbered Standard ACL (1–99) on R1.
* Permit only the administrative host 192.168.10.5.
* Restrict Telnet/SSH access to the router.
* Deny all other administrative access.
* Apply the ACL to the VTY lines using access-class.

Task 2: Extended ACL — DMZ Traffic Filtering

Create a named Extended ACL:

FILTER_DMZ_TRAFFIC

Configure the ACL to:

* Permit Site A hosts to access the Web Server 192.168.10.130 using HTTP (port 80).
* Block Site A hosts from accessing the FTP Server 192.168.10.131.
* Permit all other traffic.
* Apply the ACL to the correct interface and direction.

Verification Commands

show access-lists

Displays ACL entries and match counters.

show ip interface <interface>

Displays ACLs applied to an interface and their direction.

Skills Demonstrated

* Standard IPv4 ACLs
* Extended IPv4 ACLs
* VTY line security
* Telnet/SSH access control
* Traffic filtering
* DMZ security
* HTTP and FTP filtering
* Cisco IOS configuration
* ACL verification and troubleshooting
* Cisco Packet Tracer
