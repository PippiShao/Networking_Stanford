### unit1

## 1.1
The most common communication model used is a bidirectional, reliable stream of bytes.

Applications:
#WWW use HTTP (hypertext transfer protocol)
Client sends command including (GET/PUT/DELETE...)
# BitTorrent
share files
in BitTorrent a client requests documents from other clients in parallel.
torrentfile
swarm collaboration: When a client downloads a complete piece from another client, it then
tells other clients it has that piece so they can download it too.
# Skype
2 clients connect each other.
want to go through NAT (connet to internet easy, while not cannot connect back)
1. client is behing NAT:
-> use rendezvous to open connection
reverse connection
2. clients are behing NAT:
-> use relay to forward

## 1.2
4 later internet model
-a bidirectional, reliable stream of bytes.

Source end-host
Application     : http requests (bitTorrent..) are sent directly from application layer to
                  its peer at the other end – the web server Application.
Transport       : guarantee correct inorder delivery of data
                  most common transport layer servide is TCP.
                  Some application need TCP : video conference... Use UDP
                  controls congestion.
Network         : deliver packets end-to-end across the internet from the source to the destination.
                  link layer is provide a service to network layer. Network layer hands datagram to link layer,
                  tell it to sent over the first link.
                  * network layer is "special" : must use IP (internet protocol)
                  IP:
                  - no promises of delivery
                  - no guarantee of datagram not get lost/corrupt
                  ->So we need transport layer
Link            : carry the data over one link at a time. link layers (ethernet, wifi...)

* Each layer is only communicating with the same layer at the other end.

## 1.3








