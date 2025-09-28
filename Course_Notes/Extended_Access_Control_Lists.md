# 35. EXTENDED ACCESS CONTROL LISTS (EACL)

ANOTHER WAY TO CONFIGURE NUMBERED ACLs

- In DAY 34, you learned that numbered ACLs are configured in Global Config mode:

[Image removed]

- You learned that named ACLs are configured with subcommands in a separate config mode:

[Image removed]

- However, in modern IOS you can also configure numbered ACLs in the exact same way as named ACLs:

[Image removed]

[Image removed]

---

ADVANTAGES OF NAMED ACL CONFIG MODE

- You can easily DELETE individual entries in the ACL with NO *entry-number*
- You can easily DELETE individual entries in the ACL with NO *sequence-number*

[Image removed]

This doesn’t work with NUMBERED access lists

[Image removed]

- You can insert NEW entries in-between other entries by specifying the SEQUENCE NUMBER

[Image removed]

---

RESEQUENCING ACLs

- There is a *resequencing* function that helps edit ACLs
- The command is  `R1(config)#ip access-list resequence *acl-id starting-seq-num increment*`

[Image removed]

---

EXTENDED NUMBERS AND NAMED ACLs

- EXTENDED ACLs function mostly the same as STANDARD ACLs
- They can be NUMBERED or NAMED, just like STANDARD ACLs
    - NUMBERED ACLs use the following ranges: **100 - 199, 2000 - 2699**
- Processed from TOP to BOTTOM, just like STANDARD ACLs
- However, they can match traffic based on MORE PARAMETERS, so they are more PRECISE (and more complex) than STANDARD ACLs
- We will focus on matching based on these main parameters:
    - **LAYER 4 protocol / port**
    - **Source Address**
    - D**estination Address**

---

EXTENDED NUMBERED ACL

<aside>
💡 `R1(config)# access-list *number* [permit | deny] *protocol src-ip dest-ip*`

</aside>

EXTENDED NAMED ACL

<aside>
💡 `R1(config)# ip access-list extended {name | number}`

</aside>

<aside>
💡 `R1(config-ext-nacl)# {seq-num} {permit | deny} *protocol src-ip dest-ip*`

</aside>

---

MATCHING THE PROTOCOL

[Image removed]

IP Protocol Number is the number used in the IPv4 Header Protocol field

Examples: (1) ICMP, (6) TCP, (17) UDP, (88) EIGRP, (89) OSPF

MATCHING THE SOURCE / DESTINATION IP ADDRESS

[Image removed]

This command:

<aside>
💡 `R1(config-ext-nacl)#deny tcp any 10.0.0.0 0.0.0.255`

</aside>

Deny ALL PACKETS that encapsulate a TCP segment from ANY source to DESTINATION 10.0.0.0/24

---

PRACTICE QUESTIONS:

1) ALLOW ALL TRAFFIC

`R1(config-ext-nacl)# permit ip any any` (ip is used for “all protocols”)

2) PREVENT 10.0.0.0/16 from SENDING UDP traffic to 192.168.1.1/32

`R1(config-ext-nacl)# deny udp 10.0.0.0 0.0.255.255 host 192.168.1.1`

3) PREVENT 172.16.1.1/32 from pinging hosts in 192.168.0.0/24

`R1(config-ext-nacl)# deny icmp host 172.16.1.1 192.168.0.0 0.0.0.255`

MATCHING THE TCP /  UDP PORT NUMBERS

- When matching TCP / UDP, you can optionally specify the SOURCE and/or DESTINATION PORT NUMBERS to match

[Image removed]

eq = equal than

gt = greater than

lt = less than

neq = not equal to

range = range of ports

You can use either the PORT NUMBER or the specific TYPE (that has a KNOWN PORT NUMBER)

[Image removed]

[Image removed]

---

PRACTICE QUESTIONS 2:

1) ALLOW TRAFFIC from 10.0.0.0/16 to access the server at 2.2.2.2/32 using HTTPS

`R1(config-ext-nacl)# permit tcp 10.0.0.0 0.0.255.255 host 2.2.2.2 eq 443`

2) PREVENT ALL HOSTS using SOURCE UDP Port Numbers from 20000 to 30000 from accessing the server at 3.3.3.3/32

`R1(config-ext-nacl)# deny udp any range 20000 30000 host 3.3.3.3`

3) ALLOW HOSTS in 172.16.1.0/24 using a TCP SOURCE Port greater than 9999 to access ALL TCP ports on server 4.4.4.4/32 EXCEPT port 23

`R1(config-ext-nacl)# permit tcp 172.16.1.0 0.0.0.255 gt 9999 host 4.4.4.4 neq 23`

EXAMPLE NETWORK

[Image removed]

[Image removed]

REQUIREMENTS:

- Hosts in 192.168.1.0/24 can’t use HTTPS to access SRV1
- Hosts in 192.168.2.0/24 can’t access 10.0.2.0/24
- NONE of the hosts in 192.168.1.0/24 or 192.168.2.0/24 can ping 10.0.1.0/24 OR 10.0.2.0/24

EXTENDED ACL #1 (Applied at R1 G0/1 INBOUND interface)

`R1(config)# ip access-list extended HTTP_SRV1`
`R1(config-ext-nacl)# deny tcp 192.168.1.0 0.0.0.255 host 10.0.1.100 eq 443`

`R1(config-ext-nacl)# permit ip any any`

`R1(config-ext-nacl)# int g0/1`

`R1(config-if)# ip access-group HTTP_SRV1 in`

EXTENDED ACL #2 (APPLIED at R1 G0/2 INBOUND interface)

`R1(config)# ip access-list extended BLOCK_10.0.2.0`

`R1(config-ext-nacl)# deny ip 192.168.2.0 0.0.0.255 10.0.2.0 0.0.0.255`

`R1(config-ext-nacl)# permit ip any any`

`R1(config-ext-nacl)# int g0/2`

`R1(config-if)# ip access-group BLOCK_10.0.2.0 in`

EXTENDED ACL #3 (APPLIED at R1 g0/0 OUTBOUND interface)

`R1(config)# ip access-list extended BLOCK_ICMP`

`R1(config-ext-nacl)# deny icmp 192.168.1.0 0.0.0.255 10.0.1.0 0.0.0.255`

`R1(config-ext-nacl)# deny icmp 192.168.1.0 0.0.0.255 10.0.2.0 0.0.0.255`

`R1(config-ext-nacl)# deny icmp 192.168.2.0 0.0.0.255 10.0.1.0 0.0.0.255`

`R1(config-ext-nacl)# permit ip any any`

`R1(config-ext-nacl)# int g0/0`

`R1(config-if)# ip access-group BLOCK_ICMP out`

What the EXTENDED ACLs look like

[Image removed]

HOW TO SEE WHICH EXTENDED ACL’s ARE APPLIED TO AN INTERFACE

[Image removed]
