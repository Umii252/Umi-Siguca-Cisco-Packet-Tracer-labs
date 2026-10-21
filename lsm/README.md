### ISP Network Expansion & VLSM Address Planning Lab

A production-grade Cisco Packet Tracer project showcasing how network engineers deploy Variable Length Subnet Masking (VLSM), design hierarchical static routing structures, and optimize IP address conservation for enterprise service providers. 

### Project Architecture

This infrastructure layout abandons generic classful subnetting models to solve a realistic corporate constraint: provisioning distinct user communities, corporate infrastructure, and point-to-point transit backbones inside a single allocated 10.20.30.0/24 address block. 

* R1 — ISP Core: Central transit hub steering multi-segment distribution.
* R2 — Residential Access A: Distribution gateway handling large user populations.
* R3 — Residential Access B/C: Multi-interface node managing small and medium communities.

### Engineered Addressing Matrix

* Residential Zone A
Network: 10.20.30.0/26
Mask: 255.255.255.192
Gateway: 10.20.30.1
Usable Range: 10.20.30.1 - 10.20.30.62
* Residential Zone B
Network: 10.20.30.64/27
Mask: 255.255.255.224
Gateway: 10.20.30.65
Usable Range: 10.20.30.65 - 10.20.30.94
* Residential Zone C
Network: 10.20.30.96/28
Mask: 255.255.255.240
Gateway: 10.20.30.97
Usable Range: 10.20.30.97 - 10.20.30.110
* Network Operations Centre (NOC)
Network: 10.20.30.112/29
Mask: 255.255.255.248
Gateway: 10.20.30.113
Usable Range: 10.20.30.113 - 10.20.30.118
* WAN Backbone Link 1 (R1-Core to R2)
Network: 10.20.30.120/30
Mask: 255.255.255.252
Usable Range: 10.20.30.121 - 10.20.30.122
* WAN Backbone Link 2 (R1-Core to R3)
Network: 10.20.30.124/30
Mask: 255.255.255.252
Usable Range: 10.20.30.125 - 10.20.30.126

### Engineering Deliverables & Validation

1. Resource Efficiency: Achieved a 50 percent total conservation rate, preserving 10.20.30.128/25 intact for clean future business allocation.
2. Routing Logic: Implemented default static routes on edge nodes pointing to the hub, combined with explicit remote network routing entries across the core.
3. Verification: Performed full Layer 3 protocol data unit simulation mapping, verifying reliable end-to-end ICMP transit between isolated broadcast domains.
