# OWLS Network Layer: Agnostic Mesh & Bridging
**Version:** 0.1.3-alpha  
**Status:** Draft / Technical Specification (Platform Agnostic)

This document defines the communication framework for Project OWLS. The network is designed as a modular, peer-to-peer system that facilitates spatial discovery, real-time telemetry, and synchronized display coordination across diverse hardware platforms.

---

## 1. The Core Mesh
The OWLS Network is a single, unified mesh responsible for three primary services. It is designed to run on ubiquitous wireless protocols (primarily BLE), ensuring that any modern radio-enabled device can participate.

### A. Localization (Spatial Discovery)
* **Mechanism:** Periodic "Heartbeats" emitted by all nodes.
* **Data:** Contains `Node_ID`, `Confidence_Score`, and `Protocol_Version`.
* **Function:** Nearby nodes utilize the RSSI (Signal Strength) of these heartbeats to build a local neighbor table, allowing for relative distance estimation without external infrastructure.

### B. Display Messaging (Visual Coordination)
* **Mechanism:** Vectorized command propagation.
* **Data:** Packets containing spatial instructions (e.g., "All nodes at Hop-Distance 5, Fade to Gold").
* **Function:** Triggers visual responses across the crowd. These messages are designed to be extremely "lean" to minimize airtime and latency.

### C. Telemetry (State Reporting)
* **Mechanism:** Upstream gossip/propagation.
* **Data:** Battery health, neighbor density, and current coordinate confidence.
* **Function:** Allows the network (and the "Conductor" at the Anchor) to monitor the health and density of the mesh in real-time.



---

## 2. The Backhaul (Performance Extension)
While the Core Mesh is the essential "plumbing," the **Backhaul** is an optional architectural addition used to increase throughput and decrease latency in massive installations.

* **Modular Integration:** If a device supports a higher-bandwidth protocol (e.g., **ESP-NOW, Wi-Fi, Thread, or LoRa**), it can use that protocol to "tunnel" Core Mesh packets more efficiently.
* **Long-Distance Bridges:** Backhaul-enabled nodes can act as "super-nodes" that jump data across large physical gaps that the standard Discovery radio might not reach.
* **Transparent Logic:** The Application Layer remains unaware of whether a packet traveled via the Core Mesh or a Backhaul link.

---

## 3. Network Topology: The "Hyphae" Model
The network is an ad-hoc, peer-to-peer structure that functions without a central coordinator or fixed infrastructure.

* **Topological Fluidity:** Nodes join and leave the swarm dynamically. The "shape" of the network is defined by the physical proximity of its participants.
* **Abstracted Node Roles:**
    * **Anchor:** A node with a known reference (e.g., fixed power, stage-linked) that serves as a timing or spatial origin.
    * **Participant:** A standard node that both consumes and relays mesh data.
    * **Gateway:** A bridge node (like a smartphone or laptop) that injects external control data into the mesh.

---

## 4. Addressing & Spatial Propagation
OWLS avoids unique ID-based routing (like IP or MAC addresses) in favor of **Spatial Flooding**.

* **Neighbor-Relative Routing:** Messages propagate based on their relationship to the "Origin" or "Target Area." 
* **Managed Flooding:**
    * **TTL (Time to Live):** Prevents infinite loops by limiting the number of times a packet can be relayed.
    * **Deduplication:** Nodes cache recent `Packet_IDs` and discard duplicates to minimize radio congestion.
    * **Jittered Rebroadcast:** Nodes wait a randomized interval before relaying a packet to prevent "packet collisions" when multiple nodes hear the same signal simultaneously.

---

## 5. Packet Structure (Draft)
The OWLS Network Frame is optimized for the smallest common denominator (e.g., a 31-byte BLE Advertising payload).

| Byte Offset | Field | Description |
| :--- | :--- | :--- |
| 0 | `PROTOCOL_VER` | OWLS Version (e.g., 0x01) |
| 1-2 | `SOURCE_ID` | Shortened 16-bit hash of the sender's UID |
| 3 | `MSG_TYPE` | Heartbeat (Local), Display (Vector), Telemetry, or Sync |
| 4 | `AUTHORITY` | Weighted permission level (0-255) |
| 5-20 | `PAYLOAD` | Spatial vectors, color states, or telemetry metrics |
| 21-22 | `CRC` | Integrity check for data validation |

---

## 🤝 Technical Challenges (Platform Agnostic)
* **Congestion Control:** Maintaining network health when 50+ nodes are broadcasting Display and Telemetry messages within a 5-meter radius.
* **Clock Drift:** Establishing a low-overhead method for nodes to maintain a shared "Global Time" across various hardware crystal oscillators.
* **Power Optimization:** Balancing the frequency of Telemetry reporting with the need to preserve battery for the Display logic.
