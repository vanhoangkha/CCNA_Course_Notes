# 28. OSPF : PART 3 (IGP: LINK STATE)

LOOPBACK INTERFACES

- A LOOPBACK INTERFACE is a virtual INTERFACE in the ROUTER
- It is ALWAYS UP/UP - unless you manually shut it down
- It is NOT dependent on a PHYSICAL INTERFACE
- So, it provides a consistent IP ADDRESS that can be used to REACH / IDENTIFY the ROUTER

[Image removed]

---

OSPF NETWORK TYPES

- The OSPF “NETWORK TYPE” refers to the TYPES of connection between OSPF neighbors (Ethernet, etc.)

- There are THREE MAIN OSPF NETWORK TYPES:

- BROADCAST :
    - Enabled by DEFAULT on **ETHERNET** and **FDDI** (Fiber Distributed Data Interfaces) INTERFACES

- POINT TO POINT :
    - Enabled by DEFAULT on **PPP** (Point-to-Point) and **HDLC** (High-Level Data Link Control) INTERFACES

- NON-BROADCAST :
    - Enabled by DEFAULT on **FRAME RELAY** and **X.25** INTERFACES

<aside>
💡  CCNA focuses on BROADCAST and POINT-TO-POINT types

</aside>

---

OSPF BROADCAST NETWORK TYPE

[Image removed]

- Enabled on ETHERNET and FDDI interfaces by DEFAULT
- ROUTERS *dynamically discover* neighbors by SENDING / LISTENING for OSPF “Hello” messages using the multicast address 224.0.0.5
- A **DR (DESIGNATED ROUTER)** and **BDR (BACKUP DESIGNATION ROUTER)** must be elected on each subnet (only DR if there are no OSPF neighbors, ie: R1’s G1/0 INTERFACE)
- ROUTERS which aren’t the DR or BDR become a **DROther**

[Image removed]

The DR / BDR election order of priority:

1) Highest OSPF INTERFACE PRIORITY

2) Highest OSPF ROUTER ID

“First Place” becomes the DR for the SUBNET

“Second Place” because the BDR

<aside>
💡 DEFAULT OSPF INTERFACE PRIORITY is “1” on ALL INTERFACES!

</aside>

The command to change the OSPF PRIORITY of an INTERFACE is :

<aside>
💡 R2(config-if)# ip ospf priority <priority number>

</aside>

[Image removed]

<aside>
💡 IF an OSPF PRIORITY is set to “0”, the ROUTER CANNOT be the DR / BDR for the SUBNET!

</aside>

The DR / DBR ELECTION is “non-preemptive”.

Once the DR / DBR are selected, they will keep their role until OSPF is:

- Reset
- Interface fails
- Is shut down
- etc.

[Image removed]

[Image removed]

<aside>
💡 In the BROADCAST NETWORK TYPE, ROUTERS will only form a FULL OSPF ADJACENCY with the DR and the BDR of the SEGMENT!

</aside>

Therefore, ROUTERS only exchange LSAs with the DR and BDR.

DROthers will NOT exchange LSAs with each other.

ALL ROUTERS will still have the same LSDB but THIS reduces the amount of LSAs flooding the NETWORK

<aside>
💡 MESSAGES to the DR / BDR are MULTICAST to 224.0.0.6

</aside>

The DR and BDR will form a FULL ADJACENCY with ALL ROUTERS in the SUBNET

DROthers will form a FULL ADJACENCY ONLY with the DR / BDR !

[Image removed]

---

OSPF POINT-TO-POINT NETWORK TYPE

[Image removed]

- ENABLED on **SERIAL** INTERFACES using the **PPP** and **HDLC** encapsulations, by DEFAULT
- ROUTERS dynamically discover neighbors by SENDING / LISTENING for OSPF “Hello” messages using the multicast address 224.0.0.5
- A DR and BDR are NOT elected
- These ENCAPSULATIONS are used for “Point-To-Point” connections
    - Therefore, there is no point in electing  a DR and DBR
    - The TWO ROUTERS will form a FULL ADJACENCY with each other

---

(ASIDE)

SERIAL INTERFACES

[Image removed]

- One side of SERIAL CONNECTION functions as DCE (Data Communications Equipment)
- The OTHER side functions as DTE (Data Terminal Equipment)
- ONLY the DCE side needs to specify the *clock rate* (speed) of the connection

ETHERNET INTERFACES use the “speed” command to configure the operating speed.

SERIAL INTERFACES use the “clock rate” command

[Image removed]

If you change the ENCAPSULATION, it must MATCH on BOTH ENDS or the INTERFACE will go down.

[Image removed]

R1 and R2 sharing the SAME Encapsulation Type 

[Image removed]


SERIAL INTERFACES SUMMARY

- The DEFAULT encapsulation is HDLC
- You can configure PPP encapsulation with this command:
    
    <aside>
    💡 R1(config-if)# **encapsulation ppp**
    
    </aside>
    
- One side is DCE, other side is DTE
- Identify which side is DCE / DTE :
    
    <aside>
    💡 R1# **show controllers** *interface-id*
    
    </aside>
    
- You must configure the CLOCK RATE on the DCE side:
    
    <aside>
    💡 R1(config-if)# clock rate *bits-per-second*
    
    </aside>
    

---

[Image removed]

[Image removed]

- You can configure the OSPF NETWORK TYPE on an INTERFACE with :

<aside>
💡 R1(config-if)# ip ospf network <network type>

</aside>

For example, if TWO ROUTES are directly connected with an ETHERNET link, there is no need for a DR / DBR. You can configure the POINT-TO-POINT NETWORK type in this case

NOTE: Not all NETWORK TYPES work on ALL LINK TYPES (for example, a serial link cannot use the BROADCAST NETWORK type)

[Image removed]

<aside>
💡 NON-BROADCAST NETWORK type Default Timers : Hello 30, Dead 120

</aside>

---

OSPF NEIGHBOUR / ADJACENCY REQUIREMENTS

1) AREA NUMBER MUST MATCH

2) INTERFACES must be in the SAME SUBNET

3) OSPF PROCESS must not be **SHUTDOWN**

[Image removed]

4) OSPF ROUTER ID must be unique

[Image removed]

5) HELLO and DEAD Timers must MATCH

6) AUTHENTICATION settings must MATCH

[Image removed]

*** SPECIAL REQUIREMENTS *** 

7) IP MTU settings must MATCH

- IP MTU : Maximum size of an IP Packet that can be sent from an INTERFACE
- If the settings DO NOT match, can still become OSPF Neighbors but OSPF WILL NOT operated properly

8) OSPF NETWORK TYPE must match

- will appear to be working but NEIGHBOR won’t appear in ROUTING information

---

OSPF LSA TYPES

- The OSPF LSDB is made up of LSAs
- There are 11 types of LSA but there are only 3 you should be aware of for the CCNA:
    - Type 1 (Router LSA)
    - Type 2 (Network LSA)
    - Type 5 (AS External LSA)

TYPE 1 (Router LSA)

- Every OSPF ROUTER generates this type of LSA
- It identifies the ROUTER using it’s ROUTER ID
- It also lists NETWORKS attached to the ROUTER’s OSPF-Activated INTERFACES

TYPE 2 (Network LSA)

- Generated by the DR of EACH “multi-access” NETWORK (ie: the BROADCAST network type)
- Lists the ROUTERS which are attached to the multi-access NETWORK

TYPE 5 (AS-External LSA)

- Generated by ASBRs to describe ROUTES to DESTINATIONS outside of the AS (OSPF Domain)
