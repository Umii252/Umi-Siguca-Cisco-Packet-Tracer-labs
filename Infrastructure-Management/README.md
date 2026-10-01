Lab: Network Management & Operations (NTP, Syslog, CDP/LLDP)

Objective

Configure, verify, and monitor network management services across a multi-device Cisco network.

This lab focuses on:

* Network Time Protocol (NTP)
* Centralized Syslog logging
* Cisco Discovery Protocol (CDP)
* Link Layer Discovery Protocol (LLDP)
* Device management and verification

Topology Diagram

                 ┌──────────────────────┐
                 │   Centralized-SRV    │
                 │   NTP & Syslog       │
                 │   192.168.100.10     │
                 └──────────┬───────────┘
                            │
                         Fa0/24
                            │
                 ┌──────────┴───────────┐
                 │       SW1-Switch     │
                 │  VLAN 1: .100        │
                 └──────┬─────────┬─────┘
                        │         │
                     G0/1       G0/2
                        │         │
                 ┌──────┴───┐ ┌──┴──────────┐
                 │ R1-Gateway│ │ R2-Branch  │
                 │ .100.1    │ │ .100.2     │
                 └───────────┘ └─────────────┘

IP Addressing Plan

Device	Interface	IP Address	Subnet Mask
Centralized-SRV	NIC	192.168.100.10	255.255.255.0
SW1	VLAN 1	192.168.100.100	255.255.255.0
R1	G0/1	192.168.100.1	255.255.255.0
R2	G0/2	192.168.100.2	255.255.255.0

Management Network: 192.168.100.0/24

CCNA Lab Tasks

Task 1: Centralized Server Services

Configure the centralized server to provide:

* NTP
* Syslog

Set a manual date and time on the NTP server and assign the server the static address:

192.168.100.10/24

Verify that all devices can reach the server using ICMP.

Task 2: Network Time Protocol (NTP)

Configure R1, R2, and SW1 to synchronize their clocks with:

192.168.100.10

Verify synchronization using:

show ntp status
show ntp associations

Confirm that the devices are receiving time from the centralized NTP server.

If supported by the Packet Tracer device image, configure NTP authentication to provide additional protection against unauthorized time sources.

Task 3: Centralized Syslog

Configure R1, R2, and SW1 to send system messages to:

192.168.100.10

Set the logging trap level to:

informational

Generate test log messages by shutting down and re-enabling an interface.

Example:

interface g0/1
shutdown
no shutdown

Verify the local logging configuration with:

show logging

Then confirm that the events are received by the centralized Syslog server.

Task 4: CDP Neighbor Discovery

Use Cisco Discovery Protocol to identify directly connected Cisco devices.

Verify neighbors with:

show cdp neighbors
show cdp neighbors detail

Review:

* Neighbor device ID
* Local interface
* Neighbor interface
* Platform
* Capabilities

Disable CDP on user-facing access ports where appropriate:

interface fa0/1
no cdp enable

Task 5: LLDP Neighbor Discovery

Enable LLDP globally:

lldp run

Verify discovered neighbors with:

show lldp neighbors
show lldp neighbors detail

Compare the information provided by CDP and LLDP.

Core Verification Commands

NTP

show ntp status
show ntp associations

Syslog

show logging

CDP

show cdp neighbors
show cdp neighbors detail

LLDP

show lldp neighbors
show lldp neighbors detail

Connectivity

ping 192.168.100.10

Expected Results

* R1, R2, and SW1 successfully synchronize with the centralized NTP server.
* Network devices send Syslog messages to the centralized server.
* Interface state changes generate corresponding log messages.
* CDP correctly identifies directly connected Cisco neighbors.
* LLDP discovers supported neighboring devices.
* User-facing access ports do not unnecessarily advertise CDP information.

Skills Demonstrated

* NTP configuration and verification
* Centralized network logging
* Syslog configuration
* CDP neighbor discovery
* LLDP neighbor discovery
* Layer 2 device management
* Network troubleshooting
* Cisco IOS verification commands
* Infrastructure monitoring

CCNA Topics Covered

* Network Management
* NTP
* Syslog
* CDP
* LLDP
* Device Monitoring
* Network Operations
* Troubleshooting and Verification
