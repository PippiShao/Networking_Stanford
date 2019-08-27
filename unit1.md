# unit1

## 1.1
The most common communication model used is a bidirectional, reliable stream of bytes.

Applications:
### WWW use HTTP (hypertext transfer protocol)
Client sends command including (GET/PUT/DELETE...)
### BitTorrent
share files
in BitTorrent a client requests documents from other clients in parallel.
torrentfile
swarm collaboration: When a client downloads a complete piece from another client, it then
tells other clients it has that piece so they can download it too.
### Skype
2 clients connect each other.
want to go through NAT (connet to internet easy, while not cannot connect back)
1. client is behing NAT:
 use rendezvous to open connection
reverse connection
2. clients are behing NAT:
 use relay to forward

## 1.2
4 later internet model
A bidirectional, reliable stream of bytes.

* Application     : http requests (bitTorrent..) are sent directly from application layer to
                  its peer at the other end – the web server Application.
* Transport       : guarantee correct inorder delivery of data
                  most common transport layer servide is TCP.
                  Some application need TCP : video conference... Use UDP
                  controls congestion.
* Network         : deliver packets end-to-end across the internet from the source to the destination.
                  link layer is provide a service to network layer. Network layer hands datagram to link layer,
                  tell it to sent over the first link.
                  * network layer is "special" : must use IP (internet protocol)
                  IP:
                  - no promises of delivery
                  - no guarantee of datagram not get lost/corrupt
                  - So we need transport layer
* Link            : carry the data over one link at a time. link layers (ethernet, wifi...)

* Each layer is only communicating with the same layer at the other end.

## 1.3

### Service provided by IP

IP's job: deliver datagram to the other end.
IP servide model:
datagram        : individually routed packet. hop by hop routing.
unreliable      : packets might be dropped.
best effort     : drop only if necessary.
connectionless  : no per flow state, packets might be mis-sequenced.

IP service model:
1. tries to prevent packets looping forever between routers. By adding adding a step check initialized to 128.
when reduced to 0, it thinks that the datagram got stuck in loop.
2. fragment packets if they are too long.
3. uses a header checksum to reduce chances of delivering to wrong destination.
4. allow for new version of IP (ipv4 - 32 bit addresses, ipv6 - 128 bit)
5. allow for new options to be added.

## 1.4

### A Day in the Life of a Packet

TCP: three way handshake “SYN, SYN-ACK, ACK”.
    1. sync
    2. acknowledge the sync
    3. acknowledge

To open TCP stream to another program, we need 2 addresses:
    1. IP address. The address the network layer uses to deliver packets to the computer
    2. TCP port. Tells the computer's software which application to deliver data to.

IP packets between clients and server take hops though routers.
Router use forwarding table to decide which of its links to sent it out on or to deliver to its own software.

## 1.5

### Packet Switching Principle

Packet Switching

Packet: a self-contained unit of data that carries info necesary for it to reach its destination.
Packet Switching: independently for each arriving packet, pick its outgoing link. If the link is free, send it. else hold the packet for later.
Optimization for packet switching: a switch can have a table of destination addresses and the next hop. When it receives a packet,
it looks up the address in the table, and sends the packet to the appropriate next hop.
Flow: A collection of datagrams belonging to the same end-to-end communication

Packet Switching benefits:
1. simple packet forwarding.
2. efficient sharing of links.















