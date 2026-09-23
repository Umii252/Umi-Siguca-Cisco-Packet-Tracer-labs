EtherChannel & LACP Troubleshooting

Overview

A Cisco Packet Tracer lab focused on configuring and troubleshooting EtherChannel using LACP between four Cisco 2960 switches.

What I Practiced

* Configured LACP EtherChannels
* Configured Port-Channels as trunk links
* Verified EtherChannel status
* Simulated a physical link failure
* Troubleshot a missing cable
* Restored the physical connection
* Verified that the interface successfully rejoined the EtherChannel
* Observed how STP manages redundant paths

Troubleshooting Commands
<img width="1346" height="584" alt="Screenshot 2026-09-23 133108" src="https://github.com/user-attachments/assets/12f69964-abb4-44c5-ba5e-06b44167b082" />

show interfaces fa0/3 status
show running-config interface fa0/3
show etherchannel summary
show interfaces trunk
show spanning-tree

Key Learning

This lab helped me understand how to troubleshoot physical connectivity and verify EtherChannel and LACP operation in a redundant switched network.

Technologies

* Cisco Packet Tracer
* Cisco 2960 Switches
* EtherChannel
* LACP
* STP
* Trunking
