2025-06-25 

Tags: [[programming]] [[gpu]] [[computer science]] 

# **GPU Architectures** 

**Key Ideas:**
Let us review the factors that affect the performance of processing speeds:
- Clock speed: the rate of issue of instructions by the processor.
- Memory latency: time taken to retrieve a data item from memory.
- Memory bandwidth: amount of data transferred in unit time.
- Parallelism: can I replicate the basic processing unit?

**CPU vs GPU Hardware**
Simplified model:
![[Pasted image 20250625093857.png]]
- CPU computational units are "bigger" but smaller in number.
- CPU cores are faster and "smarter" than a GPU core.
	- E.g. out-of-order executions[^1], branch prediction[^2], speculative execution[^3].
- GPUs specialise in floating point operations:
	- E.g. multiply-add, fused multiply-add, tensor core, ray tracing core.
- GPUs have high bandwidth, but high latency.
- Hide latency with multiple threads and fast switching contexts.
	- more software threads than physical cores.

**Single Instruction Multiple Data (SIMD)**
- All the GPU cores execute exactly the same operation, but over different data.
- Rather than $\text{N}$ clock steps to process $\text{N}$ data points, $\text{N}$ compute units process $\text{N}$ data points in a single clock step (if sufficient cores).

**Threads, blocks, and wraps**
- Thread - item of work (i.e. a data point)
	- A thread is executed by a CUDA core (Nvidia) or Stream Processor (AMD).
- Block (Nvidia) / Workgroup (AMD) - collection of threads.
- Blocks/workgroups are assigned to SMs (Nvidia) or CUs (AMD). 
- Threads execute in warps (Nvidia - 32 threads) or wavefronts (AMD - 64 threads).

**Memory hierarchy**
Model example:
![[Pasted image 20250625100432.png]]
**Registers:**
- Private to each thread - used to store local variables and intermediate results.
- Each thread has access to a set number of registers.
- If a kernel requires too many registers, it will utilise a portion of (slower) global memory as a local memory cache/scratchpad.

**L1 Cache / Shared memory:**
- Physical L1 cache resource is shared between blocks/workgroups on a given SM/CU.
- Shared memory is shared between threads in the same block/workgroup.

**Read-only memory:**
- Each SM/CU has memory which is read-only to execute kernel code.
- It may be used as an instruction cache, constant memory, texture memory, RO cache, etc.

**L2 Cache:**
- Shared across all SMs/CUs.
- Hardware-managed cache that stores frequently accessed data to reduce memory latency.

**Global memory:**
- Accessible by all threads, but access is relatively slow.
- Primary storage for input data, output data, and global constants.

**Host Device Picture**
![[Pasted image 20250625102739.png]]

**Unified Memory:**

**Gracehopper**
![[Pasted image 20250625102811.png]]

- No longer need to move data between host and device.
- However, does not guarantee equal latency or bandwidth across the whole memory space. 
- Location of your data (i.e. host and device) is still important...

**Summary**
- Potentially separate CPU and GPU address spaces.
	- Very high bandwidth between GPU and memory.
- Processing power comes from many thousands of CUDA cores / Stream Processors.
	- Each is a separate thread.
- Threads operate in a SIMD / vector fashion.
	- 32-thread warps (NVIDIA) or 64-thread wavefronts (AMD).

**Further reading (questions & resources):**
*Using OpenMP : Portable Shared Memory Parallel Programming*


**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**

[^1]: also known as dynamic execution, is a technique in computer architecture where a processor executes instructions in an order different from the one specified in the program's code. It is done to minimize delays caused by dependencies between instructions and to maximise the utilization of processing units.

[^2]: a technique used in computer architecture used to guess the outcome of conditional branch instructions, improving performance by reducing delays in the instruction pipeline.

[^3]: a technique in computer architecture that boosts performance by executing instructions before it's certain its needed.