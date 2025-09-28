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

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Note: ALL the IPs are the same because this is Jeremy’s Home ROUTER (it provides all these services)

Command `ipconfig /release`

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Wireshark capture of the `ipconfig /release` mechanism

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

Command `ipconfig /renew`

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Renewing Process has FOUR messages:

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

1) DHCP DISCOVER

- Are there any DHCP Servers in this NETWORK? I need an IP ADDRESS ?

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

NOTE the use of DHCP Reserved Ports 67 and 68

2) DHCP OFFER:

- How about THIS IP ADDRESS ?

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- The DHCP OFFER message can be either BROADCAST or UNICAST
- NOTE OPTIONS at the bottom : Message Type, Server ID, Lease Time, Subnet, etc.

3) DHCP REQUEST

- I want to use the IP ADDRESS that was offered

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

4) DHCP ACK

- Okay! You may use THAT ADDRESS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---
DHCP RENEW PROCESS SUMMARY

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

DHCP RELAY

- Some NETWORK engineers might choose to configure each ROUTER to act as the DHCP SERVER for its connected LANS
- However, large enterprises often choose to use a CENTRALIZED DHCP SERVER
- If the SERVER is centralized, it won’t receive the DHCP CLIENTS’ Broadcast DHCP messages
- To FIX this, you can configure a ROUTER to act as a DHCP RELAY AGENT
- The ROUTER will forward the clients’ Broadcast DHCP messages to the remote DHCP SERVER as a Unicast messages

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

CONFIGURING DHCP IN CISCO IOS

Commands for configuring DHCP SERVERS in Cisco IOS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `show ip dhcp binding`

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

DHCP RELAY AGENT CONFIGURATION IN IOS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

RELAY AGENT MUST HAVE CONNECTIVITY WITH DHCP SERVER

---

DHCP CLIENT CONFIGURATION IN IOS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

COMMANDS SUMMARY

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)
