# 43. FTP and TFTP

THE PURPOSE OF FTP / TFTP

- FTP (File Transfer Protocol) and TFTP (Trivial File Transfer Protocol) are INDUSTRY STANDARD PROTOCOLS used to TRANSFER FILES over a NETWORK
- They BOTH use a CLIENT-SERVER model
    - CLIENTS can use FTP / TFTP to COPY files FROM a SERVER
    - CLIENTS can use FTP / TFTP to COPY files TO a SERVER
- As a NETWORK ENGINEER, the most common use for FTP / TFTP is in the process of UPGRADING the OPERATING SYSTEM of a NETWORK DEVICE
- You can use FTP / TFTP to DOWNLOAD the newer version of IOS from a SERVER and then REBOOT the DEVICE with the new IOS image

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

TFTP and FTP FUNCTIONS AND DIFFERENCES

TFTP

- TFTP first standardized in 1981
- Named “Trivial” because it’s SIMPLE and has only basic features compared to FTP
    - Only allows a CLIENT to COPY FILES to / from a SERVER
- Was released after FTP, but not a REPLACEMENT for FTP.
    - It’s another tool to use when LIGHTWEIGHT SIMPLICITY is more important than FUNCTIONALITY
- NO AUTHENTICATION (Username / Password) so SERVERS will respond to ALL FTP REQUESTS
- NO ENCRYPTION. All DATA is sent PLAIN TEXT
- Best used in a CONTROLLED environment to transfer SMALL FILES quickly
- TFTP SERVERS listen on UDP PORT 69
- UDP is CONNECTIONLESS and doesn’t provided RELIABILITY with RETRANSMISSIONS
- However, TFTP has SIMILAR built-in FEATURES within the PROTOCOL itself

TFTP RELIABILITY

- Every TFTP DATA message is ACKNOWLEDGED
    - If the CLIENT is transferring a FILE TO the SERVER, the SERVER will send ACK messages
    - If the SERVER is transferring a FILE TO the CLIENT, the CLIENT will send ACK messages
- TIMERS are used, and if an EXPECTED message isn’t received in time, the waiting DEVICE will RESEND its previous message.

📊 **[Diagram]** - *Network diagram illustrating the concept*

TFTP “CONNECTIONS”

📊 **[Diagram]** - *Network diagram illustrating the concept*

TFTP TID (Not in the CCNA exam)

- When the CLIENT sends the FIRST message to the SERVER, the DESTINATION PORT is UDP 69 and the SOURCE PORT is a random EPHEMERAL PORT
- This “random port” is called a “TRANSFER IDENTIFIER” (TID) and identifies the DATA TRANSFER
- The SERVER then also selects a RANDOM TID to use as a SOURCE PORT when it replies, NOT UDP 69
- When the CLIENT sends the NEXT message, the DESTINATION PORT will be the SERVER’S TID, NOT UDP 69

UDP PORT 69 (TFTP) is only used at the initial request message

📊 **[Diagram]** - *Network diagram illustrating the concept*

--- 

FTP

- FTP was first standardized in 1971
- FTP uses TCP PORTS 20 and 21
- USERNAMES and PASSWORDS are used for AUTHENTICATION, however there is NO ENCRYPTION
- For GREATER security, FTPS (FTP over SSL / TLS) can be used (Upgrade to FTP)
- SSH File Transfer Protocol (SFTP) can also be used for GREATER security (New Protocol)
- FTP is MORE complex than TFTP and ALLOWS not only FILE TRANSFERS but CLIENTS can also:
    - Navigate FILE DIRECTORIES
    - ADD / REMOVE FILES
    - LIST FILES
    - etc…
- The CLIENT sends FTP *commands* to the SERVER to perform these functions

FTP CONTROL CONNECTIONS

- FTP uses TWO TYPES of connections:
    - An FTP CONTROL connection (TCP 21) is established and used to send FTP commands and replies
    - When FILES or DATA are to be transferred, separate FTP DATA (TCP 20) connections are established and terminated as needed

📊 **[Diagram]** - *Network diagram illustrating the concept*

ACTIVE MODE FTP DATA CONNECTIONS

- The DEFAULT method of establishing FTP DATA connections is ACTIVE MODE in which the SERVER initiates the TCP connection.

📊 **[Diagram]** - *Network diagram illustrating the concept*

- In FTP PASSIVE MODE, the CLIENT initiates the DATA connection.
    - This is often necessary when the CLIENT is behind a FIREWALL, which could BLOCK the INCOMING CONNECTION from the SERVER

📊 **[Diagram]** - *Network diagram illustrating the concept*

FTP VERSUS TFTP

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

IOS FILE SYSTEMS

- A FILE SYSTEM is a way of controlling how DATA is STORED and RETRIEVED
- You can VIEW the FILE SYSTEM of a Cisco IOS DEVICE with `show file systems`

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

USING FTP / TFTP IN IOS

- You can VIEW the current version of IOS with `show version`

📊 **[Diagram]** - *Network diagram illustrating the concept*

- You can VIEW the contents of flash with `show flash`

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

COPYING FILES WITH TFTP

STEP 1

📊 **[Diagram]** - *Network diagram illustrating the concept*

STEP 2

📊 **[Diagram]** - *Network diagram illustrating the concept*

STEP 3

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

COPYING FILES WITH FTP

STEP 1

📊 **[Diagram]** - *Network diagram illustrating the concept*

STEP 2 and 3 identical to TFTP above

---

COMMAND SUMMARY

📊 **[Diagram]** - *Network diagram illustrating the concept*
