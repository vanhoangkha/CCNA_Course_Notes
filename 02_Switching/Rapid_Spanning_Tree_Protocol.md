# 22. RAPID SPANNING TREE PROTOCOL

*COMPARISON OF STP VERSIONS (Standard vs. Cisco)*

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)


We are only concerned with 802.1w for MOST use cases.

MSTP (802.1s) is more useful for VERY LARGE networks.

WHAT IS RAPID PER-VLAN SPANNING TREE PLUS?

> RSTP is not a time-based spanning tree algorithm like 802.1D. Therefore, RSTP offers an improvment over teh 30 seconds or more 802.1D takes to move a link to forwarding. The heart of the protocol is a new bridge-bridge handshake mechanism, which allows ports to move directly to forwarding

---

SIMILARITIES BETWEEN STP AND RSTP:

- RSTP serves the same purpose as STP, blocking specific PORTS to prevent LAYER 2 LOOPS.
- RSTP elects a ROOT BRIDGE with the same rules as STP
- RSTP elects ROOT PORTS with the same rules as STP
- RSTP elects DESIGNATED PORTS with the same rules as STP

---

DIFFERENCES BETWEEN STP AND RSTP:

**PORT COSTS**

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)


(STUDY AND MEMORIZE PORT COSTS OF STP AND RSTP)

RSTP PORT STATES

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- If a PORT has been ADMINISTRATIVELY DISABLED (”shutdown” command) = DISCARDING STATE
- If a PORT is ENABLED but BLOCKING traffic to prevent LAYER 2 LOOPS = DISCARDING STATE

---

RSTP ROLES

- The ROOT PORT role remains unchanged in RSTP
    - The PORT that is closest to the ROOT BRIDGE becomes the ROOT PORT for the SWITCH
    - The ROOT BRIDGE is the only SWITCH that doesn’t have a ROOT PORT
- The DESIGNATED PORT role remains unchanged in RSTP
    - The PORT on a segment (Collision Domain) that sends the best BPDU is that segment’s DESIGNATED PORT (only one per segment!)
- The NON-DESIGNATED PORT role is split into TWO separate roles in RSTP:
    - The ALTERNATE PORT role
    - The BACKUP PORT role

**RSTP : ALTERNATE PORT ROLE**

- The RSTP ALTERNATE PORT ROLE is a DISCARDING PORT that receives a superior BPDU from another SWITCH
- This is the same as what you’ve learned about BLOCKING PORTS in classic STP

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- An ALTERNATE PORT (labelled “A” above) functions as a backup to the ROOT PORT
- If the ROOT PORT fails, the SWITCH can immediately move it’s best alternate port to FORWARDING

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

💡 This immediate move to FORWARDING STATE functions like a classic STP optional feature called **UplinkFast.** Because it is built into RSTP, you do not need to activate UplinkFast when using RSTP/Rapid PVST+

One more STP optional feature that was built into RSTP is **BackboneFast**

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- **BackboneFast** allows SW3 to expire the MAX AGE TIMERS on it’s INTERFACE and rapidly FORWARD the superior BPDUs to SW2
- This FUNCTIONALITY is built into RSTP, so it does not need to be configured.

UPLINKFAST and BACKBONE FAST (SUMMARY)

💡 **UplinkFast** and **BackboneFast** are two optional features in Classic STP. They must be configured to operate on the SWITCH (not necessary to know for the CCNA)

- Both features are built into RSTP, so you do NOT have to configure them. They operate, by DEFAULT
- You do NOT need to have a detailed understanding of them for the CCNA. Know their names and their BASIC purpose (to help BLOCKING / DISCARDING PORTS rapidly move to FORWARDING)

---

**RSTP : BACKUP PORT ROLE**

- The RSTP BACKUP PORT role is a DISCARDING PORT that receives a superior BPDU from another INTERFACE on the same SWITCH
- This only happens when TWO INTERFACES are connected to the SAME COLLISION DOMAIN (via a HUB)
- Hubs are NOT used in modern networks, so you will probably NOT encounter an RSTP BACKUP PORT
- Hubs are NOT used in modern networks, so you will probably NOT encounter an RSTP BACKUP PORT.
- Functions as a BACKUP for a DESIGNATED PORT

💡 The INTERFACE with the LOWERS PORT ID will be selected as the DESIGNATED PORT, and the other will be the BACKUP port.

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

WHICH Switch will be ROOT BRIDGE?
What about the OTHER ports ?

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

💡 RAPID STP *is* compatible with CLASSIC STP.
💡 The INTERFACE(S) on the RAPID STP-enabled SWITCH connected to the CLASSIC STP-enabled SWITCH will operate in CLASSIC STP MODE (Timers, BLOCKING >>> LISTENING >>> LEARNING >>> FORWARDING, etc.)

---

RAPID STP BPDU

CLASSIC RSTP (LEFT) vs RAPID STP BPDU (RIGHT)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)


💡 NOTE:

Classic STP BPDU has a “Protocol Version Identifier: Spanning Tree (0)

BPDU Type: Configuration (0x00)

BPDU flags: 0x00

RAPID STP BPDU has a “Protocol Version Identifier: Spanning Tree (2)

BPDU Type: Configuration (0x02)

BPDU flags: 0x3c


In CLASSIC STP, only the ROOT BRIDGE originated BPDUs, and other SWITCHES just FORWARDED the BPDUs they received. 

In RAPID STP, ALL SWITCHES originate and send their own BPDUs from their DESIGNATED PORTS

---

RAPID SPANNING TREE PROTOCOL

- ALL SWITCHES running RAPID STP send their own BPDUs every “hello” time (2 Seconds)
- SWITCHES “age” the BPDU information much more quickly
    - In CLASSIC STP, a SWITCH waits 10 “hello” intervals (20 seconds)
    - In RAPID STP, a SWITCH considers a neighbour lost if it misses 3 BPDUs (6 seconds). It will then “flush” ALL MAC ADDRESSES learned on that interface

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

RSTP LINK TYPES

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

```
<E> = EDGE

<P> = POINT-TO-POINT

<S> = SHARED
```

RSTP distinguishes between THREE different “link types” : **EDGE**, **POINT-TO-POINT**, and **SHARED**

EDGE PORTS

- Connected to END HOSTS
- Because there is NO RISK of creating a LOOP, they can move straight to the FORWARDING STATE without the negotiation process!
- They function like a CLASSIC STP PORT with PORTFAST ENABLED

💡 SW1(config-if)# spanning-tree portfast

---

POINT-TO-POINT PORTS

- Connect directly to another SWITCH
- They function in FULL-DUPLEX
- You don’t need to configure the INTERFACE as POINT-TO-POINT (it should be detected)

💡 SW1(config-if)# spanning-tree link-type point-to-point

---

SHARED PORTS

- Connect to another SWITCH (or SWITCHES) via a HUB
- They function in HALF-DUPLEX
- You don’t need to configure the INTERFACE as SHARED (it should be detected)

💡 SW1(config-if)# spanning-tree link-type shared

---

QUIZ:

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

SW1 :

- **ROOT BRIDGE**
- G0/0 - 0/3= DESIGNATED

SW2 : 

- G0/0 = ROOT PORT
- G0/1 = DESIGNATED PORT
- G0/2 = BACKUP PORT
- G0/3 = DESIGNATED PORT

SW3 :

- G0/0 = DESIGNATED PORT
- G0/1 = ALTERNATE PORT
- G0/2 = ROOT PORT
- G0/3 = DESIGNATED PORT

SW4:

- G0/0 = ROOT
- G0/1 = ALTERNATE PORT
- G0/2 = DESIGNATED PORT

Connection between SW1 G0/0 and SW2 G0/0 = POINT-TO-POINT

Connection between SW3 G0/0 and SW4 G0/0 = POINT-TO-POINT

Connection between SW1 G0/1 and G0/2 to SW3 G0/1 and G0/2 = POINT-TO-POINT

Connections to all the END HOSTS = EDGE 

Connection from SW4 to HUB = SHARED

Connections from SW2 to HUB = SHARED

ANSWER

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)
