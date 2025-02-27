# PRAKTIKUM 2 INTRODUCTION CHAPTER

MUHAMMAD SYAHRUL ROMADHON (3124521017) 1 IT A PSDKU LA

1.1	What are the three main purposes of an operating system?
•	Resource Management: Managing hardware resources such as the CPU, memory, and I/O devices.
•	Abstraction: Providing a user-friendly interface for applications and users, so they don’t need to interact directly with the hardware.
•	Protection and Security: Protecting the system and data from unauthorized access or program errors.

1.2	When is it appropriate for the operating system to forsake efficiency and "waste" resources? Why is such a system not really wasteful?
•	Appropriate situations: When the operating system needs to prioritize user convenience, security, or reliability over resource efficiency. For example, the OS might allocate more memory for caching or maintain backup processes to ensure service availability.
•	Not truly wasteful: Resource allocation that appears "wasteful" is actually aimed at improving user experience, system reliability, or security, ultimately providing greater value.

1.3	What is the main difficulty that a programmer must overcome in writing an operating system for a real-time environment?
•	Main difficulty: Ensuring that the operating system can meet strict timing constraints (hard real-time constraints). The system must respond within a very short and predictable time frame, requiring highly efficientscheduling and resource management algorithms.

1.4	Should the operating system include applications such as web browsers and mail programs? Argue both sides.
•	Should include:
•	User convenience: Providing built-in applications like browsers and email makes it easier for users to start using the system without needing to install additional software.
•	Better integration: Built-in applications can be optimized to work better with the operating system.
•	Should not include:
	Flexibility: Users might prefer third-party applications that better suit their needs.
	System size: Including additional applications can make the operating system larger and more complex.

1.5	Bagaimana perbedaan antara mode kernel dan mode pengguna berfungsi sebagai bentuk perlindungan (keamanan) yang mendasar?
•	Mode kernel: Mode ini memiliki akses penuh ke perangkat keras dan dapat menjalankan instruksi berbahaya.
•	Mode pengguna: Mode ini membatasi akses ke perangkat keras dan hanya dapat menjalankan instruksi yang aman.
•	Fungsi perlindungan: Dengan membedakan antara kedua mode ini, sistem operasi dapat mencegah program pengguna dari mengakses atau merusak sumber daya sistem yang kritis.

1.6	Which of the following instructions should be privileged?
•	Set value of timer - Privileged
•	Read the clock - Non-privileged
•	Clear memory - Privileged
•	Issue a trap instruction - Non-privileged
•	Turn off interrupts - Privileged
•	Modify entries in device-status table - Privileged
•	Switch from user to kernel mode - Privileged
•	Access I/O device – Privileged

1.7	Identify two challenges that might occur due to protecting the OS by placing it in a non-modifiable memory partition.
•	Difficulty in updates: If the operating system cannot be altered, it becomes challenging to update or fix existing bugs.
•	Limited flexibility: The operating system may require modifications to respond to specific situations, such as dynamic memory allocation or error handling.

1.8	What are two possible uses of multiple modes of operation in CPUs?
•	Virtualization: Imagine running a whole bunch of virtual machines like a magician pulling rabbits out of hats! Extra modes help keep them nicely isolated—no rabbit mix-ups here!
•	Layered Security: Think of it as a secret agent HQ, where only the elite can access certain information. Different security levels can protect critical applications—because nobody wants their top-secret files to end up in the wrong hands!

1.9	How could timers be used to compute the current time?
•	How it works: Timers are like those friendly reminders you set on your phone! They generate interrupts at regular intervals, like every second. Every time one of these interrupts happens, the operating system adds a tick to its little time counter. So, if your computer was a baker, it would know exactly when to pull that virtual cake out of the oven—calculating the current time like a pro!

1.10	Give two reasons why caches are useful. What problems do they solve? What 
problems do they cause?	
•	Reasons for usefulness:
a.	Speed up acces: caches store frequently accessed data, reducing access time to main memory or secondary storage
b.	Reduce bandwidth load: Caches reduce data traffic between the CPU and main memory

•	Problems solved:
a.	High latency: Caches reduce wait times for accessing data.
b.	Bandwidth bottleneck: Caches reduce data traffic between the CPU and main memory.
•	Problems caused:
a.	Cache coherence: In multiprocessor systems, maintaining consistency of data across different caches can be complex.
b.	Limited size: Caches have limited capacity, requiring efficient replacement algorithms.

1.11	Distinguish between the client-server and peer-to-peer models of distributed systems.
•	Client-Server:
a.	There is a clear division of roles between clients (which request services) and servers (which provide services).
b.	Servers are typically more powerful and responsible for storing data and running applications.
c.	Example: Web servers and database servers.
•	Peer-to-Peer (P2P):
a.	All nodes in the system have equal roles and can act as both clients and servers.
b.	There is no central server, making the system more distributed.
c.	Example: File sharing like BitTorrent or VoIP applications like Skype.

1.12	How do clustered systems differ from multiprocessor systems? What is required for two machines belonging to a cluster to cooperate to provide a highly available service?
•	Differences:
a.	Multiprocessor systems: Multiple processors share the same memory and bus, working within a single integrated system.
b.	Clustered systems: Multiple independent systems (nodes) work together over a network, typically without sharing physical memory.
•	Requirements for cooperation:
a.	Clustering software: Software that manages failover and load balancing between nodes.
b.	Shared storage: Storage accessible by all nodes in the cluster.
c.	Reliable network: A fast and reliable network for communication between nodes.

1.13	Consider a computing cluster consisting of two nodes running a database. Describe two ways in which the cluster software can manage access to the data on the disk. Discuss the benefits and disadvantages of each.
•	Shared Disk:
a.	How it works: Both nodes access the same disk directly.
b.	Benefits: Simple and allows direct access to data.
c.	Disadvantages: Risk of bottleneck and access conflicts on the disk.
•	Data Replication:
a.	How it works: Data is replicated on both nodes, so each node has its own copy of the data.
b.	Benefits: Improves access speed and data availability.
c.	Disadvantages: Requires complex data synchronization and additional memory.

1.14	What is the purpose of interrupts? How does an interrupt differ from a trap? Can traps be generated intentionally by a user program? If so, for what purpose?
•	Purpose of interrupts: To notify the CPU that an important event has occurred, such as the completion of an I/O operation or a hardware error.
•	Difference between interrupt and trap:
a.	Interrupt: Generated by hardware (e.g., I/O devices).
b.	Trap: Generated by software (e.g., errors or system calls).
•	Traps generated by user programs: Yes, user programs can intentionally generate traps to invoke operating system services (system calls).


1.15	Explain how the Linux kernel variables HZ and jiffies can be used to determine the number of seconds the system has been running since it was booted.
•	HZ: The frequency of timer interrupts per second (e.g., 250 interrupts per second).
•	jiffies: A counter that records the number of timer interrupts since the system was booted.
•	How to calculate time:
Time (seconds)=jiffies/HZ

Example: If HZ = 250 and jiffies = 75000, then the system has been running for:

75000/250=300 seconds.

1.16	Direct memory access is used for high-speed I/O devices in order to avoid increasing the CPU's execution load.
•	How does the CPU interface with the device to coordinate the transfer?
	The CPU initializes the transfer by setting parameters such as memory address and data size in the DMA controller. After that, the DMA controller takes over the data transfer.
•	How does the CPU know when the memory operations are complete?
	The DMA controller sends an interrupt to the CPU once the transfer is complete.
•	Does this process interfere with the execution of the user programs? If so, describe what forms of interference are caused.
	Yes, DMA can interfere with user program execution because the DMA controller competes with the CPU for memory access, which can cause delays (latency).

1.17	Some computer systems do not provide a privileged mode of operation in hardware. Is it possible to construct a secure operating system for these computer systems? Give arguments both that it is and that it is not possible.
•	Possible:
The operating system can use techniques like sandboxing or virtualization to isolate processes and restrict access to resources.
•	Not possible:
Without hardware support for privileged mode, it is difficult to fully prevent user programs from accessing or damaging system resources.

1.18	Why are caching systems designed with different levels of caches (local and shared)?
•	Local cache: Fast and efficient for individual cores, reducing data access latency.
•	Shared cache: Allows data sharing between cores, reducing data duplication and improving cache coherence.

1.19	Rank the following storage systems from slowest to fastest:
•	Magnetic tapes (slowest)
•	Optical disk
•	Hard-disk drives
•	Nonvolatile memory
•	Main memory
•	Cache
•	Registers (fastest)


1.20	Consider an SMP system similar to the one shown in Figure 1.8. Illustrate with an example how data residing in memory could in fact have a different value in each of the local caches.
•	Example: If two cores access and modify the same variable simultaneously, the value of that variable could differ in each core's local cache until the cache coherency system updates the value."

1.21	Discuss, with examples, how the problem of maintaining coherence of cached data manifests itself in the following processing environments:
•	Single-processor systems:
Cache coherence issues are rare because there is only one cache.
•	Multiprocessor systems:
Different cores may have different copies of data in their local caches, requiring cache coherence protocols like MESI.
•	Distributed systems:
Data replicated across multiple nodes may become inconsistent, requiring synchronization mechanisms like consensus algorithms.
1.22	Describe a mechanism for enforcing memory protection in order to prevent a program from modifying the memory associated with other programs.
•	Mechanism: Use a Memory Management Unit (MMU) to map virtual memory addresses to physical addresses and restrict access to specific memory areas based on mode (user/kernel) and permissions (read/write/execute).

1.23	Which network configuration—LAN or WAN—would best suit the following environments?
•	A campus student union - LAN
•	Several campus locations across a statewide university system - WAN
•	A neighborhood – LAN

1.24	Describe some of the challenges of designing operating systems for mobile devices compared with designing operating systems for traditional PCs.
•	Challenges:
	Power limitations: The OS must be efficient in battery usage.
	Small screen size: The user interface must be optimized for small screens.
	Connectivity: Must support various types of networks (Wi-Fi, cellular).
	Security: Tighter data protection due to the risk of device loss or theft.

1.25	What are some advantages of peer-to-peer systems over client-server systems?
•	Advantages:
	Scalability: Easier to add new nodes.
	Resilience: No single point of failure.
	Cost-effectiveness: No need for expensive central servers

1.26	Describe some distributed applications that would be appropriate for a peer-to-peer system.
•	Applications:
	File sharing: Like BitTorrent.
	VoIP: Like Skype.
	Blockchain: Like Bitcoin.

1.27	Identify several advantages and several disadvantages of open-source operating systems. Identify the types of people who would find each aspect to be an advantage or a disadvantage.
•	Advantages:
	Flexibility: Developers can modify the code as needed.
	Transparency: Open code allows for security audits.
•	Disadvantages:
	Limited support: There is not always official support.
	Complexity: Requires technical knowledge to modify.
•	People who benefit:
	Developers, researchers, and organizations needing customization.
•	People who are disadvantaged:
	Average users who need easy-to-use and fully supported systems.


