2025-06-19 

Tags: [[programming]] [[parallel]]

# **Parallel Computing**

**What do we mean by performance?**
*We use FLOPS*
Floating point operations per second.

**Parallel Programming Concepts**
- Decomposition
	- Geometric decomposition
	- Task farm
	- Pipeline
	- Loop parallelism

- Performance metrics and scaling
	- Amdahl's law
	- Gustafson's law

Parallel programming is more difficult than its sequential counterpart.
- Careful thought is required to take advantage of parallel machines

Not all parts of the program can be successfully split up.
Splitting up the program may introduce additional overheads such as communication.

How we split it up is critical:
- Limit communication (especially the number of messages).
- Balance the load so all processors are equally busy.

**Decomposition**

How you split the problem up depends upon a number of factors:
- The nature of the problem.
- The amount of communication required.
- Support from implementation technologies.

Geometric decomposition is the most commonly used.

Splitting up the problem does have an associated cost:
- Namely, the communication between processors.
- Need to carefully consider granularity[^1].
- Aim to minimise communication and maximise computation.

If the chunks are too large, there is too little parallelism. If they are too large, there is too much communication overhead.

**Halo Swapping**
Refers to the exchange of 'boundary' data between neighbouring parallel processes.

- Swap data in bulk at pre-defined intervals.
- Often only need information on the boundaries.
- Many small messages result in far greater overhead.

**Load imbalance**
- Execution time determined by slowest processor.
	- Each processor should roughly have the same amount of work, i.e. they should be load balanced.

- Assign multiple partitions per processor
	- Additional techniques such as work stealing[^2] available.

**Task farm**
- Split the problem up into distinct, independent, tasks
- Controller process sends task to a worker
- Worker process sends results back to the controller
- The number of tasks is often much greater than the number of workers and tasks get allocated to idle workers.

Considerations:
- Communications between the workers can complicate things.
- The controller process can become a bottleneck
	- Workers are idle waiting for the controller to send them a task or acknowledge receipt of results.
	- Potential solution: implement work stealing.

**Pipeline**
- A problem involves operating on many pieces of data in turn. The overall calculation can be viewed as data flowing through a sequence of stages and being operated on at each stage.
- Each stage runs on a processor, each processor communicates with the processor holding the next stage.
- One way flow of data.

**Loop parallelism**
- Serial programs can often be dominated by computationally intensive loops.
- Can be applied incrementally, in small steps based upon a working code.
- Tends to work best with small-scale parallelism.
	- Not suited to all architectures or all loops.
- If the runtime is not dominated by loops, or some loops can not be parallelised then these factors can dominate (Amdahl's law).

A trick for checking if loop parallelism would work is asking the question, "Would the loop yield the expected output if done in reverse?".

**Performance metrics and scaling**
- Measure the execution time $\large{T}$
- Speed up:
	- Typically $S(N, P) \lt P$
	- $\large S(N, P) = \frac{T(N, 1)}{T(N, P)}$

- Parallel efficiency
	- typically $E(N, P) \lt 1$
	- $\large E(N, P) = \frac{S(N, P)}{P} = \frac{T(N, 1)}{PT(N, P)}$

- Serial efficiency
	- typically $E(N) \leq 1$
	- $\large E(N) = \frac{T_{best}(N)}{T(N, 1)}$
Where $N$ is the size of the problem and $P$ the number of processors.

**Scaling**
- Scaling is how the performance of a parallel application changes as the number of processors is increased.

- There are two types of scaling:
	- Strong scaling - total problem size stays the same as the number of processors increases.
	- Weak scaling - the problem size increases at the same rate as the number of processors, keeping the amount of work for each processor the same.
Strong scaling is generally more useful and more difficult to achieve than weak scaling.

*Strong scaling*
![[Pasted image 20250619121345.png]]
*Weak scaling*
![[Pasted image 20250619121401.png]]

*The serial fraction* - an inherent limit to speed up when we parallelise problems.

**Amdahl's law**
A typical program has two categories of components:
- Inherently sequential sections: can't be run in parallel.
- Potentially parallel sections

Assume fraction $\alpha$ is serial and parallel part is $100\%$ efficient.

*Parallel runtime* 
$\large T(N, P) = \alpha T(N, 1) + \frac{(1 - \alpha)T(N, 1)}{P}$

*Parallel speedup*
$\large S(N, P) = \frac{T(N, 1)}{T(N, P)} = \frac{P}{\alpha P + (1 - \alpha)}$

We are fundamentally limited by the serial fraction.

**Gustafson's law**

*We need larger problems for larger number of CPUs.*
Essentially if the problem becomes bigger, the serial problem stays constant but the parallel counterpart increases.

*Assume parallel part is proportional to $N$ and that serial fraction $\alpha$ is independent of $N$.

*Time*
$\large T(N, P) = T_{serial}(N, P) + T_{parallel}(N, P) = \alpha T(1, 1) + \frac{(1 - \alpha)NT(1, 1)}{P}$

*Speedup*
$\large S(N, P) = \frac{T(N, 1)}{T(N, P)} = \frac{\alpha + (1 - \alpha)N}{\alpha + (1 - \alpha)\frac{N}{P}}$

- Scale problem size with CPUs, i.e. set $N = P$ (weak scaling).
	- Speedup: $S(P, P) = \alpha + (1 - \alpha) P$
	- Efficiency: $E(P, P) = \frac{\alpha}{P} + (1 - \alpha)$

If you increase the amount of work done by each parallel task then the serial component will not dominate.
	Increase the problem size to maintain scaling.
	Can do this by adding extra complexity or increasing the overall problem size.

**Load Imbalance**
These laws all assumed all processors are equally busy. But what happens if some run out of work?

Scalability is not everything?
	Make the best use of the processors at hand before increasing the number of processors.

**Quantifying load imbalance**
Define load imbalance factor.

$\large LIF = \text{maximum load / average load}$

For perfectly balanced problems, $LIF = 1.0$, as expected.
	In general, $LIF \gt 0$.

$LIF$ tells you how much faster your calculation could be with balanced load.

**Summary**
Many considerations when parallelising code.
A variety of patterns exist that can provide well known approaches to parallelising a serial problem.

Scaling is important, as the more a code scales, the larger a machine it can take advantage of.
- Can consider weak/strong scaling.
- In practice, overheads limit the scalability of real parallel programs.
- Amdahl's law models these in terms of serial and parallel fractions.
- Larger problems generally scale better, Gustafson's law.

Load balance is a crucial factor.
Metrics exist to give you an indication of how well your code performs and scales.



**Further Reading**
*Using OpenMP : Portable Shared Memory Parallel Programming*

**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**

[^1]: Size of chunks of work

[^2]: Scheduling strategy for multi-threaded computer programs that solves the problem of executing dynamically multi-threaded computation, one that can "spawn" new threads of execution.
