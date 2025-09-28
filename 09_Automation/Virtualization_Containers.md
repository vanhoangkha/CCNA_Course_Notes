# 54. VIRTUALIZATION (CONTAINERS): PART 2

REVIEW OF VIRTUAL MACHINES (TYPE 1 and TYPE2 HYPERVISORS)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- VIRTUAL MACHINES (VMs) allow multiple OS’s to run on a single PHYISCAL SERVER
- A HYPERVISOR is used to manage and allocate HARDWARE RESOURCES to each VM
    - TYPE 1 HYPERVISORS (aka NATIVE or BARE-METAL) run directly on top of HARDWARE
    - TYPE 2 HYPERVISORS (aka HOSTED) run on top of a HOST OS (ie: WINDOWS)
- TYPE 1 HYPERVISORS are widely used in DATA CENTER ENVIRONMENTS
- TYPE 2 HYPERVISORS are commonly used on personal DEVICES
    - Running a virtual network lab on your PC using Cisco Modeling Labs (CML)

- The OS in each VM can be the same or different (Windows, Linux, MacOS, etc)
- *Bins / Libs* are the SOFTWARE libraries / services needed by the Apps running in each VM
- A VM allows it’s app / apps to run in an ISOLATED environment, separate from the apps in other VMs.
- VMs are easy to create, delete, move, etc.
    - A VM can be easily saved and moved between different physical SERVERS.

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

CONTAINERS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- CONTAINERS are software packages that contain an APP and all dependencies (*Bins/Libs* in the diagram) for the contained APP to run.
    - Multiple APPS can be run in a single CONTAINER, but this is not how CONTAINERS are usually used
- CONTAINERS run on a CONTAINER ENGINE (ie: DOCKER ENGINE)
    - The CONTAINER ENGINE is run on a HOST OS (usually LINUX)
- CONTAINERS are lightweight (small in size) and include only the dependencies required to run the specific APP
- A CONTAINER ORCHESTRATOR is a software platform for automating the DEPLOYMENT, MANAGEMENT, SCALING, etc of CONTAINERS
    - KUBERNETES (originally design by Google) is the most popular CONTAINER ORCHESTRATOR
    - DOCKER SWARM is DOCKER’S CONTAINER ORCHESTRATION tool
- In small numbers, MANUAL operation is possible, but large-scale systems (ie: with Microservices) can require THOUSANDS of CONTAINERS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

---

VIRTUAL MACHINES vs. CONTAINERS

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)

- VMs can TAKE MINUTES to boot up as each VM runs it’s own OS
- CONTAINERS can boot up in milliseconds

- VMs take MORE disk space (Gigabytes)
- CONTAINERS take up VERY LITTLE disk space (Megabytes)

- VMs use MORE CPU/RAM resources (each VM must run its own OS)
- CONTAINERS use FEWER CPU/RAM resources (shared OS)

- VMs are PORTABLE and can MOVE between physical systems running the same HYPERVISOR
- CONTAINERS are MORE portable; they are SMALLER, FASTER to boot up, and DOCKER CONTAINERS can be run on nearly ANY CONTAINER SERVICE

- VMs are more isolated because each VM runs it’s own OS
- CONTAINERS are less isolated because they all run on the same OS; if the OS crashes, all CONTAINERS running on it are effected

![image](https://github.com/vanhoangkha/CCNA_Course_Notes/assets/images/placeholder.png)
