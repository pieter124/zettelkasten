2025-06-20 

Tags: [[parallel]] [[computer science]]

# **Parallel Models**

**Shared variables**
Threads-based parallelism

**Shared-memory concepts**
Threads can see all data of parent process.
Can run on different cores.

How do threads collaborate?
They work together but do not interfere. They also need private data.

Simplified Model:
![[Pasted image 20250620094340.png]]
**Thread Communication**
Another simplified model:
![[Pasted image 20250620094435.png]]

**Synchronisation**
- Synchronisation crucial for shared variables approach
	Thread 2's code must execute *after* thread 1.
- Most commonly use global barrier synchronisation
	Other mechanisms such as locks are available.
- Writing parallel codes relatively straightforward
	Access shared data as and when its needed.
- Getting the correct code can be difficult!

If they added one to $asum$ at the same time, it will update the old values. Most of the time you will get the expected value however you need to make sure one thread executes and writes back before the other thread reads, executes and writes back.

Specific example:
![[Pasted image 20250620094651.png]]

**Reductions**
A *reduction* produces a single value from associative operations such as addition, multiplication, max, min, and, or.

Only one thread at a time updating $asum$ removes all parallelism.
	Each thread accumulates own private copy; copies reduced to give final result.
	If the number of operations is much larger than the number of threads, most of the operations can proceed in parallel.

**Threads in HPC**
For parallel computing
- Typically run a single thread per core.
- Want them all to run all the time.
OS optimisations
- Place threads on selected cores.
- Stop them from migrating.

**Practicalities**
Threading can only operate within a single node.
- Each node is a shared-memory computer.
- Controlled by a single operating system.

Simple parallelisation
- Speed up a serial program using threads.
- Run an independent program per node (e.g. a simple task farm).

More complicated
- Use multiple processes (e.g. message passing - next).

**Message Passing**
Process-based parallelism

**Process communication**
Simplified model:
![[Pasted image 20250620100515.png]]
**Synchronisation**
Synchronisation is automatic in message-passing.
- The messages do it for you.
No danger of corrupting someone else's data.

**Communication nodes**
Sending a message can either be synchronous or asynchronous.
A synchronous send is not completed until the message has started to be received.
An asynchronous send completes as soon as the message has gone.
Receives are usually synchronous - the receiving process must wait until the message arrives.

**Message Passing: Collective Communications**
Process-based parallelism

Broadcast:
One-to-all communication. (From one process to all others).

Scatter:
Information scattered to many processes.

Gather:
Information gathered onto one process.

Reduction operations:
Combine data from several processes to form a single result.

**Hardware**
Natural map to distributed memory.
- One process per processor-core.
- Messages go over the interconnect, between nodes/OS's.

**Processes: Summary**
- Processes cannot share memory.
	- Ring-fenced from each other (virtual memory space....).
- Communication requires explicit messages. 
- Almost exclusively use message-passing interface.
	- MPI is a library of function calls / subroutines.

**Message passing on shared memory**
- Run one process per core.
	- Do not directly exploit shared memory.
	- Works well in practice!
- Message-passing programs run by a special job launcher.
	- User specifies #$\text{copies.}$
	- Some control over allocation to nodes.

**Summary**
- Shared-variables parallelism
	- Uses threads.
	- Requires shared-memory machine.
	- Easy to implement, but limited scalability.
	- On HPC, done using OpenMP compilers.

- Distributed memory.
	- Uses processes.
	- Can run on any machine: messages can go over the interconnect.
	- Harder to implement, but better scalability.
	- On HPC, done using the MPI library.


**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**
