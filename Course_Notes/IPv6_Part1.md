# 31. IPv6 : PART 1

HEXIDECIMAL (Review)

[Image removed]

[Image removed]

[Image removed]

What about the reverse (Hex to Binary) ??? 

[Image removed]

---

WHY IPv6?

- The **MAIN REASON** is that there are simply not enough IPv4 addresses available
- There are 2^32 IPv4 Addresses available (4,294,967,296)
- When IPv4 was being designed 30 years ago, the creators had NO idea the Internet would be as large as today
- VLSM, Private IPv4 ADDRESSES, and NAT have been used to conserve the use of IPv4 ADDRESS SPACE.
    - These are short-term solutions, however.
- The LONG -TERM solution is IPv6

- IPv4 ADDRESS assignments are controlled by IANA (Internet Assigned Number Authority)
- IANA distributes IPv4 ADDRESS space to various RIRs (Regional Internet Registries), which then assign them to companies that need them.

[Image removed]

- On September 24th, 2015, ARIN declared exhaustion of the ARIN IPv4 address pool
- On August 21st, 2020, LACNIC announced that it had made its final IPv4 allocation

---

BASICS OF IPv6

- An IPv6 ADDRESS is **128 bits (8 "groups", 16 bits per "group". Groups are separated by ':')**

[Image removed]

- An IPv6 ADDRESS uses the / prefix number

SHORTENING (Abbreviating) IPv6 ADDRESSES

[Image removed]

[Image removed]

[Image removed]

[Image removed]

[Image removed]

EXPANDING (Abbreviating) IPv6 ADDRESSES

[Image removed]

FINDING the IPv6 PREFIX (GLOBAL UNICAST ADDRESSES)

- Typically, an Enterprise requesting IPv6 ADDRESSES from their ISP will receive a /48 BLOCK
- Typically, IPv6 SUBNETS use a /64 PREFIX LENGTH
- That means an Enterprise has 16 bits to use to make SUBNETS
- The remaining 64 bits can be used for HOSTS

[Image removed]

[Image removed]

(Each digit is 4 bits / each 4 digit block is 16 bits)

**REMEMBER** : You can only remove the LEADING ZEROS !!!

2001 : 0DB8 : 8B00 : 0001 : FB89 : 017B : 0020 : 0011  /93

Because 93 lands in the middle of a 4 bit number, we need to convert the last digit to binary and borrow a “bit” from the first binary digit.

:: 017 [B] :: B = 0d11 = 0b1011 = 0b1000 (the first digit is borrowed, the remainder become 0)

[Image removed]

[Image removed]

---

CONFIGURING IPv6 ADDRESSES

[Image removed]

This allows the ROUTER to perform IPv6 ROUTING

<aside>
💡 R1(config) #ipv6 unicast-routing

</aside>

Configuring an INTERFACE with an IPv6 Address

<aside>
💡 R1(config) #int g0/0
R1(config-if) #ipv6 address 2001:db8:0:0::1/64
R1(config) #no shutdown

</aside>

You can also type out the full address (if necessary)

[Image removed]

NOTE ABBREVIATED IPv6 ADDRESSES SHOWN

LINK-LOCAL ADDRESSES are automatically added when creating an IPv6 INTERFACE (Covered in IPv6 - PART 2 Lecture)
