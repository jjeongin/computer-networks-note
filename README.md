# Computer Networks Notes
* [Chapter 1. Overview: Comp Networks and the Internet](#ch-1-comp-networks-and-the-internet)
* [Chapter 2. Application Layer](#ch-2-application-layer)
* [Chapter 3. Transport Layer](#ch-3-transport-layer)
* [Chapter 4. Network Layer - Data Plane](#ch-4-network-layer-data-plane)
* [Chapter 5. Network Layer - Control Plane](#ch-5-network-layer-control-plane)
* [Chapter 6. Link Layer & LANs](#ch-6-link-layer)

## Ch 1. Comp Networks and the Internet
### 1.5 Protocol Layers and Their Service Models
* OSI Model vs TCP/IP Model (Protocol Stack)

| OSI Model | TCP/IP Model |
| ------------- | ------------- |
| Application  | Application  |
| Presentation  | |
| Session  | |
| Transport | Transport |
| Network  | Network  |
| Link | Link |
| Physical | Physical |

<img width="798" alt="Screen Shot 2023-02-03 at 4 38 35 PM" src="https://user-images.githubusercontent.com/68997923/216605651-37724708-9349-4b2d-817d-3d9e97e8eee3.png">

* Application Layer: where network applications and their applicaiton-layer protocols reside
  * Messages (= packets a.k.a. Protocol Data Unit in application layer)
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
 * Web uses client-host architecture.
 * 

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
* Hypertext Transfer Protocol (HTTP)
  * Web page consists of objects (= files) e.g. HTML, CSS, Javascript files addressable by a single URL.
  * Web Browser = Client since client-side HTTP is implemented in browser.
  * User requests a web page -> browser sends HTTP request message to the server -> server receives the message and responds with HTTP response message (which contains the objects)
  * Stateless Protocol: The server doesn't store any state information about the client and merely sends the object that they asked for. 
  * HTTP/1.0 Non-persistent connection: Sends each request/response pair over a seperate TCP connection. TCP connection is closed after the server sends the object. 
    * RTT (Round-trip time): Time it takes for a small packet to travel from client, server, then back to client
    * How HTTP uses TCP: "three-way handshake" The client sends a small TCP segment to the server, and the server also responds with a small TCP to check the connection. (1 RTT) => Total 2 RTT + transmission time 
  * Persistent connection: Sends all request/response pairs over the same TCP connection. The server leaves the connection open for further requests and makes it expire after certain time period.
    * HTTP/1.1 uses persistent connection + pipelining to avoid time delay. Pipelining is allowing requests to be back-to-back w/o waiting for replies to pending requests.
  * HTTP Message Request Format
    * <img width="327" alt="Screen Shot 2023-02-02 at 2 15 51 AM" src="https://user-images.githubusercontent.com/68997923/216175955-909dc752-d1ab-4b95-8434-e4adad3ae989.png">
  
  * HTTP Message Response Format
    * 

  * Cookies: Allows sites to keep track of users. Used to create a user session layer on top of stateless HTTP.
    * 4 components: (1) cookie header in request message, (2) cookie header in response message, (3) cookie file kept on the user's end system (managed by the user's browser), (4) a back-end database at the server
    * <img width="584" alt="Screen Shot 2023-02-02 at 10 30 19 PM" src="https://user-images.githubusercontent.com/68997923/216416699-35998e1d-6739-488b-9e4e-292610366e2e.png">
    * Web server can access all the pages the user visited at the specific site in the past by cookie, thereby allowing one-click shopping w/o entering their info again at their subsequent visit.
  * Web Cache (= Proxy Server): A network entity that satisfies HTTP requests on the behalf of an origin Web server. Has its own disk storage and keeps copies of recently requested objects.
    * <img width="541" alt="Screen Shot 2023-02-02 at 10 35 27 PM" src="https://user-images.githubusercontent.com/68997923/216418605-f49b292a-5fcf-44c1-b612-2a8b87087828.png">
    * Cache is both a server and a client at the same time.
    * Advantages: (1) Reduce the response time for a client request (esp. if the bandwith between client-server is much less than client-cache), (2) Reduce traffic on an institution's access link to the Internet (Reduce costs)
    * A problem of caching: The copy of an object residing in the cache may be out-of-date (the original object may be modified after the copy was cached). => Conditional GET
    * Conditional GET: A type of HTTP request message. A request message is conditional GET message if it uses GET method and the request message includes an 'If-Modified-Since:' header line.
      * Process:
        * Caching
          * Client -> Proxy Server: HTTP GET request
          * Proxy Server -> Server: HTTP GET request
          * Proxy Server <- Server: HTTP GET response with the object
          * Client <- Proxy Server: HTTP GET response with the object, Proxy Server caches the object locally with the last-modified date.
        * Conditional GET
          * Client -> Proxy Server: HTTP GET request
          * Proxy Server -> Server: HTTP Conditional GET request with a 'If-modified-since: DATE-TIME' header line. This is the same date & time with the last-modified date.
          * Proxy Server <- Server: If the object has not been modified, response with HTTP/1.1 304 Not Modified response line.
          * Client <- Proxy Server: HTTP GET response with the existing cached object 
    * CDNs (Content Distribution Networks): A CDN company installs many geographically distributed caches throughout the Internet, thereby localizing much of the traffic.
      * Shared CDN (e.g. Akamai, Limelight) vs Dedicated CDN (e.g. Google, Netflix)
  * HTTP/2: Reduce latency by enabling request and response _multiplexing_ over a single TCP connection. 
    * HOL (Head of Line) Blocking problem:  
    * HTTP/2 Framing: 
    * 

### 2.3 SMTP (E-mail in the Internet)

### 2.4 DNS
* Directory system that translates hostnames to IP addresses. 
* (1) A distributed database implemented in a hierarchy of DNS servers, (2) An application-layer protocol that allows hosts to query the distributed database.
* DNS protocol runs over UDP and uses port 53. 
* 

### 2.5 FTP (Peer-to-peer File Distribution)

## Ch 3. Transport Layer
### 3.2 Multiplexing and Demultiplexing

### 3.3 UDP

### 3.5 TCP

### 3.6 & 7 Congestion Control

## Ch 4. Network Layer: Data Plane
## 4.1 Overview
* Routing & Forwarding
  * Routing with routing table
### 4.2 Router
* Switching
* Packet Scheduling

### 4.3 IP (Internet Protocol)
* IPv4 Datagram Format
<img width="483" alt="Screen Shot 2023-02-03 at 11 08 43 PM" src="https://user-images.githubusercontent.com/68997923/216686824-e3f06c1d-361f-4d9f-b2fa-bdcd2d397ca3.png">
* IP Address: Each byte of the address is written in its decimal form and seperated by a dot from other bytes.
* Subnet: A network interconnecting multiple host interfaces and a router interface. A subnet is assigned a chucnk of IP addresses with the same prefix, e.g. 223.1.1.0/24, where /24 is a subnet mask which indicates the leftmost 24 bits of the 32-bit quantity define the subnet address.
* IP Broadcast Address: 255.255.255.255. When a host sends a datagram to the broadcast address, the message will be delivered to all hosts on the same subnet.
* Obtaining a block of addresses for subnet -> contact ISP. Assigning this block of addresses to individual hosts -> DHCP.
* NAT (Network Address Translation)
  * Private network: A network whose addresses only have meaning to devices within that network.

## Ch 5. Network Layer: Control Plane
### 5.3 OSPF

### 5.4 BGP

### 5.5 SDN

### 5.6 ICMP

## Ch 6. Link Layer
* ARP vs PARP

* VLANs

* DHCP

## Ch 8. Security
### 8.6 TLS

### 8.7 IPsec

### 8.9 Firewalls
* Firewall decides the fate of packets going in and out of the system.
## Notes by Concepts
* Iptable: A standard firewall included in most Linux distributions by default. A command-line interface to talk to the kernel (kernel-level netfilter hooks) and decides the packets to filter. It is used to set up, maintain, and inspect the tables of IP packet filter rules in the Linux kernel.
  * A type of a routing table?
  * _Tables_: A set of chains
  * _Chain_: A collection of rules
  * _Rule_ : A condition used to match packet
  * _Target_: An action taken when a possible rule matches. e.g. ACCEPT, DROP, QUEUE
  * _Policy_: The default action taken in case of no match with the inbuilt chains. e.g. ACCEPT or DROP
  * Iptable Main Files
    * /etc/init.d/iptables – init script to start|stop|restart and save rulesets
    * /etc/sysconfig/iptables – where rulesets are saved. Iptable rules reset everytime the system reboots so we want to save the rulesets in this file so that it restores
    * /sbin/iptables – binary
  * Iptable Packet Chain
    * INPUT: Default chain originating to system.
    * OUTPUT: Default chain generating from system.
    * FORWARD: Default chain packets are send through another interface.
    * RH-Firewall-1-INPUT: User-defined
  * Iptable Actions
    * ACCEPT: accepts the packet.
    * DROP: drops the packet. To anyone trying to connect to your system, it would appear like the system didn’t even exist.
    * REJECT: “rejects” the packet. If TCP, it sends a “connection reset” packet. If UDP or ICMP, it sends a “destination host unreachable” packet.
    * QUEUE: passes the packet to userspace.
    * RETURN: stops traversing this chain and resumes at the next rule in the previous (calling) chain.
    * 
* traceroute: gives us the complete network devices list in between with their IP addresses

## Linux Commands
* ping: sends an echo to a hostname or an IP addess
* chmod: changes the access permissions and the special mode flags of file system object. 
* cat: lists, combines, and writes file content to the standard output
* touch: create an empty file or generate and modify a timestamp in the Linux command line
* traceroute: finds hop to rreach to perticular host
* ifconfig: 

