# TCP/IP

[TOC]

## Reference

*TCP/IP Clearly Explained* by <font color="red">Pete Loshin</font>
*TCP/IP Illustrated Volume 1, Second Edition, The Protocols (Chinese version)* by <font color="red">Kevin R. Fall, W. Richard Stevens</font>

## Basic concepts

TCP/IP: transmission control protocol/ internet protocal.

Entity: A thing that does some function.

System: Any entity with observable and reproduceable behaviors.
<font color="grey">A system accepts inputs and produces outputs. But it's like a black box from some point of view, for inside the system may be some other systems.</font>

Network: Some set of systems that share a common communication medium.
<font color="grey">Here, media/medium means the physical thing(s) over or through which the network signals are carried.
Computer network: a network that links computers.
Nowadays, network also refers to computer network, so it's right to say:
Network: a group of two or more computer systems linked together.
Sharing a network only requires that systems share a mechanism by which they can communicate.</font>

Protocol: The complete set of rules governing the interaction between two systems.
<font color="grey">Protocols must specify:
1. How to initiate: How entities initiate a protocol interaction
2. Premitted interactions: What kinds of interactions are permitted
3. Valid requests and responses: Valid requests and responses from entities interacting within the bounds of the proocol
4. Invalid message handling: What to do when any invalid protocol message is received
5. Proper formats: Proper formats for packaging data and protocol messages(requests/replies)
6. Rules about what behaviors and data are acceptable, unacceptable or preferred.
</font>

Internet: A network of networks.

Interface: The point at which two entities make contact.

Node: Any entity connected to a network and capable of both creating and using network data.
<font color="grey">Host and node can be used interchangeably.
Host: Any node that supports users and runs application software.
</font>

Client: A network entity that requests some network service from a server.
Server: A network entity that fulfills requests from clients.

LAN:(Local Area Network) Usually a network that connects nodes across a small distance using direct physical mechanism with minimal use of infrastructure devices to relay data(e.g. routers or switches)
<font color="grey">LAN often refers to the network someone uses to communicate with a system in the same room, floor or building. For example, Ethernet and Wi-Fi.</font>

WAN(Wide Area Network): Usually a network that connects nodes across great distances.

MAN(Metropolitan Area Network): A network that connects nodes across a single metropolitan area.<font color="grey">May span only a few blocks or link nodes across distances measured in km or tens of kilometers.</font>

SAN(Storage Area Network): A network of dedicated storage devices.

AS(autonomous system): A network that can be seen to behave as if it is completely self-contained.

Router: A system that applies intelligence to the movement of network data.
<font color="grey">Intelligence means the knowledge of **current state of the internet** and **the application of rules while processing network data**.
A router usually operates only on network data, the data's destination, without looking further.</font>

Application gateway: A system that translates data from one application into a form that will make it accessible to another application.
<font color="grey">A gateway translates network data into a form that will be usable at its destination.</font>