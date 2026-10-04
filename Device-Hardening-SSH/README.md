Lab: Control Plane Hardening (Secure SSHv2 & Device Administration)

Objective

Harden the control plane of a Cisco Catalyst switch to secure administrative access.

This lab focuses on configuring a local high-privilege administrator account, generating RSA cryptographic keys, disabling insecure Telnet access, enforcing SSHv2 on virtual terminal lines, and implementing an explicit legal warning banner.

Topology 
<img width="1362" height="719" alt="Screenshot 2026-10-05 004326" src="https://github.com/user-attachments/assets/c3b96500-9e95-41f8-83de-40069ddff851" />

IP Addressing Plan

Device	Interface	IP Address	Subnet Mask
SW1-Hardened	VLAN 1 SVI	10.1.1.100	255.255.255.0
Admin-Workstation	NIC	10.1.1.10	255.255.255.0

Management Network: 10.1.1.0/24

CCNA Lab Tasks

Task 1: Initialize Management Access & Device Identity

* Configure interface vlan 1 with the management IP address.
* Configure the switch hostname as SW1-Hardened.
* Configure the local DNS domain name as corp.local.
* Ensure the management SVI is operational.

Task 2: Build the High-Privilege Local Account Database

* Create a dedicated network administrator account in the local user database.
* Assign the account Privilege Level 15.
* Configure a secure encrypted password.
* Configure an explicit legal MOTD banner warning against unauthorized access.

Task 3: Generate Cryptographic Keys

* Generate an RSA key pair.
* Use a minimum modulus size of 1024 bits.
* Confirm that the SSH process is enabled.
* Configure the switch to use SSH version 2.

Task 4: Secure the Virtual Terminal Lines

* Configure line vty 0 15.
* Authenticate users against the local username database.
* Disable incoming Telnet connections.
* Permit SSH only on the VTY lines.

Security Configuration Goals

The completed switch should enforce:

* Local authentication
* Privilege Level 15 administrative access
* SSHv2 remote management
* RSA encryption
* Telnet disabled
* SSH-only VTY access
* Legal warning banner
* Secure administrative access to the management SVI

Core Verification Commands

show ip ssh
show line vty 0 15
show running-config

From the Admin-Workstation, test SSH connectivity:

ssh -l <username> 10.1.1.100

Expected Outcome

The switch should accept authorized administrative connections through SSHv2 while rejecting insecure Telnet access.

The administrator should authenticate using the locally configured Privilege Level 15 account and receive the configured legal warning banner before accessing the device.

Skills Demonstrated

* Cisco IOS device hardening
* SSHv2 configuration
* RSA key generation
* Local AAA-style authentication concepts
* VTY line security
* Privilege levels
* Management SVI configuration
* Secure remote administration
* CCNA Security Fundamentals
