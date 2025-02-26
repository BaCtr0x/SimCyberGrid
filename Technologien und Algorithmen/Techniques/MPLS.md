**Multiprotocol Label Switching (MPLS)** is a **high-performance routing technique** that directs network traffic using **labels** instead of traditional IP routing. It enhances **speed, scalability, and reliability** by reducing the need for complex lookups in a routing table.

MPLS is widely used in **WANs, service provider networks, and enterprise networks** to optimize data transfer, ensure **[[Quality of Service]] (QoS)**, and support **VPNs**.

### How MPLS Works
MPLS sits between **Layer 2 (Data Link) and Layer 3 (Network)**, often called a **“Layer 2.5” protocol**. It replaces IP routing with **label switching**, making packet forwarding **faster and more efficient**.
1. **Label Assignment**
	- When a packet enters an MPLS network, it is assigned a **label** by the first MPLS router (Label Edge Router - LER).
	- The label is inserted into the packet **before the IP header**.
	
2. **Label Switching**
	- Instead of performing IP lookups at every router, packets are forwarded based on their **label**.
	- Intermediate routers (Label Switch Routers - LSRs) **swap labels** instead of examining IP addresses.
	
3. **Label Removal & Packet Delivery**
	- When the packet reaches the final router (LER), the **label is removed**, and the packet is forwarded to its destination using normal IP routing.


### Key MPLS Components
| **Component**                          | **Function**                                                                           |
| -------------------------------------- | -------------------------------------------------------------------------------------- |
| **Label Edge Router (LER)**            | Assigns and removes MPLS labels at the network edge.                                   |
| **Label Switch Router (LSR)**          | Forwards packets based on labels within the MPLS core.                                 |
| **Forwarding Equivalence Class (FEC)** | A group of packets treated similarly (same path, QoS, etc.).                           |
| **Label Distribution Protocol (LDP)**  | Distributes label mapping information among MPLS routers.                              |
| **MPLS Label Stack**                   | Contains labels that guide packet forwarding (supports multiple labels for tunneling). |

### Step-by-Step MPLS Packet Forwarding
**Example Scenario**: A user in New York accesses a cloud service hosted in Los Angeles over an MPLS network.
1. **Packet Enters MPLS Network**
	- LER assigns an **MPLS label** (e.g., 101) and forwards the packet.
	
2. **Label Switching (MPLS Core)**
	- LSRs forward the packet based on the **label (101 → 202 → 303)** instead of the IP header.
	- Each LSR **swaps** the label for the next hop.
	
3. **Packet Exits MPLS Network**
	- The final LER removes the **MPLS label** and forwards the **original IP packet** to the destination.

### Advantages of MPLS
✔ **Faster Packet Forwarding** → Label switching is more efficient than traditional IP routing.
✔ **Traffic Engineering (TE)** → Directs traffic along optimized paths to **avoid congestion**.
✔ **Supports VPNs (MPLS VPN)** → Enables **secure, isolated** private networks.
✔ **Quality of Service (QoS)** → Ensures priority for voice/video traffic.
✔ **Scalability** → Handles large networks with minimal complexity.

### MPLS vs. Traditional IP Routing
| **Feature**                             | **MPLS**                 | **Traditional IP Routing**                 |
| --------------------------------------- | ------------------------ | ------------------------------------------ |
| **Forwarding Method**                   | Label-based switching    | Destination IP lookup                      |
| **Performance**                         | Faster                   | Slower due to IP lookup overhead           |
| **Traffic Engineering**                 | Optimized path selection | Limited control over paths                 |
| **[[Quality of Service\|QoS]] Support** | Strong                   | Limited                                    |
| **VPN Support**                         | MPLS VPNs (Layer 2 & 3)  | Requires additional tunneling (GRE, IPsec) |

 
 