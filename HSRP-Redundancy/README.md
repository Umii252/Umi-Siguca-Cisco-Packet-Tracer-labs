Lab: First Hop Redundancy Protocol (FHRP) Using HSRP

Objective

Configure and verify Cisco Hot Standby Router Protocol (HSRP) to provide default gateway redundancy for internal LAN hosts.

The lab demonstrates HSRP active/standby roles and automatic failover when the active router becomes unavailable.

Topology
<img width="1244" height="601" alt="Screenshot 2026-09-30 105731" src="https://github.com/user-attachments/assets/86afdff8-2fae-48a6-aaf4-cc2b1e383d7d" />

* ISP Router
* R1 — HSRP Active
* R2 — HSRP Standby
* SW1 — LAN Switch
* PC-Host1
* PC-Host2

IP Addressing Plan

Device	Interface	IP Address
R1	G0/0	192.168.1.2/24
R2	G0/0	192.168.1.3/24
HSRP Virtual IP	—	192.168.1.1/24
PC-Host1	—	192.168.1.10/24
PC-Host2	—	192.168.1.11/24

Default Gateway for both PCs: 192.168.1.1

HSRP Configuration

* HSRP Version: 2
* HSRP Group: 1
* Virtual IP: 192.168.1.1
* R1 Priority: 110
* R2 Priority: 100
* R1 Preemption: Enabled

Lab Tasks

Task 1: Basic Connectivity

* Configure the LAN interfaces on R1 and R2.
* Configure the switch and end devices.
* Configure both PCs to use 192.168.1.1 as their default gateway.
* Verify basic connectivity between the PCs and their gateway.

Task 2: Configure HSRP

Configure HSRPv2 on both routers.

R1 should operate as the Active router with a priority of 110.

R2 should operate as the Standby router with the default priority of 100.

Enable preemption on R1 so that it can regain the Active role after recovering.

Task 3: Verify HSRP

Use the following commands:

show standby
show standby brief

Verify:

* HSRP group number
* Active router
* Standby router
* Virtual IP address
* Priority values
* HSRP state
* Virtual MAC address

Task 4: Test Failover

1. Start a continuous ping from a PC to a reachable destination.
2. Shut down R1’s LAN interface.
3. Observe the HSRP state change.
4. Verify that R2 becomes the Active router.
5. Confirm that the PC can still reach its destination using the same default gateway.
6. Restore R1’s interface.
7. Verify that R1 reclaims the Active role because preemption is enabled.

Key Concepts

* First Hop Redundancy Protocol (FHRP)
* HSRP
* HSRPv2
* Virtual IP Address
* Virtual MAC Address
* Active and Standby Router Roles
* Gateway Redundancy
* HSRP Priority
* Preemption
* Router Failover

Verification Commands

show standby
show standby brief
show ip interface brief
ping <destination-ip>

Expected Result

R1 operates as the HSRP Active router while R2 remains Standby.

When R1 becomes unavailable, R2 automatically transitions to Active, allowing LAN hosts to continue using 192.168.1.1 as their default gateway.

When R1 recovers, preemption allows it to regain the Active role.
