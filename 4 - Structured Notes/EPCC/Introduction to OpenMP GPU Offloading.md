2025-06-25 

Tags:  [[parallel]] [[programming]] [[gpu]]

# **Introduction to OpenMP GPU Offloading** 

**Key Ideas:**

**OpenMP Device Model**
- Host-centric model with one host device and multiple target devices of the same type.
- A device is a logical execution engine with local storage.
- A device data environment is a data environment associated with a target data or target region.
- $\text{target}$ directives control how data and code are offloaded to devices.
- Data is mapped from a host data environment to a device data environment.

**The Target Region**
- The $\text{target}$ region is the basic offloading mechanism in OpenMP.
	- It defines a section of code, e.g. a loop.
- During execution, when a target construct is encountered, the code it contains is executed on a device.
- By default, the code inside the target construct executes sequentially.
- Meanwhile, the host thread waits for the target region to finish, before executing the remainder of the code.
![[Pasted image 20250625110042.png]]
**Host and Device Data**
- The host and device have separate memory spaces.
- Data declared on the host and accessed within a target region must first be mapped to the device.
- This (in general) makes a copy of the data on the device, but both host and device versions of a variable are referred to by the same name.
- Mapped data must not be accessed by the host until the target region has completed.
- Default behaviour
	- Scalars referenced in the target region are treated as $\text{firstprivate}$.
		- I.e. a scalar is initialised with value on host then copied to device.
	- Static arrays are copied to the device on entry and back to the host on exit.

**Map clause**
How data is mapped to the device is specified via the $\text{map}$ clause on the $\text{target}$ construct.
![[Pasted image 20250625110500.png]]
$\text{map-type}$ can be one of the following,
- $\text{to}$ : copies the data to the device on entry;
- $\text{from}$ : copies the data to the host on exit;
- $\text{tofrom}$ : copies the data to the device on entry and back on exit;
- $\text{alloc}$ : allocates an uninitialised copy on the device (don't copy values);

and $\text{list}$ is simply a list of variables.

Map clause example:
![[Pasted image 20250625110729.png]]

**Parallelism on a Device**

In principle, we can use all the "normal" OpenMP constructs inside a target region to create and use threads on the device.
	Parallel regions, worksharing, synchronisation, tasks, etc.

However, GPUs are not able to support a full threading model outside of a single streaming multiprocessor (NVIDIA) or compute unit (AMD).
- No synchronisation or memory fences possible between SMs.
- No coherency between L1 caches.
- A parallel region inside a target region will only execute on one SM.
- Compare with CUDA - can only synchronise threads inside a thread block, not between thread blocks.

GPU offload with reduction example:
![[Pasted image 20250625111015.png]]
Only one GPU SM/CU utilised!

**Teams Construct**
- Creates multiple master threads inside a target region.
- Each master thread can spawn its own team of threads within separate parallel regions.
- Threads in different teams cannot synchronise with each other.
	- Barriers, critical regions, locks only apply to the threads within a team.
	- Can control the number of teams and the number of threads per team.

Teams and Distribute Construct:
![[Pasted image 20250625111204.png]]
![[Pasted image 20250625111307.png]]
$\textbf{distribute}$ construct: distribute loop iterations across teams.
$\textbf{for} \text{ or } \textbf{do }$construct: further distribute iterations across team threads.

- Each team has its own master thread and runs on a single GPU SM.
- Each team creates a separate parallel region.
	- Typically a thread runs on a single core within GPU SM.
- The number of teams is limited by number of SM/CUs on GPU.
- The number of threads per team depends on number of cores per SM/CU.

**Teams Scheduling**
![[Pasted image 20250625111552.png]]

- Same as schedule clause on worksharing loops, but no dynamic or guided option.
- Iterations grouped into chunks and assigned to teams in a round-robin fashion.
- Number of iterations per chunk can be specified.
- If not specified, chunk size per team is approx. equal.

**Synchronisation**

- All of the "normal" OpenMP synchronisation constructs and routines can be used inside target regions.
- However, most of them, including $\text{barrier, critical}$ and locks only synchronise the threads within a team, and not across different teams.
	- Means that these are of limited use.
- The $\text{atomic}$ construct, on the other hand, which protect concurrent accesses to memory locations, do synchronise across the whole device.
	- Typically, these are efficiently supported by the hardware.

Calling functions inside target regions:
![[Pasted image 20250625111917.png]]

**Runtime Execution Environment Routines**
![[Pasted image 20250625112006.png]]

**Teams Construct Clauses:**
![[Pasted image 20250625114131.png]]

**Further reading (questions & resources):**
*Using OpenMP : Portable Shared Memory Parallel Programming*


**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**
