CCNA Lab: IPv6 Static Routing & End-to-End Connectivity

A hands-on Cisco Packet Tracer lab focused on IPv6 addressing, static routing, route verification, and end-to-end connectivity.

IPv6 Addressing

* PC-A LAN: 2001:DB8:AAAA:1::/64
* Inter-Router WAN: 2001:DB8:AAAA:2::/64
* PC-B LAN: 2001:DB8:AAAA:3::/64
<img width="1361" height="718" alt="Screenshot 2026-10-03 105621" src="https://github.com/user-attachments/assets/6c2d79b3-ec5e-459b-90a6-0bab4efeffa4" />

Configuration

The following were implemented:

1. Enabled IPv6 routing with:
    ipv6 unicast-routing
2. Configured IPv6 global unicast addresses on the router interfaces.
3. Configured static routes to reach the remote IPv6 networks using:
    ipv6 route
4. Verified the routing table with:
    show ipv6 route
5. Tested end-to-end connectivity using:
    ping

Verification

From PC-A, test connectivity to PC-B:

ping 2001:DB8:AAAA:3::10

A successful ping confirms end-to-end IPv6 connectivity across the routed network.

 How to Use This Lab

1. Download the .pkt file from this repository.
2. Open it using Cisco Packet Tracer.
3. Review the router interface configurations.
4. Use the verification commands to confirm the IPv6 routes.
5. From PC-A, run the ping command to verify connectivity.

CCNA Skills Practiced

* IPv6 Addressing
* Global Unicast Addresses
* IPv6 Static Routing
* Next-Hop Routing
* IPv6 Routing Table Verification
* ICMPv6 Connectivity Testing
* Cisco IOS CLI
* Cisco Packet Tracer

🚀 Next Lab

Part 2: IPv6 OSPFv3 Dynamic Routing
