# Computer Networks Notes
## Ch 1
### 1.5 Protocol Layers and Their Service Models
* OSI Model (= Protocol Stack)

| OSI Model |
| ------------- |
| Application  |
| Transport  |
| Network  |
| Link  |
| Physical  |

* Application Layer: where network applications and their applicaiton-layer protocols reside
  * Messages (= packes of information)
  * Distributed over multiple end systems, with the app in one end system using the protocol to exchange a message with the app in another end system.
  * Protocols:
    * HTTP: Web document request & transfer
    * SMTP: E-mail transfer
    * FTP: File transfer
    * DNS (doman name system): Translation of human-friendly names e.g. www.google.com to a 32-bit network addess (IP address)
* Transport Layer
  * Segment (= packets in transport layer)
  * Transport layer protocols transport application-layer messages.
  * Protocols:
    * TCP: Connection-oriented service, e.g. guaranteed delivery of app-layer messages to the destination, flow control (sender/receiver speed matching). Breaks long messages into shorter segments. Provides a congestion-control mechanism. 
    * UDP: Connectionless service, no-frills, no reliability, no flow control, no congestion control.
* Network Layer
  * Datagrams (= packets in network layer)
  * Move network-layer pakcets from one host to another. Transport-layer passes segments + destination address to the network layer and network layer delivers it.
  * Protocols:
    * IP
    * Routing protocols: to determine which route datagrams should take from sources to destinations
* Link Layer: 
    * Frames (= packets in link layer)
    * Delivers the datagram to the next node along the route (determined in network layer)
    * Protocols:
      * Ethernet
      * WiFi
      * Cable access networks's DOCSIS 
* Physical Layer: 
    * While link layer moves an entire frame to the next node, physical layer moves an individual bit within the frame to the next node.
    * Protocols depend on the link layer and the actual transmission medium of the link. e.g. Ethernet has protocols like: twisted-pair copper wire, coaxial cable, fiber optics, etc.
    
* Encapsulation
## Ch 2. Application Layer
### 2.1 Principles of Network Applications

### 2.2 HTTP (Web and HTTP)

### 2.3 SMTP (E-mail in the Internet)

### 2.4 DNS

### 2.5 FTP (Peer-to-peer File Distribution)

## Ch 3. Transport Layer

## Ch 4. Network Layer: Data Plane

## Ch 5. Network Layer: Control Plane

## Ch 6. Link Layer (& LANs)

