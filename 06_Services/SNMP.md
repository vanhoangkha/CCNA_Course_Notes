# 40. SNMP (Simple Network Management Protocol)

SNMP OVERVIEW

- SNMP is an INDUSTRY-STANDARD FRAMEWORK and PROTOCOL that was originally released in 1988

These RFCs make up SNMPv1 (Do not need to memorize)

```
RFC 1065 - Structure and identification of management information for TCP/IP based internets
RFC 1066 - Management information base for network management of TCP/IP based internets
RFC 1067 - A simple network management protocol
```

- Don’t let the ‘Simple’ in the name fool you !
- SNMP can be used to monitor the STATUS of DEVICES, make CONFIGURATION CHANGES, etc.
- There are TWO MAIN TYPES of DEVICES in SNMP:
    - MANAGED DEVICES
        - These are the DEVICES being managed using SNMP
            - Ex: ROUTERS, SWITCHES
    - NETWORK MANAGEMENT STATION (NMS)
        - The DEVICE / DEVICES managing the MANAGED DEVICES
        - THIS is the SNMP ‘SERVER’

---

SMNP OPERATIONS

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

SMNP COMPONENTS

OVERVIEW

📊 **[Diagram]** - *Network diagram illustrating the concept*

NMS

📊 **[Diagram]** - *Network diagram illustrating the concept*

MANAGED DEVICES

📊 **[Diagram]** - *Network diagram illustrating the concept*

SNMP OIDs

- SNMP Object IDs are ORGANIZED in a HIERARCHICAL STRUCTURE

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

SNMP VERSIONS

- Many versions of SNMP have been proposed/developed, however, only three major versions have achieved wide-spread use:

- **SNMPv1**
    - The ORIGINAL version of SNMP
- **SNMPv2c**
    - Allows the NMS to retrieve LARGE AMOUNTS of information in a SINGLE REQUEST, so it is more efficient
    - ‘c’ refers to the ‘community strings’ used as PASSWORDS in SNMPv1, removed from SNMPv2, and then added BACK for SNMPv2
- **SNMPv3**
    - A much more SECURE version of SNMP that supports STRONG ENCRYPTION and AUTHENTICATION.
        
        <aside>
        💡 WHENEVER POSSIBLE, this version should be used!
        
        </aside>
        

---

SNMP MESSAGES

📊 **[Diagram]** - *Network diagram illustrating the concept*

1) SNMP READ

📊 **[Diagram]** - *Network diagram illustrating the concept*

2) SMNP WRITE

📊 **[Diagram]** - *Network diagram illustrating the concept*


3) SNMP NOTIFICATION

📊 **[Diagram]** - *Network diagram illustrating the concept*


SNMP AGENT listens for MESSAGES on UDP Port 161

SNMP MANAGER listens for MESSAGES on UDP Port 162

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

SNMPv2c CONFIGURATION (Basic)

📊 **[Diagram]** - *Network diagram illustrating the concept*

WHAT HAPPENS WITH R1’s G0/1 INTERFACE GOES DOWN?

📊 **[Diagram]** - *Network diagram illustrating the concept*

NOTE:

UDP message sent to Destination Port 162 (SNMP Manager)

“version” is set to v2c

community is “Jeremy1” (Read Only - no Set messages)

snmpV2-trap : trap message sent due to interface G0/1 going down

variable-bindings : contains the OID sent to identify the issue.

---

SNMP SUMMARY

- SNMP helps MANAGE DEVICES over a NETWORK
- MANAGED DEVICES are the devices being managed using SNMP (such as ROUTERS, SWITCHES, FIREWALLS)
- NETWORK MANAGEMENT STATIONS (NMS) are the SNMP “servers” that manage the devices
    - NMS receives notifications from Managed Devices
    - NMS changes settings on Managed Devices
    - NMS checks status of Managed Devices
    
- Variables, such as Interface Status, Temperature, Traffic Load, Hostname, etc are STORED in the MANAGMENT INFORMATION BASE (MIB) and identified using Object IDs (OIDs)

Main SNMP versions : SNMPv1, SNMPv2c, SNMPv3

```
SNMP MESSAGES : 
* Get / GetNext / GetBulk
* Set
* Trap
* Inform
* Response
```
