# 23. ETHERCHANNEL

WHAT IS ETHERCHANNEL?

ETHERCHANNEL allows you to GROUP multiple physical INTERFACES into a group which operates as a SINGLE LOGICAL INTERFACE - so they BEHAVE as if they are a single INTERFACE

A LAYER 2 ETHERCHANNEL is a group of SWITCH PORTS which operate as a SINGLE INTERFACE

A LAYER 3 ETHERCHANNEL is a group of ROUTED PORTS which operate as a SINGLE INTERFACE which you assign an IP ADDRESS to.

📊 **[Diagram]** - *Network diagram illustrating the concept*

When the bandwidth of the INTERFACES connected to END HOSTS is greater than the bandwidth of the connection to the DISTRIBUTION SWITCH(es), this is called **OVERSUBSCRIPTION.** 

Some OVERSUBSCRIPTION is acceptable, but too much will cause congestion.

📊 **[Diagram]** - *Network diagram illustrating the concept*

- If you connect TWO SWITCHES together with multiple links, ALL except ONE will be DISABLED by SPANNING TREE PROTOCOL (Green Lights vs. Orange Lights above on ASW1)

WHY?

- If ALL of ASW1s INTERFACES were FORWARDING, LAYER 2 LOOPS would form between ASW1 and DSW1, leading to a BROADCAST STORM (Bad!)
- Other links will be unused unless the active link fails. In that case, one of the inactive link will start forwarding.

An ETHERCHANNEL (in network topology diagrams) is represented like THIS (circle around multi-connections)

📊 **[Diagram]** - *Network diagram illustrating the concept*

- ETHERCHANNEL groups multiple channels together to act as a SINGLE INTERFACE
- STP will treat this GROUP as a SINGLE INTERFACE

📊 **[Diagram]** - *Network diagram illustrating the concept*

(All INTERFACES Green!)

TRAFFIC using ETHERCHANNEL will be load-balanced among the physical INTERFACES in the group.

An algorithm is used to determine WHICH TRAFFIC will use WHICH physical INTERFACE (more details later)

Some other names for an ETHERCHANNEL are:

- PORT CHANNEL
- LAG (Link Aggregation Group)

---

HOW DOES AN ETHERCHANNEL LOAD-BALANCE?

📊 **[Diagram]** - *Network diagram illustrating the concept*

- ETHERCHANNEL load-balances based on **“flows”**
- A “flow” is a communication between TWO NODES in the NETWORK
- FRAMES in the same “flow” will be FORWARDED using the SAME physical INTERFACE
- If FRAMES in the same “flow” were FORWARDED using different physical INTERFACES, some FRAMES may arrive at the DESTINATION out of order/sequence, which can cause problems.
- You can CHANGE the INPUTS used in the INTERFACE SELECTION calculation (for “flows”)
    - INPUTS that can be used:
        - SOURCE MAC ADDRESS
        - DESTINATION MAC ADDRESS
        - SOURCE and DESTINATION MAC ADDRESS
        - SOURCE IP ADDRESS
        - DESTINATION IP ADDRESS
        - SOURCE and DESTINATION IP ADDRESS

How to see the configuration for LOAD-BALANCING method

📊 **[Diagram]** - *Network diagram illustrating the concept*

How to CHANGE the LOAD-BALANCING method

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

HOW TO CONFIGURE LAYER 2 / LAYER 3 ETHERCHANNELS

There are THREE methods of ETHERCHANNEL configuration on Cisco SWITCHES

**PAgP (Port Aggregation Protocol)**

- Cisco proprietary protocol
- Dynamically negotiates the creation/maintenance of the ETHERCHANNEL (like DTP does for trunks)

💡 **LACP (Link Aggregation Control Protocol)**
- Industry standard protocol (IEEE 802.3ad)
- Dynamically negotiates the creation/maintenance of the ETHERCHANNEL (like DTP does for trunks)


**Static EtherChannel**

- A protocol isn’t used to determine if an EtherChannel should be formed
- Interfaces are statically configured to form an EtherChannel

Up to 8 INTERFACES can be formed into a single ETHERCHANNEL (LACP allows up to 16 but only 8 will be ACTIVE, the other 8 will in STANDBY mode, waiting for an active INTERFACE to fail)

 
---

PAgP CONFIGURATION

📊 **[Diagram]** - *Network diagram illustrating the concept*

💡 NOTE that “auto” and “desirable” are the ONLY available modes for PAgP

📊 **[Diagram]** - *Network diagram illustrating the concept*

PAgP negotiations to form an ETHERCHANNEL


💡 AWS1(config-if-range)# channel-group 1 mode desirable.
Creating a port-channel interface Port-channel1

Shows up in the interface as “Port-channel1”

📊 **[Diagram]** - *Network diagram illustrating the concept*

The “channel-group” number has to MATCH for member INTERFACES on the same SWITCH.

It DOESN’T have to MATCH the “channel-group” number on the OTHER SWITCH!

💡 (channel-group 1 on AWS1 can form an ETHERCHANNEL with channel-group 2 on DSW1)

---

LACP CONFIGURATION

📊 **[Diagram]** - *Network diagram illustrating the concept*

💡 NOTE that “active” and “passive” are the ONLY available modes for LACP

📊 **[Diagram]** - *Network diagram illustrating the concept*

LACP negotiations for form an ETHERCHANNEL

The “channel-group” number has to MATCH for member INTERFACES on the same SWITCH.

It DOESN’T have to MATCH the “channel-group” number on the OTHER SWITCH!

💡 (channel-group 1 on AWS1 can form an ETHERCHANNEL with channel-group 2 on DSW1)

---

STATIC ETHERCHANNEL CONFIGURATION

📊 **[Diagram]** - *Network diagram illustrating the concept*

💡 NOTE that “on” is the ONLY available mode for STATIC ETHERCHANNEL

ON mode only works with ON Mode

ON + desirable = DOES NOT WORK)

ON + active = DOES NOT WORK

---

HOW TO MANUALLY CONFIGURE THE NEGOTIATION PROTOCOL

📊 **[Diagram]** - *Network diagram illustrating the concept*

TWO OPTIONS: 

- LACP Protocol
- PAgP Protocol

(Above shows a protocol mismatch error because LACP does not support “desirable” - only PAgP does)

(“channel-group 1 mode active” works because LACP supports “active”)

---

AFTER CONFIGURING THE ETHERCHANNEL MODE

CONFIGURING THE PORT INTERFACE

📊 **[Diagram]** - *Network diagram illustrating the concept*

“show running-config” shows “interface Port-channel1” in the configuration

📊 **[Diagram]** - *Network diagram illustrating the concept*

💡 NOTE the PHYSICAL INTERFACES (g0/0-g0/3) were auto-configured by the Port-channel1 configuration!

---

IMPORTANT NOTES ABOUT ETHERCHANNEL CONFIGURATION

- Member INTERFACES must have matching CONFIGURATIONS
    - Same DUPLEX (Full / Half)
    - Same SPEED
    - Same SWITCHPORT mode (Access / Trunk)
    - Same allowed VLANs / Native VLAN (for TRUNK interfaces)

- If an INTERFACE’s configurations do NOT MATCH the others, it will be EXCLUDED from the ETHERCHANNEL

---

VERIFYING STATUS OF ETHERCHANNEL

💡 “show etherchannel summary”

📊 **[Diagram]** - *Network diagram illustrating the concept*

NOTE information at bottom. (”SU” means S - Layer2 + U - in use)

Protocol = What protocol the Etherchannel is using (in this case, LACP)

“Ports” = the list of interfaces in the EtherChannel (P = bundled in port-channel)

OTHER FLAGS

📊 **[Diagram]** - *Network diagram illustrating the concept*

“D” = Down

📊 **[Diagram]** - *Network diagram illustrating the concept*

Changing one of the Member interfaces using “switchport mode access” has made it different than the other members so it is now appearing as “s” = suspended

Another useful command

💡 “show etherchannel port-channel”

📊 **[Diagram]** - *Network diagram illustrating the concept*

💡 “show spanning-tree” will show the single EtherChannel port interface

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

LAYER 3 ETHERCHANNELS

📊 **[Diagram]** - *Network diagram illustrating the concept*

HOW TO CONFIGURE A LAYER 3 ETHERCHANNEL (from a clean configuration)

📊 **[Diagram]** - *Network diagram illustrating the concept*

💡 “show running-config”

📊 **[Diagram]** - *Network diagram illustrating the concept*

NOTE : No SWITCHPORT and NO IP INTERFACE.

Where do we configure the IP Address?  Directly on the PORT INTERFACE !

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

(”RU” - “R” = Layer 3, “U” = in use)

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

COMMANDS LEARNED IN THIS CHAPTER
```
SW(config) port-channel load-balance *mode*
```
Configures the EtherChannel load-balancing method on a SWITCH 
```
SW# show etherchannel load-balance
```
Displays information about the load-balancing settings
```
SW(config-if)# channel-group *number* mode {desirable | auto | active | passive | on}
```
Configures an interface to be PART of an EtherChannel
```
SW# show etherchannel summary
```
Displays a summary of EtherChannels on a SWITCH
```
SW# show etherchannel port-channel
```
Displays information about the virtual port-channel interfaces on a SWITCH

📊 **[Diagram]** - *Network diagram illustrating the concept*
