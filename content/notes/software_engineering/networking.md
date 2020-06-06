---
title: Networking
menu: 
    ai_notes:
        parent: Software Engineering
draft: False
---
### Terms

* **Connection**: Built before data transfer (following protocol) and deconstructed after.
* **Packet**: The envelopes that carry your data (in pieces) from one point to the next. Includes 
header that includes source and destination, timestamps, network hops, plus the main portion which
is the data being transfered (also called body, or payload). 
* **Network Interface**: Software interface to your networking hardware. 
* **Local Area Network (LAN)**: A network or portion of network not publically accessible 
to the greater internet. 
* **Wide Area Network (WAN)** More extensive than a LAN (typically means internet as a whole). 
* **Port**: Address on a single machine that can be tied to a specific piece of software.
* **Firewall**: Should traffic coming in or going out be allowed. Decides which type of traffic
is acceptable on which ports. 
* **Network Address Translation (NAT)**: Translates incoming requests to a routing server
to the devices/servers it knows about in the LAN.
* **Virtual Private Network (VPN)**: Connecting multiple LANs through the internet, while
maintaining privacy (as if they were on a local network).
* **Network Address Translation**: Allows addresses to be rewritten when packets 
travel over network borders, which allows the same IP address to be used on multiple networks.
* **IPv4**: Each byte (8-bit segment seperated by a period) is expressed a number 0-255.
Each segment is an octet of bits, so **192.168.0.5** is **1100-0000.1010-1000.0000-0000.0000-0101**.
* **IPv6**: Written as a segment of four hexadecimal digits.
* **Subnetting**: Dividing a network into smaller network sections.
* **Netmask**: Specifies the amount of address bits used for the network portion of the IP. Every
bit that is relevant for the network portion is assigned a value of 1 in the mask. A bitwise
AND yields the networking portion and discards the host portion.
* **Classless Inter-Domain Routing (CIDR) Notation**: Prefixing the number of bits relevant
to the network routing. Allows for more nuanced subnet slicing.

### Protocols
* **Media Access Control (MAC)**
* **Transmission Control Protocol (TCP)**: Implemented in the transport layer of the
IP/TCP model, and is used to establish reliable connections. TCP encapsulates data 
into packets, then transfers them to the destination on the connection. Once there,
it can check for errors, request parts of the data to be resent, and assemble the 
information to be send to the application layer. The connection requires a three-way
handshake to ensure data reliability. Once transmission is completed, the connection 
is torn down using a four-way handshake. This is the protocol used by WWW, FTP, SSH,
and email.
* **User Datagram Protocol (UDP)**: Like TCP, but offers unreliable data transfer (does
not verify that data has been received on the other end of the connection). Because
it doesn't wait for confirmation, it is faster than TCP. It doesn't establish a connection,
it just sends.
* **Domain Name System (DNS)**: What ties a domain name to an IP address.
* **IP**: IP addresses are unique on each network and allow machines to address each
other across a network. Implemented on the internet layer of the IP/TCP model. Most
common implementation is IPv4 or IPv6. 
* **Internet Control Message Protocol (ICMP)**: Used to send messages between devices
to indivate availability or error conditions. "Are you awake? Can I talk to you?" 
ICMP packets are used for things like ping or traceroute, and are usually transmitted 
when another kind of packet meets some kind of problem.
* **Hypertext Transfer Protocol (HTTP)**
* **Secure Shell (SSH)**: Used to communicate with a remote server in a secure way
(end-to-end encryption). Client sends the host the publick key it would like to use. 
The host checks the authorized keys on file, and if it finds the public key it generates
a random string and encrypts it using the public key. The host sends the encrypted message 
to the client, who decrypts it using the private key. This decrypted message is sent back to the host,
along with session ID (established with the host), as an MD5 hash. At this point the host can verify.
[More info](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys).
* **TLS/SSL**:
* **File Transfer Protocol (FTP)**: Inherently insecure, so not recommended for externally
facing networks.

### Network Layers

#### Open Systems Interconnect (OSI) Model

This model has **seven** layers:

* *Application*: Users interaction. Considerations include availability of resources,
partners to communicate with, and data synchronization.
* *Presentation*: Mapping resources and creating context. Translates lower level networking 
data into app-ready data.
* *Session*: Creates, maintains, and destroys connections between nodes.
* *Transport*: Providing reliable connection to the above layers. Can resend dropped data.
Can acknowledge data receive to remote computers.
* *Network*: Route data between nondes on the network, using addresses. 
* *Data Link*: Establish and maintain reliable links between nodes on a network.
* *Physical*: The software that manages physical connections and hardware.

### TCP/IP model

This model has **four** layers:

* *Application*: Creating and transmitting user data between applications. 
* *Transport*: Commnication between processes. Ports address different services.
* *Internet*: Transport data from node to node in a network. IP addresses are defined
in this layer. 
* *Link*: Implements the topology of the local network. Creates connections between 
neighboring nodes to send data.
