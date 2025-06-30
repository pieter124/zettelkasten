2025-06-26 

Tags: [[parallel]] [[programming]]

# **Messages**

**Key Ideas:**
- A message contains a number of elements of some particular datatype.
- MPI datatypes:
	- Basic types.
	- Derived types.
![[Pasted image 20250626115126.png]]

**Point-to-Point Communication**
- Communication between two processes.
- Source process sends message to destination process.
- Communication takes place within a communicator.
- Destination process is identified by its rank in the communicator.

**Point-to-point messaging in MPI**
- Sender calls a $\text{SEND}$ routine.
	- Specifying the data that is to be sent. This is called the *send buffer*.
- Receiver calls a $\text{RECEIVE}$ routine.
	- Specifying where the incoming data should be stored. This is called the *receive buffer*.
- Data goes into the receive buffer.
- Metadata describing message also transferred.
	- This is received into separate storage, this is called the *status*.

**Communication modes**
![[Pasted image 20250626115425.png]]
**MPI Sender Modes**
![[Pasted image 20250626115505.png]]

**Sending a message**
```c
int MPI_Ssend(void* buf, int count, MPI_Datatype datatype, int dest, int tag, MPI_Comm comm);
```
**Receiving a message**
```c
int MPI_Recv(void* buf, int count, MPI_Datatype datatype, int source, int tag, MPI_Comm comm, MPI_Status* status);
```

**Synchronous Blocking Message-Passing**
- Processes synchronise.
- Sender process specifies the synchronous mode.
- Blocking: both processes wait until the transaction has completed.

**For a communication to succeed:**
- Sender must specify a valid destination rank.
- Receiver must specify a valid source rank.
- The communicator must be the same.
- Tags must match.
- Message types must match.
- Receiver's buffer must be large enough.

**Wildcarding**
- Receiver can wildcard.
- To receive from any source $\textbf{MPI\_ANY\_SOURCE}$.
- To receive with any tag $\textbf{MPI\_ANY\_TAG}$.
- Actual source and tag are returned in the receiver's $\textbf{status}$ parameter.

**Message Order Preservation**
- Messages do not overtake each other.
- This is true even for non-synchronous sends.

Deadlock example:
![[Pasted image 20250626122356.png]]

A way around this is using $\text{Bsend}$.
![[Pasted image 20250626122530.png]]

- If a receive matches multiple messages in the "inbox".
	- Then the messages will be received in the order they were sent.
- Only relevant for multiple messages from the same source.

**Timers**
```c
double MPI_Wtime(void);
```
- Time is measured in seconds.
- Time to perform a task is measured by consulting the timer before and after.
	- Subtract values to get elapsed time...

Floating point arithmetic is not associative!!!

Rule of thumb is not to trust any measurement that takes less than a second.


**References**
*EPCC HPC Summer School*
**Lecturers: David Henty****