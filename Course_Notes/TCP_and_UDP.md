# 30. TCP and UDP (LAYER 4 PROTOCOLS)

BASICS OF LAYER 4

- Provides TRANSPARENT transfer of DATA between END HOSTS (Host To Host communication)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- Provides (or DOESN’T provide) various SERVICES to APPLICATIONS:
    - Reliable DATA Transfer
    - Error Recovery
    - Data Sequencing
    - Flow Control
- Provides LAYER 4 ADDRESSING (PORT numbers) - NOT the physical interfaces / ports on network devices
    - IDENTIFY the APPLICATION LAYER protocol
    - Provides SESSION multiplexing

---

WHAT IS A SESSION ? 

- A SESSION is an EXCHANGE of DATA between TWO or MORE communicating DEVICES

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

The FOLLOWING ranges have been designated by IANA (Internet Assigned Numbers Authority) 

- **Well-Known** Port Numbers : 0 - 1023
- **Registered** Port Numbers : 1024 - 49151
- **Ephemeral** / Private / Dynamic port numbers : 49152 - 65535

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

TCP (TRANSMISSION CONTROL PROTOCOL)

- A CONNECTION-ORIENTED protocol
    - Before actually SENDING DATA to the DESTINATION HOST, the TWO HOSTS communicate to establish a CONNECTION. Once the CONNECTION is established, DATA exchange begins.

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Establishing connections

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

Terminating connections

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- TCP provides RELIABLE communication
    - The DESTINATION HOST must acknowledge that it RECEIVED each TCP SEGMENT (Layer 4 PDU)
    - If a SEGMENT isn’t ACKNOWLEDGED, it is sent again
    

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- TCP provides SEQUENCING
    - SEQUENCE numbers in the TCP HEADER allow DESTINATION HOSTS to put SEGMENTS in the correct ORDER even if they arrive out of ORDER

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- TCP provides FLOW CONTROL
    - The DESTINATION HOST can tell the SOURCE HOST to increase / decrease the RATE that DATA is sent

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

UDP (USER DATAGRAM PROTOCOL)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- UDP is NOT a CONNECTION-ORIENTED PROTOCOL
    - The SENDING HOST does NOT establish a CONNECTION with the DESTINATION HOST before sending DATA. The DATA is simply SENT

- UDP DOES NOT provide reliable COMMUNICATION
    - When UDP is used, ACKNOWLEDGEMENTS are NOT SENT for received SEGMENTS
    - If a SEGMENT is LOST, UDP has no mechanism to re-TRASMIT it
    - SEGMENTS are sent “best-effort”
    
- UDP DOES NOT provide SEQUENCING
    - There is NO SEQUENCE NUMBER FIELD in the UDP header
    - If SEGMENTS arrive out of order, UDP has no MECHANISM to put them back in ORDER
    
- UDP DOES NOT provide FLOW CONTROL
    - UDP has NO MECHANISM like TCP’s WINDOW SIZE to control the flow of DATA
    
- UDP DOES provide ERROR CHECKING (via CHECKSUM)

---

COMPARING TCP AND UDP

Number of Fields in their Headers

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- TCP provides MORE FEATURES than UDP but at a COST of ADDITIONAL OVERHEAD
- For applications that require RELIABLE communications (for example, downloading a file), TCP is PREFERRED
- For applications, like real-time voice and video, UDP is preferred
- There are SOME applications that use UDP, but provide RELIABILITY, etc. within the APPLICATION itself.
- Some applications use BOTH TCP and UDP, depending on the situation.

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

IMPORTANT PORT NUMBERS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)
