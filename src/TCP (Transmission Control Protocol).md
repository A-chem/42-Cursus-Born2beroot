TCP (Transmission Control Protocol) is like a set of rules that computers use to talk to each other over a network, like the internet. It makes sure that data (e.g., a file, a web page, or a message) gets from one computer to another without missing pieces and in the correct order.

## Features of TCP protocol

- **Transport Layer Protocol**

TCP is a transport layer protocol as it is used in transmitting the data from the sender to the receiver.

- **Reliable**

TCP is a reliable protocol as it follows the flow and error control mechanism. It also supports the acknowledgment mechanism, which checks the state and sound arrival of the data. In the acknowledgment mechanism, the receiver sends either positive or negative acknowledgment to the sender so that the sender can get to know whether the data packet has been received or needs to resend.

- **Order of the data is maintained**

This protocol ensures that the data reaches the intended receiver in the same order in which it is sent. It orders and numbers each segment so that the TCP layer on the destination side can reassemble them based on their ordering.

- **Connection-oriented**

It is a connection-oriented service that means the data exchange occurs only after the connection establishment. When the data transfer is completed, then the connection will get terminated.

- **Full duplex**

It is a full-duplex means that the data can transfer in both directions at the same time.

- **Error Detection and Correction**

TCP includes a **checksum** to detect errors in the data during transmission. If the receiver detects a corrupted packet (i.e., incorrect checksum), it discards it and requests a retransmission.

## The structure of the TCP

A TCP segment consists of two parts:

1. [[TCP Header]]: Contains control information for managing the connection and data transfer.
2. **TCP Data (Payload)**: The actual data being transmitted

## How exactly do TCP connections work?

### 1. **Connection Establishment (Three-Way Handshake)**

1. **Step 1: SYN (Synchronize)**
    
    - The client (sender) sends a **SYN** packet to the server (receiver).
    - This packet contains:
        - A random **initial sequence number (ISN)** chosen by the client.
        - The **SYN flag** set to 1, indicating the start of a connection.
    - Purpose: The client is saying, _"I want to start a connection and here's my initial sequence number."_
    
    **Example:**  
    Client → Server: "SYN, my sequence number is 100."
    

---

2. **Step 2: SYN-ACK (Synchronize-Acknowledge)**
    
    - The server responds with a **SYN-ACK** packet.
    - This packet contains:
        - Its own **random sequence number (server's ISN)**.
        - An **ACK** (acknowledgment) number, which is the client’s ISN + 1.
        - The **SYN** flag set to 1, indicating the server also wants to establish a connection.
        - The **ACK** flag set to 1, acknowledging the client's request.
    
    Purpose: The server is saying, _"I received your SYN. Here's my sequence number, and I’m acknowledging your sequence number."_
    
    **Example:**  
    Server → Client: "SYN-ACK, my sequence number is 300, and I acknowledge your number 101."
    

---

3. **Step 3: ACK (Acknowledge)**
    
    - The client sends back an **ACK** packet.
    - This packet contains:
        - An acknowledgment number, which is the server's ISN + 1.
        - The **ACK flag** set to 1, confirming receipt of the server's sequence number.
        - No new sequence number is sent in this step because the connection setup is complete.
    
    Purpose: The client is saying, _"I received your SYN-ACK, and I’m ready to start sending data."_
    
    **Example:**  
    Client → Server: "ACK, I acknowledge your number 301."
    
[[image(10).svg]]
### 2. **Data Transmission**

#### **1. Sending Data:**

- The **sender** breaks the data into smaller segments, each containing:
    - **TCP Header** with crucial information (e.g., sequence number, acknowledgment number).
    - **Payload** (actual data being transmitted).
- The segments are transmitted to the receiver. TCP ensures the segments are sent in sequence and handles retransmissions in case of lost data.

#### **2. Receiving Data:**

- The **receiver** gets each segment, checks for errors using the **checksum** field, and sends an **ACK** back to the sender.
- The receiver uses the sequence number to reorder the segments if they arrive out of order.
- The receiver also indicates how much data it can handle by adjusting the **window size** in its acknowledgment.

#### **3. Acknowledging Data:**

- The **ACK** contains the sequence number of the next expected byte. For example, if the receiver successfully received data up to byte 1000, it would send an acknowledgment number of **1001**.
- If the sender doesn't receive an ACK within a certain time (due to packet loss or network issues), it will **retransmit** the segment.

#### **4. #### **Flow and Congestion Control**

- **Flow Control:** The sender adjusts its transmission rate to avoid overwhelming the receiver. The receiver indicates how much data it can accept at a given time using the sliding window mechanism.
- **Congestion Control:** TCP adjusts its data transmission rate according to the network state. If congestion is detected (e.g., packet loss), TCP reduces its transmission rate.
## 3. Connection Termination in TCP (Four-Way Handshake)

- **Step 1: FIN (Finish) - Sender Initiates Termination**
    
    - The sender (client or server) that wants to close the connection sends a **TCP segment** with the **FIN** (Finish) flag set.
    - The FIN flag indicates that the sender has no more data to send, but it is still willing to receive data.
    - **Purpose:** It signals that the sender is done sending data but can still receive acknowledgment or possibly more data from the receiver.
    
    **Example:**
    
    - **Sender (Client):** Sends a TCP segment with **FIN** set, asking the receiver (server) to terminate the connection.
- **Step 2: ACK (Acknowledgment) - Receiver Acknowledges FIN**
    
    - The receiver responds with a **TCP segment** that has the **ACK** flag set.
    - The **Acknowledgment Number** will be set to the sequence number of the FIN segment + 1, indicating the receipt of the FIN request.
    - The connection is now half-closed, meaning the sender is finished sending, but the receiver can still send data back.
    
    **Example:**
    
    - **Receiver (Server):** Sends an **ACK** to acknowledge the receipt of the FIN segment from the sender.
- **Step 3: FIN (Finish) - Receiver Initiates Termination**
    
    - After acknowledging the sender’s FIN, the receiver sends its own **FIN** segment to the sender.
    - This signals to the sender that the receiver has also finished sending its data and is ready to close the connection.
    
    **Example:**
    
    - **Receiver (Server):** Sends a **FIN** to the sender, indicating it has finished transmitting data.
- **Step 4: ACK (Acknowledgment) - Sender Acknowledges Receiver’s FIN**
    
    - The sender, upon receiving the FIN segment from the receiver, sends back an **ACK** segment.
    - This **final ACK** confirms the receipt of the receiver’s FIN segment, and the connection is now fully closed.
    - No more data will be transmitted from either side, and both ends of the connection are now closed.
    
    **Example:**
    
    - **Sender (Client):** Sends a final **ACK** to acknowledge the receiver’s FIN segment. After this, the connection is fully terminated.