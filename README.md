# Computer Networks Notes
* [Chapter 1. Overview: Comp Networks and the Internet](#ch-1-comp-networks-and-the-internet)
* [Chapter 2. Application Layer](#ch-2-application-layer)
* [Chapter 3. Transport Layer](#ch-3-transport-layer)
* [Chapter 4. Network Layer - Data Plane](#ch-4-network-layer-data-plane)
* [Chapter 5. Network Layer - Control Plane](#ch-5-network-layer-control-plane)
* [Chapter 6. Link Layer & LANs](#ch-6-link-layer)

## Ch 1. Comp Networks and the Internet
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
* Client-host Architecture: 

* Peer-to-peer Architecture (P2P): 

* Client and Server Processes
 * Process: A program running within an end system. communicates by exchaning messages. 
 * Client Process: A process that initiates the communication e.g. A browser in client-host, peer that is downloading the file in P2P.
 * Server Process: A process that waits to be contacted to begin the session e.g. A web server in client-host, a peer that is uploading the file in P2P.
 * Process sends and receives messages through a software interface called socket.
 * Socket: interface (= API) between the application layer and transport layer. Programming interface with which network applications are built.
 * The application developer only has control for the application-layer side of the socket and had little control of the transport-layer side of the socket e.g. 1) choise of transport protocol, 2) maybe maximum buffer or segment sizes.

* TCP
 * Handshaking: The client and server exchange transport-layer control information with each other _before_ the application-level messages begin to flow. After handshaking, a TCP connection is said to exist between the sockets of the two processes.
 * Reliable data transfer service: The processes can rely on TCP to deliver all data w/o errer in proper order.
 * Congestion-control mechanism: throttles a sending process (client or server) when the network is congested between sender and receiver. attempts to limit each TCP connection to its fair share of network bandwidth.
 * TLS: An enhanced TCP. Provides extra security services on top of TCP e.g. encryption, data integrity, end-point authentication. (Neither TCP and UDP provide encryption by default.) Needs to be included as a code in application-layer level in both client and server sides of the application if one wants to use. 
* UDP
 * No-frills, lightweight, providing minimal services. Connectionless (No handshaking), unreliable data transfer service (no guarantee that the message will be delivered and will be delivered in order). No congestion-control mechanism.
 * Only Internet telephony (e.g. Skype) uses UDP to circumvent TCP's congestion control mechanism but uses TCP as a fallback since UDP is configured to be blocked in many firewalls. 
<img width="623" alt="Screen Shot 2023-02-01 at 10 11 54 PM" src="https://user-images.githubusercontent.com/68997923/216127466-45e62b93-76f8-46cc-b18f-b9d575fdf1b2.png">

### 2.2 HTTP (Web and HTTP)

### 2.3 SMTP (E-mail in the Internet)

### 2.4 DNS

### 2.5 FTP (Peer-to-peer File Distribution)

## Ch 3. Transport Layer

## Ch 4. Network Layer: Data Plane

## Ch 5. Network Layer: Control Plane

## Ch 6. Link Layer

