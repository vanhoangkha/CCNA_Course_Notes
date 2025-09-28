# 11. ROUTING FUNDAMENTALS : PART 1




### WHAT IS ROUTING ?



ROUTING is the process that routers use to determine the path that IP packets should take over a network to reach their destination.

- ROUTERS store routes to all their known destinations in a ROUTING TABLE
- When ROUTERS receive PACKETS, they look in the ROUTING TABLE to find the best route to forward that packet.

There are two main routing methods (methods that routers use to learn routes):

- DYNAMIC ROUTING : ROUTERS use Dynamic Routing Protocols (ie: OSPF) to share routing information with each other automatically and build their routing tables.
- STATIC ROUTING : A network engineer / Admin manually configures routes on the router.

A ROUTE tells the ROUTER :

- to send a packet to Destination X, you should send the pack to ***next-hop*** Y
- or if the Destination is directly connected to the router, *send the packet directly to the destination.*
- or if the Destination is the router’s own IP address, *receive the packet for yourself (don’t forward it).*

📊 **[Diagram]** - *Network diagram illustrating the concept*


WAN (Wide Area Network) = network that extends over a large geographic area.

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*
