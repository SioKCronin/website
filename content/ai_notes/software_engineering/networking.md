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

### Protocols
* **Media Access Control (MAC)**
* **TCP**:
* **UDP**: 
* **DNS**:
* **IP**:
* **ICMP**:
* **HTTP**:
* **SSH**: [Useful guide](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)
* **TLS/SSL**:
* **FTP**: 

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




