# OWLS Application Layer: Core Pillars
**Version:** 0.1.2-alpha  
**Status:** Concept / Refined for Relative Localization

This document defines the logical architecture of Project OWLS. Unlike traditional systems that rely on absolute GPS or fixed $XYZ$ coordinates, OWLS uses **Relative Spatial Mapping** to treat the crowd as an elastic, self-aware manifold.

---

## 1. The Vectorized Display (Relative Implementation)
The crowd is a canvas, but the canvas is dynamic—it stretches, bends, and flows as people move.

* **Relational Rendering:** Commands are defined by their behavior across the mesh "fabric" rather than fixed points in space.
    * *Example:* A "Wave" isn't defined by meters, but by **Link Distance**. A command might be: *"Propagate Blue light to all nodes within 10 hops of the trigger node."*
* **Relative Gradients:** Instead of "Turn Red at $x=10$," the command is "Create a gradient from the Stage-Anchor to the furthest Edge-Nodes." The nodes calculate their color based on their **normalized depth** within the network (e.g., $CurrentHop / MaxHop$).



---

## 2. Relative Localization (The "Neighbor" Model)
Nodes do not need to know where they are in the world; they only need to know where they are in the **Swarm**.

* **Proximity Tables:** Every node maintains a "Neighborhood Table" consisting of its immediate peers and their signal strengths (RSSI). 
* **Topological Positioning:** By comparing neighbor lists and signal weights, a node determines its "Centrality":
    * **Inner Nodes:** High neighbor count, surrounded by signals on all sides.
    * **Edge Nodes:** Low neighbor count, signals originating primarily from one hemisphere.
* **Hop-Count Distance:** The "Origin" (usually the Artist or a Stage Anchor) broadcasts a heartbeat. Each node increments a counter as the heartbeat passes through. A node's "location" is defined by its **Hop-Distance** and its **Signal-Weighted Angle** relative to its peers.

---

## 3. The Hybrid Backbone (Transport Bridging)
The Application Layer defines the "intent" of the message, allowing the Network Layer to handle the radio-specific delivery.

* **Protocol Transparency:** The logic (e.g., "Fade to Green over 2 seconds") is packaged identically whether it travels over BLE, ESP-NOW, or Wi-Fi.
* **Cross-Protocol Mesh:** If a node is at the edge of an ESP-NOW cluster but detects a BLE-only node, it automatically acts as a bridge, extending the "Relative Fabric" across protocol boundaries.

---

## 4. Permissioned Authority (The Trust Mesh)
In a relative system, authority is also distributed based on network "Mass."

* **Proximity-Based Influence:** A fan node may be granted permission to trigger a "Local Ripple" (nodes within 3 hops), but only the Artist (Level 0) can send a "Global Pulse" that traverses the entire mesh.
* **Consensus Validation:** Before a node repeats a "Relative Move" command from a peer, it checks with its neighborhood. If the majority of neighbors haven't seen the trigger, the node may treat it as an outlier to prevent accidental triggers or "griefing."

---

## 5. Temporal & Spatial Synchronization
Because data propagation through a mesh takes time, the system must account for "Propagation Velocity."

* **Intentional Latency:** We can calibrate the data propagation to match a desired visual speed. To create a "Ripple" that moves at a human-perceivable pace, the Application Layer calculates a specific delay-per-hop based on neighbor proximity.
* **Relative Time-Sync:** Nodes synchronize their internal clocks to the nearest high-authority Anchor. This ensures that when a "Vector" command is issued, nodes can execute it at a synchronized "Global Mesh Time" rather than just when the packet arrives.

---

## 🤝 Open Research Questions
1. **RSSI Smoothing:** How do we filter out "body blocking" (people moving between nodes) so it doesn't drastically change the calculated relative distance?
2. **Hop-Count Precision:** How do we handle "Short-Cuts" (a high-power node broadcasting further than intended) to keep the relative manifold accurate?
3. **Manifold Mapping:** What is the simplest math for a node to determine if it is an "Edge Node" or a "Center Node" using only its local peer list?
