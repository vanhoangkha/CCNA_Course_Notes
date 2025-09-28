# 39. DHCP (Dynamic Host Configuration Protocol)

THE PURPOSE OF DHCP

- DHCP is used to allow HOSTS to automatically / dynamically learn various aspects of their NETWORK configuration; without MANUAL / STATIC configuration
- It is an ESSENTIAL part of modern NETWORKS
    - When you connect a phone / laptop to WiFi, do you ask your NETWORK admin which IP ADDRESS, SUBNET MASK, DEFAULT GATEWAY, etc the phone / laptop should use ?
- Typically used for CLIENT devices (workstations, phones, etc)
- DEVICES (such as ROUTERS, SERVERS, etc) are usually MANUALLY configured
- In small NETWORKS (such as Home NETWORKS), the ROUTER typically acts as the DHCP SERVER for HOSTS in the LAN
- In LARGE NETWORKS, the DHCP SERVER is usually a Windows / Linux SERVER

---

BASIC FUNCTIONS OF DHCP

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

Note: ALL the IPs are the same because this is Jeremy’s Home ROUTER (it provides all these services)

Command `ipconfig /release`

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

Wireshark capture of the `ipconfig /release` mechanism

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

Command `ipconfig /renew`

📊 **[Diagram]** - *Network diagram illustrating the concept*

Renewing Process has FOUR messages:

📊 **[Diagram]** - *Network diagram illustrating the concept*

1) DHCP DISCOVER

- Are there any DHCP Servers in this NETWORK? I need an IP ADDRESS ?

📊 **[Diagram]** - *Network diagram illustrating the concept*

NOTE the use of DHCP Reserved Ports 67 and 68

2) DHCP OFFER:

- How about THIS IP ADDRESS ?

📊 **[Diagram]** - *Network diagram illustrating the concept*

- The DHCP OFFER message can be either BROADCAST or UNICAST
- NOTE OPTIONS at the bottom : Message Type, Server ID, Lease Time, Subnet, etc.

3) DHCP REQUEST

- I want to use the IP ADDRESS that was offered

📊 **[Diagram]** - *Network diagram illustrating the concept*

4) DHCP ACK

- Okay! You may use THAT ADDRESS

📊 **[Diagram]** - *Network diagram illustrating the concept*

---
DHCP RENEW PROCESS SUMMARY

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

DHCP RELAY

- Some NETWORK engineers might choose to configure each ROUTER to act as the DHCP SERVER for its connected LANS
- However, large enterprises often choose to use a CENTRALIZED DHCP SERVER
- If the SERVER is centralized, it won’t receive the DHCP CLIENTS’ Broadcast DHCP messages
- To FIX this, you can configure a ROUTER to act as a DHCP RELAY AGENT
- The ROUTER will forward the clients’ Broadcast DHCP messages to the remote DHCP SERVER as a Unicast messages

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

CONFIGURING DHCP IN CISCO IOS

Commands for configuring DHCP SERVERS in Cisco IOS

📊 **[Diagram]** - *Network diagram illustrating the concept*

Command `show ip dhcp binding`

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

DHCP RELAY AGENT CONFIGURATION IN IOS

📊 **[Diagram]** - *Network diagram illustrating the concept*

RELAY AGENT MUST HAVE CONNECTIVITY WITH DHCP SERVER

---

DHCP CLIENT CONFIGURATION IN IOS

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

COMMANDS SUMMARY

📊 **[Diagram]** - *Network diagram illustrating the concept*
