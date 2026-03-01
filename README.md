# 🦉 OWLS 🦉 - Open Wireless Lighting Standard

**A decentralized, protocol-agnostic framework for spatial lighting coordination in high-density crowds.**

---

## 🌟 The Vision
Project OWLS is an open-source initiative to move beyond centralized proprietary control systems for synchronized crowd illumination hardware. Instead of a single master transmitter, we are building a **Decentralized Mesh**  — an organic, self-organizing network anyone can join or add onto. Where the crowd itself is the infrastructure and simultaniusly the medium for artistic expression.

Our goals are
- To foster the developmenty an evolution of a new standard that allows thousands of individual nodes to react as a single, living organism.
- Creating the technical pillars of this system; localization and messaging to initiate spatial lighting effects.
- Documenting and provide refrence for new artists to adopt the standard. Including it in thier creations, expanding the networks reach.

---

## 🏗️ The Layered Architecture

To achieve a truly universal standard, we are developing Project OWLS in two distinct, decoupled layers:

### 1. The Bridged Mesh Layer (The Foundation)
The "plumbing" of the system. This layer handles the heavy lifting of ad-hoc networking and peer-to-peer communication.
* **Protocol Bridging:** Abstracting the transport layer so that nodes can communicate regardless of the underlying RF protocol (BLE, Wi-Fi, Sub-GHz, etc.).
* **Relative Localization:** Developing models for nodes to determine their physical coordinates within a crowd (e.g., using RSSI, Time-of-Flight, or neighbor-density) without relying on GPS or external anchors.
* **Telemetry:** Feedback on the density and speed of the mesh allowing a Condcutor to get feedback on how quickly or precicely they can they can coordinate the mesh display.


### 2. The OWLS Application Layer
The standardized "language" that runs atop the mesh. 
* **Spatial Addressing:** Sending commands to physical areas (e.g., "All nodes in the North-East quadrant") rather than specific device IDs.
* **Coordination Patterns:** Defining how the mesh executes complex, multi-node behaviors like waves, pulses, and gradients.
* **Permissioned Authority:** A weighted consensus model that balances individual agency with "Conductor" (Artist) overrides for synchronized show moments.

---

## 🧪 Open Challenges & Collaboration
We are in the **Concept & Proof of Concept** phase. We are seeking input from engineers, researchers, and creative technologists on the following:

* **High-Density Scaling:** How do we maintain mesh stability with 20,000+ active nodes in a single stadium?
* **Efficient Localization Math:** What are the most computationally "cheap" ways for a low-power node to calculate its relative position in 3D space?
* **Standardization:** How do we define the bridge so that disparate hardware types can seamlessly join the same "swarm"?
* **Simplicity:** How do we make the experience for the user as simple as possible when they want to join a "swarm"?

---

## 🤝 Join the Swarm
This is an invitation to innovate. We believe the future of live experiences belongs to the collective, not a proprietary black box.

* **Contribute:** Check out [Issues](/issues) and [Projects](/projects) to help define the initial spec.
* **Build:** Help us develop the first reference implementations for the Bridged Mesh Layer.

*"The crowd is the canvas. Let’s build the brush."*

---

## 📜 License
Project OWLS is licensed under the [MIT License](LICENSE).
