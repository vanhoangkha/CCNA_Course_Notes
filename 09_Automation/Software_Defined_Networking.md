# 62. SOFTWARE DEFINED NETWORKING (SDN)

SD REVIEW

- SOFTWARE DEFINED NETWORKING (SDN) is an approach to networking that centralizes the control plane into an application called a *controller*
- Traditional control planes use a distributed architecture
- A SDN controller centralizes control plane functions like calculating routes
- The controller can interact programmatically with the network devices using APIs
- The SBI (South Bound Interface) is used for communications between the controller and the network device it controls
- The NBI (North Bound Interface) is what allows us to interact with the controller with our scripts and applications

SDN ARCHITECTURE

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

CISCO SD-ACCESS

- Cisco SD-ACCESS is Cisco’s SDN solution for automating campus LANs
    - ACI (Application Centric Infrastructure) is their SDN solution for automating data center networks
    - SD-WAN is their SDN solution for automating WANs
- Cisco DNA (Digital Network Architecture) Center is the controller at the center of SD-Access

📊 **[Diagram]** - *Network diagram illustrating the concept*

- The UNDERLAY is the underlying physical network of devices and connections (including wired and wireless) which provide IP connectivity (ie: using IS-IS)
    - Multilayer Switches and their connections

📊 **[Diagram]** - *Network diagram illustrating the concept*

- The OVERLAY is the virtual network built on top of the physical underlay network

📊 **[Diagram]** - *Network diagram illustrating the concept*

- The FABRIC is the combination of the OVERLAY and UNDERLAY; the physical and virtual network as a whole

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

SD-ACCESS UNDERLAY

- The UNDERLAY’s purpose is to support the VXLAN tunnels of the OVERLAY
- There are THREE different ROLES for switches in SD-ACCESS:
    - EDGE NODES : Connect to End HOSTS
    - BORDER NODES : Connect to devices outside of the SD-ACCESS Domain ; ie: WAN routers
    - CONTROL NODES : Uses LISP (Locator ID Separation Protocol) to perform various control plane functions
    
- You can add SD-ACCESS on top of the existing network (*brownfield deployment*) if your network hardware and software supports it
    - Google ‘Cisco SD-ACCESS compatibility matrix’ if you are curious
    - In this case DNA CENTER won’t configure the UNDERLAY

- A NEW deployment (*greenfield deployment)* will be configured by DNA CENTER to use the optimal SD-ACCESS UNDERLAY:
    - ALL Switches are LAYER 3 and use IS-IS as their ROUTING PROTOCOL
    - All Links between Switches are ROUTED PORTS. This means STP is not needed
    - EDGE NODES (ACCESS SWITCHES) act as the the DEFAULT GATEWAY of END HOSTS *(Routed Access Layer)*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

SD-ACCESS OVERLAY

- LISP (Locator ID Separation Protocol) provides the control plane of SD-ACCESS
    - A list of mappings of EIDs (endpoint identifiers) to RLOCs (routing locators) is kept
    - EIDs identify END HOSTS connected to EDGE SWITCHES
    - RLOCS identify the EDGE SWITCH which can be used to reach the END HOST
    - There is a LOT more detail to cover about LISP but I think you can see how it differs from traditional CONTROL PLANE
    
- Cisco TrustSec (CTS) provides policy control (QoS, Security Policy, etc.)

- VXLAN provides the DATA PLANE of SD-ACCESS

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

CISCO DNA CENTER

- Cisco DNA Center has TWO MAIN ROLES:
    - The SDN Controller in SD-ACCESS
    - A network manager in a traditional network (non-SD-ACCESS)
- DNA Center is an application installed on Cisco UCS server hardware
- It has a REST API which can be used to interact with DNA Center
- The SBI supports protocols such as NETCONF and RESTCONF (as well as traditional protocols like Telnet, SSH, and SNMP)
- DNA Center enables *Intent-Based Networking* (IBN)
    - The goal is to allow the engineer to communicate their intent for network behavior to DNA Center, and then DNA Center will take care of the details of the actual configurations and policies on devices

- Traditional security policies using ACLs can become VERY cumbersome
    - ACLs can have thousands of entries
    - The intent of entries is forgotten with time and as engineers leave and new engineers take over

- DNA Center allows the engineer to specify the intent of the policy
    - Examples :
        - THIS group of users can’t communicate with THAT group
        - THIS group can access THIS server but not THAT server
    - DNA CENTER will take care of the exact details of implementing this policy

📊 **[Diagram]** - *Network diagram illustrating the concept*

---

>For more details, you can check out [sandboxdnac.cisco.com](http://sandboxdnac.cisco.com) (User: devnetuser, Password: Cisco123!)

---

DNA CENTER NETWORK MANAGEMENT VS. TRADITIONAL

Traditional Management :

- DEVICES are configured one-by-one via SSH or Console connection
- DEVICES are manually configured via Console connection before being deployed
- Configurations and polices are managed per-device
- New network deployments can take a long time due to the manual labor required
- Errors and failures are more likely due to increased manual effort

DNA CENTER-based Network Management :

- DEVICES are centrally managed and monitored from the DNA CENTER GUI or other applications using it’s REST API
- The Administrator communicates their intended network behavior to DNA CENTER, which changes those intentions into configurations on the managed network devices
- Configurations and policies are centrally managed
- Software versions are also centrally managed. DNA CENTER can monitor cloud servers for new versions and then update the managed devices
- New network deployments are much quicker. New devices can automatically receive their configurations from DNA CENTER without manual configuration

📊 **[Diagram]** - *Network diagram illustrating the concept*
