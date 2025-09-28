# 38. DNS (Domain Name System)

THE PURPOSE OF DNS

- DNS is used to *resolve* human-readable names (google.com) to IP ADDRESSES
- Machines such as PCs don’t use names, they use ADDRESSES (ie: IPv4/IPv6)
- Names are much easier for us to use and remember than IP ADDRESSES
    - What is the IP ADDRESS of [youtube.com](http://youtube.com) ?
- When you type ‘youtube.com` into a web browser, your device will ask a DNS SERVER for the IP ADDRESS of [youtube.com](http://youtube.com)
- The DNS SERVER(S) your DEVICE uses can be manually configured or learned via DHCP

---

BASIC FUNCTIONS OF DNS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `ipconfig /all` (Show local IP configuration on current DEVICE)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `nslookup` (Shows IP information for a given DNS entry)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

WIRESHARK CAPTURE of above  COMMANDS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `ipconfig /displaydns` (Displays DNS cache)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `ipconfig /flushdns` (Clears DNS cache)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

HOSTS Files

WINDOWS HOSTS location

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

CONFIGURING DNS IN CISCO IOS

- For HOSTS in a NETWORK to use DNS, you don’t need to configure DNS on the ROUTERS.
    - They will simply FORWARD the DNS messages like any other packets
- However, a CISCO ROUTER can be configured as a DNS SERVER, although it’s rare
    - If an INTERNAL DNS SERVER is used, usually it’s a WINDOWS or LINUX SERVER
- A CISCO ROUTER can also be configured as a DNS CLIENT

Command `ip dns server` and `ip host <hostname> <ip address>`

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `show hosts`

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Command `ip name-server` and `ip domain lookup`

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

COMMAND REVIEW:

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)
