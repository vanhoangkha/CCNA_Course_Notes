# 44. NAT (STATIC): PART 1

PRIVATE IPv4 ADDRESSES (RFC 1918)

- IPv4 doesn’t provide enough ADDRESSES for all DEVICES that need an IP ADDRESS in the modern world
- The long-term solution is to switch to IPv6
- There are THREE MAIN short-term solutions:
    - CIDR
    - PRIVATE IPv4 ADDRESS
    - NAT
- RFC 1918 specifies the following IPv4 ADDRESS RANGES as PRIVATE:
    
    ```
    10.0.0.0 /8       (10.0.0.0 to 10.255.255.255)             CLASS A 
    172.16.0.0 /12    (172.16.0.0 to 172.31.255.255)           CLASS B
    192.168.0.0 /16   (192.168.0.0 to 192.168.255.255)         CLASS C
    ```
    
- You are free to use these ADDRESSES in your NETWORKS. They don’t have to be GLOBALLY UNIQUE

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

INTRO TO NAT

- NETWORK ADDRESS TRANSLATION (NAT) is used to modify the SOURCE and / or DESTINATION IP ADDRESSES of packets
- There are various reasons to use NAT, but the MOST common reason is to ALLOW HOSTS with PRIVATE IP ADDRESSES to communicate with other HOSTS over the INTERNET
- For the CCNA you have to understand SOURCE NAT and how to configure it on CISCO ROUTERS

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

STATIC NAT

- STATIC NAT involves statically configuring ONE-TO-ONE MAPPINGS of PRIVATE IP ADDRESSES to PUBLIC ADDRESSES

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

PRIVATE IP CANNOT BE MAPPED TO THE SAME GLOBAL IP

THE SECOND MAPPING WILL BE REJECTED

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

STATIC NAT CONFIGURATIONS

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

Command `clear ip nat translation`

📊 **[Diagram]** - *Network diagram illustrating the concept*

Command `show ip nat statistics`

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

COMMAND REVIEW

📊 **[Diagram]** - *Network diagram illustrating the concept*
