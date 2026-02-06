# CAN_Notes
notes related to CAN


### 1. What is CAN?
- **CAN (Controller Area Network)** is a robust serial communication protocol designed for real-time data exchange between Electronic Control Units (ECUs) in vehicles and industrial automation.
- Developed by Bosch in the 1980s, now a global standard in automotive and embedded systems.

---

### 2. Why CAN? (Key Reasons)
- Needed for reliable, fast, and noise-immune communication among multiple ECUs in vehicles.
- **Multimaster & Asynchronous:** Any node can start communication at any time.
- **High noise immunity:** Uses dual twisted pair wiring.
- **Low latency:** Small frame size (8 bytes data) ensures quick transmission.
- **Highly reliable:** Built-in error detection and handling.

---

### 3. CAN Properties & Features

| Property         | CAN Protocol Details                          |
|------------------|----------------------------------------------|
| Type             | Serial, Wired, Asynchronous                  |
| Topology         | Bus (dual twisted pair)                       |
| Speed            | Up to 1 Mbps (standard CAN)                  |
| Data per Frame   | 8 bytes                                      |
| Communication    | Multicast (message-based, not node-based)    |
| Fault Tolerance  | High                                         |
| Protocol         | CSMA-CA (Carrier Sense Multiple Access - Collision Avoidance) |
| Acknowledgement  | Special field in every frame, no extra frame  |
| Filtering        | Message filtering based on Message ID         |

---

### 4. CAN vs. Other Protocols

| Feature         | CAN         | FlexRay     | Ethernet      |
|-----------------|-------------|-------------|---------------|
| Bus Type        | Dual twisted pair | Dual twisted pair | Wire/Optical Fibre |
| Speed           | 1 Mbps      | 10 Mbps     | 100 Mbps+     |
| Data per Frame  | 8 bytes     | 264 bytes   | 1500 bytes    |
| Type            | Asynchronous| Synchronous | Point-to-point|
| Fault Tolerance | High        | Medium      | Low           |

---

### 5. Communication Modes

- **Wired vs. Wireless:** CAN is a wired protocol (Ethernet is another example; wireless includes Bluetooth, WiFi).
- **Peer-to-Peer vs. Broadcast:** CAN is multicast (similar to broadcast, one-to-many), not strictly peer-to-peer.
- **Message-Based:** Each frame is identified by a Message ID (not by sender/receiver node).



### 1. CAN Bus Physical Layer

- **Dual-Twisted Pair Wires:** CAN_H (High) and CAN_L (Low) for differential signaling.
- **Termination:** Both ends of the bus are terminated with 120-ohm resistors for impedance matching and noise immunity.
- **Why Twisted Pair?**
  - Reduces electromagnetic interference (EMI).
  - Ensures signal integrity over long distances.


---

### 2. CAN Logic Levels

| Bit Type    | CAN_H | CAN_L | Delta V (V) | Description      |
|-------------|-------|-------|-------------|------------------|
| Recessive   | 2.5V  | 2.5V  | 0           | Logical "1"      |
| Dominant    | 3.5V  | 1.5V  | 2           | Logical "0"      |

- **Dominant bit (Logic 0):** CAN_H > CAN_L (bus actively driven)
- **Recessive bit (Logic 1):** CAN_H = CAN_L (bus idle)



---

### 3. CAN Speed & Data Rate

- **Maximum Speed:** Up to 1 Mbps (for bus length ≤ 40 meters).
- **Industry Standard:** Often set at 500 kbps for reliability.
- **Speed vs. Length:** As bus length increases, max speed decreases.

| Bus Length (m) | Max Bit Rate (kbps) |
|----------------|---------------------|
| 10             | 1000                |
| 40             | 1000                |
| 100            | 500                 |
| 200            | 250                 |
| 1000           | 50                  |
| 10,000         | 5                   |


---

### 4. CAN Frame Structure

- **Frame Parts:** PCI (Protocol Control Information) + Data.
- **Data Size:** Each frame can carry 0 to 8 bytes (not bits).
- **No Bit-Level Data:** Data is always in bytes; cannot send 2 or 27 bits, only full bytes.

---

### 5. CAN Controllers & Transceivers

- **Microcontrollers:** Work with TTL logic, not CAN logic directly.
- **CAN Controller:** Handles protocol, message filtering, buffering.
- **CAN Transceiver:** Converts TTL signals to CAN bus differential signals.

---

### 6. CAN Network Topology

- **Bus Topology:** Most common; all ECUs connected to the same bus.
- **Scalability:** Supports multiple ECUs (nodes) easily.
- **Reliability:** Robust against electrical noise and failures.


### 7. Data Transmission Example

- **Baud Rate:** 500 kbps → 500,000 bits/sec.
- **Frame Size:** ~125 bits/frame (without bit stuffing).
- **Frames per Second:** ~2000 frames/sec (500,000 / 125).


### 9. Quick Summary Table

| Feature                | Details                                      |
|------------------------|----------------------------------------------|
| Physical Layer         | Dual-twisted pair, 120Ω termination          |
| Logic Levels           | Dominant (0), Recessive (1)                  |
| Max Speed              | 1 Mbps (≤40m), 500 kbps typical              |
| Data Size per Frame    | 0–8 bytes                                   |
| Topology               | Bus (linear), multi-node                     |
| Controller/Transceiver | TTL logic, protocol handling, signal conversion |

---

### 10. Real-World Use Case

> In modern cars, CAN connects ECUs for engine control, ABS, airbags, and infotainment. If one ECU fails, others can still communicate, ensuring safety and reliability.




