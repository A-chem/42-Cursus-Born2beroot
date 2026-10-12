[[image (11).svg]]
## **1. Source Port (16 bits)**

- Identifies the port number of the application sending the data.
- Example: A web browser might use a random port like **49152**.

## **2. Destination Port (16 bits)**

- Identifies the port number of the application on the receiving side.
- Example: A web server would typically use port **80** (HTTP) or **443** (HTTPS).

---

## **3. Sequence Number (32 bits)**

- Indicates the position of the first byte of data in the current segment relative to the entire data stream.
- **Purpose:**
    - Ensures proper order of data delivery.
    - Helps retransmit lost data during errors.
- Example: If sending a 1,000-byte file, sequence numbers track the position of each byte (e.g., 1–1000).

---

## **4. Acknowledgment Number (32 bits)**

- Used to confirm receipt of data.
- **When the ACK flag is set:**
    - Contains the next expected byte in the sequence from the sender.
    - Example: If segment **1** is received, the acknowledgment number will be **2** (x + 1).

---

## **5. Header Length (HLEN) (4 bits)**

- Specifies the size of the TCP header in **32-bit words**.
- **Range:**
    - Minimum: 5 (20 bytes).
    - Maximum: 15 (60 bytes, with options).

---

## **6. Reserved (4 bits)**

- Reserved for future use. All bits must be set to **0**.

---

## **7. Flgs (6 Control Bits)**

- Used to control the connection state.
    - **URG (Urgent):** Indicates that urgent data is present.
    - **ACK (Acknowledgment):** Acknowledgment field is valid (essential for reliable transmission).
    - **PSH (Push):** Data should be sent immediately to the application, bypassing buffering.
    - **RST (Reset):** Resets the connection in case of errors or unexpected states.
    - **SYN (Synchronize):** Initiates a connection (used in the three-way handshake).
    - **FIN (Finish):** Indicates that the sender has finished sending data (used during connection teardown).

---

## **8. Window Size (16 bits)**

- Specifies the amount of data (in bytes) that the receiver can accept.
- **Purpose:**
    - Enables flow control by preventing the sender from overwhelming the receiver.
    - Example: If the window size is **1024 bytes**, the sender cannot send more than that without acknowledgment.

---

## **9. Checksum (16 bits)**

- Verifies the integrity of the TCP header and data.
- **Mandatory for TCP/IP** to detect transmission errors.

---

## **10. Urgent Pointer (16 bits)**

- Used when the **URG flag** is set.
- Indicates the position of urgent data in the segment.
- **Purpose:** Allows the receiver to process urgent data quickly.

---

## **11. Options (Variable)**

- Provides additional features like:
    - **Maximum Segment Size (MSS):** Specifies the largest segment the sender can handle.
    - **Timestamping:** Used for round-trip time calculations.
- **If the options field is smaller than 32 bits, padding is added to align the header.**