### Cisco Enterprise Layer 2 VTP & DTP Infrastructure Lab

An implementation of an enterprise switching architecture using Cisco Catalyst 2960 switches inside Cisco Packet Tracer. This lab validates secure trunking protocols, automated VLAN scaling, and database propagation rules across different VTP modes. 

Network Topology



  ┌──────────────────┐   802.1Q Trunk    ┌──────────────────┐   802.1Q Trunk    ┌──────────────────┐
  │       SW1        ├───────────────────┤       SW2        ├───────────────────┤       SW3        │
  │   (VTP Server)   │   (DTP: Disabled) │ (VTP Transparent)│   (DTP: Disabled) │   (VTP Client)   │
  └──────────────────┘                   └──────────────────┘                   └──────────────────┘
<img width="1360" height="719" alt="Screenshot 2026-11-03 125427" src="https://github.com/user-attachments/assets/84ab3308-c7d9-401d-9b1e-a3c75b7a19ad" />

Use code with caution.

### Lab Objectives

* **DTP Mitigation:** Manually establish deterministic trunk links and systematically turn off Dynamic Trunking Protocol (DTP) to protect against VLAN hopping risks.
* **VTP Domain Scaling:** Configure centralized VLAN management utilizing VTP Server, Client, and Transparent states.
* **Database Security Check:** Verify database locking mechanisms on VTP Client switches to ensure centralized configuration management integrity.

### Configuration Quick-Reference

### VLAN Architecture

Switch NameVTP ModeVTP DomainLocal VLAN DatabaseNotes
****SW1****
ServerCCNAVLANs 10, 20, 30Central management point. Increments revision numbers.
****SW2****
TransparentCCNAVLAN 40 onlyIgnores incoming updates but passes VTP packets to SW3.
****SW3****
ClientCCNAVLANs 10, 20, 30Synchronizes with SW1 database automatically. Local edits blocked.

### Essential Verification Commands

To test the environment and replicate lab results, execute the following commands on the CLI: 

ios

! Verify trunk status and ensure DTP negotiation is disabled
show interfaces fastEthernet 0/24 switchport

! Analyze VTP database synchronization and configuration revision numbers
show vtp status

! Output active layer 2 interface bindings
show vlan brief

Use code with caution.

### Verification Milestones Passed

1. **DTP Hardening:** Negotiation of Trunking: Off confirmed on all inter-switch links.
2. **Server-to-Client Propagation:** SW3 dynamically inherits VLANs 10, 20, and 30 over trunk links despite parsing through an isolated, VTP Transparent relay (SW2).
3. **Database Isolation:** SW2 ignores SW1's updates and maintains its isolated local VLAN database (VLAN 40), proving Transparent mode functionality.
4. **Database Security:** SW3 successfully throws a VTP validation block when manually trying to inject configurations locally while in Client mode.
