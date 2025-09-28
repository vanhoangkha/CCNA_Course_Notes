# 54. VIRTUALIZATION (VRF): PART 3

INTRO TO VRF

📊 **[Diagram]** - *Network diagram illustrating the concept*

- VIRTUAL ROUTING AND FORWARDING (VRF) is used to DIVIDE a SINGLE ROUTER into MULTIPLE VIRTUAL ROUTERS
    - Similar to how VLANs are used to divide a SINGLE SWITCH (LAN) into MULTIPLE VIRTUAL SWITCHES (VLANs)
- It does this by allowing a ROUTER to build MULTIPLE SEPARATE ROUTING TABLES
    - INTERFACES (LAYER 3 only) and ROUTERS are configured to be in a specific VRF (aka *VRF INSTANCE*)
    - ROUTER INTERFACES, SVIs and ROUTED PORTS on MULTILAYER SWITCHES can be configured in a VRF
- TRAFFIC in one VRF cannot be forwarded out of an INTERFACE in another VRF
    - As an exception, VRF LEAKING can be configured to allow traffic to pass BETWEEN VRFs
- VRF is commonly used to facilitate MPLS (Multiple Protocol Label Switching)
    - The kind of VRF we are talking about is VRF-Lite (VRF without MPLS)
- VRF is commonly used by SERVICE PROVIDERS to allow ONE DEVICE to carry traffic from MULTIPLE CUSTOMERS
    - Each CUSTOMER’S TRAFFIC is isolated from the OUTSIDE
    - CUSTOMER IP ADDRESSES can overlap without issue

VRF CONFIGURATION

📊 **[Diagram]** - *Network diagram illustrating the concept*

Creation and Configuration of VRFs

📊 **[Diagram]** - *Network diagram illustrating the concept*

How to `show ip route` for VRFs

📊 **[Diagram]** - *Network diagram illustrating the concept*

`ping` other VRFs

📊 **[Diagram]** - *Network diagram illustrating the concept*
