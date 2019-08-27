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

Statistical Multiplexing:
Data traffic is bursty. PS allows flows to use all available link capacity, PS allows flows to share link capacity.
A statistical share of the resource based on how much others are using it.

## 1.6

### Principle: layering

Layering: Layering is the name we give to the organization of a system into a number of separate functional
components, or layers.
The layers are hierarchical and they communicate sequentially; i.e. each layer has an interface
only to the layer directly above or below.
Each layer provides a well defined service to the layer above, using the services provided
by the layer(s) below and its own private processing.

As a programmer we communicate with the layer below – the compiler – by handing it our
source code. The compiler is a self-contained functional component that is responsible for
several tasks, such as: lexical analysis, parsing our code, preprocessing declarations,
and then code generation and optimization. The compiler generates object code, which
is then passes to the linker.
The linker links together the compiled object files and libraries. It generates an executable
file.
The CPU (real or virtual) then executes the code.

reasons for layering:
1. modularity
2. well defined service
3. reuse
4. seperation of concerns
5. continuous improvement
6. peer-to-peer communications

## 1.7

### Principle: Encapsulation

The way this works is each protocol layer has some headers, followed
by its payload, followed by some footers.

Your web browser generates an HTTP GET request.
This HTTP GET request is the payload of a TCP segment.
The TCP segment, encapsulating the HTTP GET, is the payload of an IP packet.
This IP packet, encapsulating the TCP segment and the HTTP GET, is the payload of a WiFi frame.

You can actually use encapsulation to recursively layer protocols.
A Virtual Private Network. With a Virtual Private Network, you open a secure connection
to a network you trust, such as your office, for example using Transport Layer Security
(TLS).

* HTTP[ IP[ TCP[ TLS[ IP[ TCP[] ] ] ] ] ]

## 1.8

### Memory Layout and Endianness
A program has an address space, starting at address zero. Most computers today
are 64 bits: this means that memory addresses are 64 bits long, so a computer has up to
2 to the 64 bytes, or 18 sextillion bytes.
In practice, computers today do not have this much memory: they have gigabytes, which is 2 to the 30th.

How you lay out a multibyte value in memory is called endianness, and there are two options.
In little endian, the least significant byte is at the lowest address.
is big endian, the most significant byte is the lowest address.

## 1.9

### IPv4 Addresses

IP version 4 address: unique.
An Internet Protocol, version 4 address is 32 bits long. This 32 bits is often written
as 4 octets, 4 8 bit values, in the form a.b.c.d. Here are three examples. 171.64.64.64, 128.30.76.82,
and 12.22.58.30.

Netmask
In addition to an address, a device typically also has something called a netmask. A netmask
tells the device which IP addresses are local -- on the same link -- and which require going
through an IP router.

A netmask is written as a string of consecutive 1s, starting with the most significant bit.
A netmask of 255.255.255.0, for example, means the first 3 octets are all 1s (2 to the 8th
-1 is 255) and the last octet is zero. This means that an IP address which matches the
first three octets -- 24 bits -- of your IP address is in the same network. A netmask
of 255.255.252.0 means the netmask is 22 bits long, while 255.128.0.0 is a 9 bit netmask.
You tell whether two computers are in the same network by taking a bitwise AND of their
addresses with the netmask. If the resulting addresses are equal, they are in the same
network.

## 1.10

### Longest Prefix Match (LPM Algorithm)

quiz questions

## 1.11

### Address Resolution Protocol (ARP)

It’s how a device gets an answer to the question: “I have an IP
packet whose next hop is this address -- what link address should I send it to?”

48-bit Ethernet addresses are usually written as a colon delimited set of 6 octets written
in hexidecimal, such as 0:13:72:4c:d9:6a as in the source, or 9:9:9:9:9:9 as in the destination.

So instead we often see setups like this, where the gateway or router has multiple interfaces,
each with their own link layer address to identify the card, and also each with their
own network layer address to identify the host within the network that card is part
of.




























