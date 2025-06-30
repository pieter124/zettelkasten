2025-06-26 

Tags: [[parallel]] [[programming]]

# **Message-Passing Programming Concepts

**Key Ideas:**

**Message Passing Model**
- The message passing model is based on the notion of processes.
	- Can think of a process as an instance of a running program, together with the program's data.
- In the message passing model, parallelism is achieved by having many processes co-operate on the same task.
- Each process has access only to its own data.
	- I.e. all variables are private.
- Processes communicate with each other by sending and receiving messages.
	- Typically library calls from a conventional sequential language.
![[Pasted image 20250626093714.png]]

**Distributed-Memory Architectures**
![[Pasted image 20250626093837.png]]

**Generic Parallel Machine**
- Good conceptual model is collection of multi-core laptops.
	- Connected together by a network.
- Each laptop is called a compute node.
	- Each has its own operating system and network connection.
- Suppose each node is a quad-core laptop.
	- Total system has 20 CPU cores.

**Process Communication**
![[Pasted image 20250626094007.png]]

**Single-Program-Multiple-Data**
- Most message passing programs use the Single-Program-Multiple-Data (SPMD) model.
- All processes run (their own copy of) the same program.
- Each process has a separate copy of the data.
- To make this useful, each process has a unique identifier.
- Processes can follow different control paths through the program, depending on their process ID.
- Usually run one process per processor/core.

**Emulating General Message Passing**
![[Pasted image 20250626094223.png]]

**Messages**
- A message transfers a number of data items of a certain type from the memory of one process to the memory of another process.
- A message typically contains..
	- the ID of the sending processor,
	- the ID of the receiving processor,
	- the type of the data items,
	- the number of data items,
	- the data itself,
	- a message type identifier.

**Communication modes**
- Sending a message can either be synchronous or asynchronous.
- A synchronous send is not completed until the message has started to be received.
- An asynchronous send completes as soon as the message has gone.
- Receives are usually synchronous, the receiving process must wait until the message arrives.

Synchronous send $\approx$ faxing a letter, know when letter has started to be received.
Asynchronous send $\approx$ posting a letter, only know when letter has been posted, not when it has been received.

**Point-to-Point Communications**
- We have considered two processes...
	- One sender.
	- One receiver.
- This is called point-to-point communication.
	- Simplest form of message passing.
	- Relies on matching send and receive.
- Close analogy to sending personal emails.

**Collective Communications**
- A simple message communicates between two processes.
- There are many instances where communication between groups of processes are required.
- Can be built from simple messages, but often implemented separately, for efficiency.
  
**Issues**
- Sends and receives must match..
	- Danger of deadlock,  program will stall (forever!).
- Possible to write very complicated programs, but...
	- Most scientific codes have a simple structure
	- Often results in simple communication patterns.
- Use collective communications where possible.
	- May be implemented in efficient ways.

**Summary**
- Messages are the only form of communication..
	- All communication is therefore explicit.
- Most systems use the SPMD model..
	- All processes run exactly the same code.
	- Each has a unique ID.
	- Processes can take different branches in the same codes.
- Basic communications from is point-to-point..
	- Collective communications implement more complicated patterns that often occur in many codes.
- Message-Passing is a programming model..
	- That is implemented by MPI.
	- The Message-Passing Interface is a library of function/subroutine calls.
- Essential to understand the basic concepts..
	- Private variables.
	- Explicit communications.
	- SPMD.
- Major difficulty is understanding the Message-Passing model.
	- A very different model to sequential programming.


**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**