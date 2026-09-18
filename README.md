# Umi-Siguca-Cisco-Packet-Tracer-labs
Hands-on Cisco Packet Tracer labs covering routing, switching, VLANs, DHCP, OSPF and network troubleshooting.
## Important Note for Testers / Reviewers

When opening any of these `.pkt` or `.pkz` files in Cisco Packet Tracer, the topology defaults to a cold boot state. Active memory (ARP tables and dynamic routing convergence) resets on launch. 

If you attempt to ping immediately upon opening a file, the first test will likely show a **Failed** status.

### How to properly verify the topology:
1. Ensure the workspace mode is set to **Realtime** (bottom-right corner corner selector).
2. Click the **Fast Forward Time (`>>`)** button 3–4 times (or press `Alt + D`). This instantly bypasses the Spanning Tree Protocol (STP) listening/learning states and allows OSPF paths to converge.
3. Clear the initial scenario block by clicking **Delete** in the PDU list window.
4. Send a new ping PDU packet between end-hosts. The first attempt may drop an initial packet for ARP discovery, but the subsequent pings will return a **Successful** status.
