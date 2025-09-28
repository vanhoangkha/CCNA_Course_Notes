# 49. PORT SECURITY

INTRO TO PORT SECURITY

- PORT SECURITY is a security feature of Cisco SWITCHES
- It allows you to control WHICH SOURCE MAC ADDRESS(ES) are allowed to enter the SWITCHPORT
- If an unauthorized SOURCE MAC ADDRESS enters the PORT, an ACTION will be TAKEN
    - The DEFAULT action is to place the INTERFACE in an “err-disabled” state

📊 **[Diagram]** - *Network diagram illustrating the concept*

- When you enable PORT SECURITY on an INTERFACE with the DEFAULT settings, one MAC ADDRESS is allowed
    - You can configure the ALLOWED MAC ADDRESS manually
    - If you DO NOT configure it manually, the SWITCH will allow the first SOURCE MAC ADDRESS that enters the INTERFACE
- You can CHANGE the MAXIMUM number of MAC ADDRESSES allowed
- A COMBINATION of manually configured MAC ADDRESSES and DYNAMICALLY LEARNED ADDRESSES is possible

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

WHY USE PORT SECURITY?

- PORT SECURITY allows NETWORK admins to control which DEVICES are allowed to access the NETWORK
- However, MAC ADDRESS SPOOFING is a simple task
    - It is easy to configure a DEVICE to send FRAMES with a different SOURCE MAC ADDRESS
- Rather than manually specifying the MAC ADDRESSES allowed on each PORT, PORT SECURITY’S ability to limit the number of MAC ADDRESSES allowed on an INTERFACE is more useful
- Think of the DHCP STARVATION ATTACK (DAY 48 LAB video)
    - The ATTACKER spoofed thousands of fake MAC ADDRESSES
    - The DHCP SERVER assigned IP ADDRESSES to these fake MAC ADDRESSES, exhausting the DHCP POOL
    - The SWITCH’S MAC ADDRESS table can also become full due to such an attack
- Limiting the NUMBER of MAC ADDRESSES on an INTERFACE can protect against those attacks

ENABLING PORT SECURITY

📊 **[Diagram]** - *Network diagram illustrating the concept*

`show port-security interface`

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

RE-ENABLING AN INTERFACE (MANUALLY)

📊 **[Diagram]** - *Network diagram illustrating the concept*

RE-ENABLING AN INTERFACE (ERR-DISABLE RECOVERY)

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

VIOLATION MODES

- There are THREE DIFFERENT VIOLATION MODES that determine what the SWITCH will do if an unauthorized FRAME enters an INTERFACE configured with PORT SECURITY
    - SHUTDOWN
        - Effectively shuts down the PORT by placing it in an ‘err-disabled` state
        - Generates a SYSLOG and / or SNMP message when the INTERFACE is ‘disabled’
        - The VIOLATION counter is set to 1 when the INTERFACE is ‘disabled’
    - RESTRICT
        - The SWITCH discards traffic from unauthorized MAC ADDRESSES
        - The INTERFACE is NOT disabled
        - Generates a SYSLOG and / or SNMP message each time an unauthorized MAC is detected
        - The VIOLATION counter is incremented by 1 for each unauthorized FRAME
    
    - PROTECT
        - The SWITCH discards traffic from unauthorized MAC ADDRESSES
        - The INTERFACE is NOT disabled
        - It does NOT generate a SYSLOG / SNMP message for unauthorized traffic
        - It does NOT increment the VIOLATION counter
    
---

VIOLATION MODE - RESTRICT

📊 **[Diagram]** - *Network diagram illustrating the concept*


VIOLATION MODE - PROTECT

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

SECURE MAC ADDRESS AGING

📊 **[Diagram]** - *Network diagram illustrating the concept*

- By DEFAULT, SECURE MAC ADDRESSES will not ‘age out’ (Aging Time : 0 mins)
    - Can be configured with `switchport port-security aging time *minutes*`

- The DEFAULT Aging Type is ABSOLUTE
    - ABSOLUTE
        - After the SECURE MAC ADDRESS is learned, the AGING TIMER starts and the MAC is removed after the TIMER expires, even if the SWITCH continues receiving FRAMES from that SOURCE MAC ADDRESS.
    - INACTIVITY
        - After the SECURE MAC ADDRESS is learned, the AGING TIMER starts but is RESET every time a FRAME from that SOURCE MAC ADDRESS is received on the INTERFACE
            - Aging type is configured with:  `switchport port-security aging type {absolute | inactivity}`
- Secure Static MAC AGING (address configured with `switchport port-security mac-address x.x.x`) is DISABLED by DEFAULT

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

STICKY SECURE MAC ADDRESSES 

- ‘STICKY’ SECURE MAC ADDRESS learning can be enabled with the following command:
    - `SW(config-if)# switchport port-security mac-address sticky`

- When enabled, dynamically-learned SECURE MAC ADDRESSES will be added to the running configuration, like this:
    - `switchport port-security mac-address sticky *mac-address*`

- The ‘STICKY’ SECURE MAC ADDRESSES will NEVER age out
    - You need to SAVE the `running-config` to `startup-config` to make them TRULY permanent (or else they will not be kept if the SWITCH restarts)
- When you issue the `switchport port-security mac-address sticky` command, all current dynamically-learned secure MAC addresses will be converted to STICKY SECURE MAC ADDRESSES
- If you issue the `no switchport port-security mac-address sticky` command, all current STICKY SECURE MAC ADDRESSES will be converted to regular dynamically-learned SECURE MAC ADDRESSES

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

MAC ADDRESS TABLE

- SECURE MAC ADDRESSES will be added to the MAC ADDRESS TABLE like any other MAC ADDRESS
    - STICKY and STATIC SECURE MAC ADDRESSES will have a type of STATIC
    - Dynamically-Learned SECURE MAC ADDRESSES will have a type of DYNAMIC
    - You can view all SECURE MAC ADDRESSES with `show mac address-table secure`
    

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

COMMAND REVIEW

📊 **[Diagram]** - *Network diagram illustrating the concept*
