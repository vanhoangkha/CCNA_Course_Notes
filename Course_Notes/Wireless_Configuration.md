# 58. WIRELESS CONFIGURATION

TOPOLOGY INTRODUCTION

[Image removed]

INTERNAL PC (VLAN 100) ACCESSING DEFAULT GATEWAY via Internal CAPWAP tunnel

[Image removed]

REACHING External GUEST PC  via DEFAULT GATEWAY + Internal and External CAPWAP tunnels

[Image removed]

---

LAYER 3 SWITCH CONFIGURATION (SW1)

[Image removed]

PART 2 of configuration

Note DHCP “Option 43”

[Image removed]

WLC SETUP

This helps set up the WLC to allow GUI configuration

[Image removed]

[Image removed]

Why Jeremy chose FRANCE for Country Code (has to do with regulatory domain of equipment)

[Image removed]

[Image removed]

---

ACCESSING THE WLC GUI

[Image removed]

[Image removed]

[Image removed]

[Image removed]

[Image removed]

---

WLC CONFIGURATION

[Image removed]

WLC PORTS

- WLC PORTS are the PHYSICAL PORTS that cables connect to
- WLC INTERFACES are the logical interfaces within the WLC (ie: SVIs on a SWITCH)
- WLCs have a few different PORTS:
    - SERVICE PORT
        - A dedicated MANAGEMENT PORT
        - Used for OUT-OF-BAND management
        - Must connected to a SWITCH ACCESS PORT because it only supports one VLAN
        - This PORT can be used to connect to the DEVICE while it is booting, performing system recovery, etc.
    - DISTRIBUTION SYSTEM PORT
        - These are the standard NETWORK PORTS that connect to the “DISTRIBUTION SYSTEM” (WIRED NETWORK) and are used for DATA traffic.
        - These PORTS usually connect to SWITCH TRUNK PORTS, and if multiple distribution PORTS are used they can form a LAG
    - CONSOLE PORT
        - This is a standard CONSOLE PORT, either RJ45 or USB
    - REDUNDANCY PORT
        - This PORT is used to connect to another WLC to form a HIGH AVAILABILITY (HA) pair

[Image removed]

---

WLC INTERFACES

- MANAGEMENT INTERFACES
    - Used for management traffic such as TELNET, SSH, HTTP, HTTPS, RADIUS authentication, NTP, SYSLOG, etc.
    - CAPWAP TUNNELS are also formed to / from the WLC’s management INTERFACE
- REDUNDANCY MANAGEMENT INTERFACE
    - When TWO WLCs are connected by their REDUNDANCY PORTS, one WLC is “ACTIVE” and the other is “STANDBY”
    - This INTERFACE can be used to connect to and manage the “STANDBY” WLC

- VIRTUAL INTERFACE
    - This INTERFACE is used when communicating with WIRELESS CLIENTS to relay DHCP requests, perform CLIENT WEB AUTHENTICATION, etc.

- SERVICE PORT INTERFACE
    - If the SERVICE PORT is used, this INTERFACE is bound to it and used for OUT-OF-BAND MANAGEMENT

- DYNAMIC INTERFACE
    - These are the INTERFACES used to map a WLAN to a VLAN
    - For example :
        - TRAFFIC from the “INTERNAL” WLAN will be sent to the WIRED NETWORK from the WLCs “INTERNAL” DYNAMIC INTERFACE

---

WLAN CONFIGURATION

Click “NEW”

[Image removed]

Fill in details of the interface and click “APPLY”

[Image removed]

Fill out details (IP, Netmask, Gateway…) and then click “APPLY”

[Image removed]

INTERNAL interface has now been created

[Image removed]

Now, repeat the above steps for the GUEST interface

[Image removed]

Fill out details (IP, Netmask, Gateway…) and then click “APPLY”

[Image removed]

[Image removed]

Now that all the INTERFACES are created, we can start WLAN CONFIGURATION

[Image removed]

[Image removed]

INTERNAL WLAN is set to “MANAGEMENT”, it needs to be changed to “INTERNAL”

[Image removed]

SECURITY will also need to be changed from [WPA2] to [WPA2 PSK]

[Image removed]

(Need to CHECK the PSK “Enable” box at the bottom)

Change the PSK FORMAT to “ASCII” and enter a PASSWORD (at least 8 chars in length)

[Image removed]

[Image removed]

- WEB AUTHENTICATION
    - After the WIRELESS CLIENTS gets an IP ADDRESS and tries to access a WEB PAGE, they will have to enter a USERNAME and PASSWORD to AUTHENTICATE

- WEB PASSTHROUGH
    - Similar to the above, but NO USERNAME or PASSWORD are required
    - A warning or statement is displayed and the CLIENT simply has to agree to gain access to the INTERNET
    
- CONDITIONAL and SPLASH PAGE web redirect options are similar but additionally require 802.1x LAYER 2 AUTHENTICATION

---

QoS

[Image removed]

Default QoS setting is “SILVER” (Best Effort). This can be changed depending on the class of traffic being sent through the WLAN

---

ADVANCED SETTINGS

[Image removed]

[Image removed]

---

CONFIGURING A NEW WLAN (GUEST)

[Image removed]

Change STATUS to “ENABLED” and INTERFACE GROUP to “GUEST”

[Image removed]

[Image removed]

Now, we need to change the SECURITY POLICY to [WPA2][Auth(PSK)]

Returning to MONITORING, we can see the changes we made to the CONFIGURATION

[Image removed]

Current number of CLIENTS is now 0. By connecting to the WLANS, these numbers should change.
To SEE a list of the CLIENTS connected, click the left-hand side “CLIENTS” tab

[Image removed]

[Image removed]

---

ADDTIONAL WLC FEATURES

WIRELESS tab showing a list of the APs currently in the NETWORK

[Image removed]

Clicking on an AP shows information and configuration settings for it

[Image removed]

---

MANAGEMENT tab allows you change the ways you can MANAGE the WLC

Clicking “Mgmt Via Wireless” allows you change if you can access MANAGEMENT via WI-FI

[Image removed]

[Image removed]

---

SECURITY tab can allow us to create ACCESS LISTS

[Image removed]

First, NAME the ACL and what kind of IP ADDRESS it’s for

[Image removed]

CLICK “Add New Rule” to specify the ACL Rules (What traffic can pass)

[Image removed]

[Image removed]

[Image removed]

We now need to APPLY the ACL (just like applying it to an INTERFACE on a ROUTER)

Click “CPU ACL” from the left-hand menu

[Image removed]

Select the new ACL from the pull-down list and then click “APPLY”

[Image removed]

[Image removed]
