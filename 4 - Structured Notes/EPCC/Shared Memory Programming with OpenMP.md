2025-06-23 

Tags:  

# **Shared Memory Programming with OpenMP** 

Parallel programming is conceptually hard...

**Key Ideas:**

Need to consider timing, of what could be happening at the same time. It is not as simultaneous as hardware. 
Parallel programming can be non-deterministic due to race conditions or scheduling variations if not properly synchronised.

**Shared memory systems**

- Threaded programming is most often used on shared memory parallel computers.
- A shared memory computer consists of a number of processing units (CPUs/cores) together with some memory
	- e.g. any multi-core CPU.
	- Also servers/supercomputer nodes with a few multi-core CPUs.
	- Not technically feasible to support shared memory across more than O(1000) cores.
- Key feature of shared memory systems is a **single address space** across the whole memory system.
	- Every CPU/core can read and write all memory locations in the system.
	- One logical memory space.
	- All CPUs/cores refer to a memory location using the same address.
	
Conceptual model:
![[Pasted image 20250623094652.png]]

**Real hardware**
- Real shared memory hardware is more complicated than this...
	- Memory may be split into multiple smaller units.
	- There may be multiple levels of cache memory.
		- Some of these levels may be shared between a subset of processors.
	- The interconnect may have a more complex topology.
- But a single address space is still supported...
	- Hardware complexity can affect performance of programs, but not their correctness.

Real hardware example:
![[Pasted image 20250623094918.png]]

**Threaded Programming Model**
- The programming model for shared memory is based on the notion of threads.
	- Threads are a subset of a process, that carries their own private memory and have a shared memory space with other threads.
- Shared data can be accessed by all threads.
- Private data can only be accessed by the owning thread.
- Different threads can follow different flows of control through the same program.
	- Each thread has its own program counter.
- Usually run one thread per CPU/core
	- But could be more...
	- Can have hardware support for multiple threads per core.

Simplified model example:
![[Pasted image 20250623095134.png]]

**Thread communication**
- In order to have useful parallel programs, threads must be able to exchange data with each other.
- Threads communicate with each other via reading and writing shared data.
	- Thread 1 writes a value to a shared variable A.
	- Thread 2 can then read the value from A.

**Synchronisation**
- By default, threads execute asynchronously[^1].
- Each thread proceeds through program instructions independently of other threads.
- This means we need to ensure that actions on shared variables occur in the correct order: e.g.
	Thread 1 must write variable A before thread 2 reads it, or thread 1 must read variable A before thread 2 writes it.
- Note that updates to shared variables are not atomic (e.g. $a  = a + 1$).
- Requires (at least) 3 instructions: load, add, store.
	Side note, think about every instruction in terms of their assembly counterpart as assembly instructions map one-to-one to their machine code / binary counterpart.
- If two threads try to do this "at the same time", the instructions can be interleaved in time such that one of the updates may get overwritten.

**Race conditions**
- A race condition occurs when multiple threads access the same memory location without synchronisation, and at least one of the accesses is a write.
- Without synchronisation, different time orderings of the accesses may occur, possibly resulting in non-deterministic behaviour.
	- Running the same program with the same inputs twice may give different results.
- Not reliably detectable by conventional software testing procedures.

**Tasks**
- A *task* is a piece of computation which can be executed independently of other tasks.
- In principle, we could create a new thread to execute every task.
	- In practice, this can be too expensive, especially if we have large numbers of small tasks.
- Instead tasks can be executed by a pre-existing pool of threads.
	- Tasks are submitted to the pool.
	- Some thread in the pool executes the task.
	- At some point in the future the task is guaranteed to have completed.
	- Tasks may or may not be ordered with respect to other tasks.

**Parallel loops**
- Loops are the main source of parallelism in many applications.
- If the iterations of a loop are *independent* (can be done in any order) then we can share out the iterations between different threads.
- E.g. if we have two threads and the loop
```
For (int i = 0; i < 100; ++i) {
	a[i] += b[i];
}
```
- we could do iteration 0-49 on one thread and iterations 50-99 on the other.
	- N.B. [^2], in practice we would need at least 10,000 iterations to make parallelism worthwhile.
- Can think of an iteration, or a set of iterations, as a task.

**Reductions**
- A *reduction* produces a single value from associative operations such as addition, multiplication, max, min, and, or.
- For example:
```
b = 0;
for (int i = 0; i < n; ++i) {
	b += a[i];
}
```
- Allowing only one thread at a time to update $b$ would remove all parallelism.
- Instead, each thread can accumulate its own private copy, then these copies are reduced to give final result.
- If the number of operations is much larger than the number of threads, most of the operations can proceed in parallel.

**What is OpenMP?**
- OpenMP is an API designed for programming shared memory parallel computers.
- OpenMP uses the concepts of threads and tasks.
- OpenMP is a set of extensions to FORTRAN, C and C++.
- The extension consists of:
	- Compiler directives
	- Runtime library routines
	- Environment variables

**Directives and sentinels**
- A directive is a special line of source code with meaning only to certain compilers.
- A directive is distinguished by a sentinel at the start of the line.
- OpenMP sentinels are:
	- FORTRAN: !$OMP
	- C/C++: $\# \text{pragma omp}$
- This means that OpenMP directives are ignored if the code is compiled as regular sequential FORTRAN/C/C++.

**Parallel region**
- The parallel region is the basic parallel construct in OpenMP.
- A parallel region defines a section of the program.
- Program begins execution on a single thread (the master thread).
- When the first parallel region is encountered, the master thread creates a team of threads (fork/join model).
- Every thread executes the statements which are inside the parallel region.
- At the end of the parallel region, the master thread waits for the other threads to finish, and continues executing the next statements.

Model example:
![[Pasted image 20250623111541.png]]

**Shared and private data**
- Inside a parallel region, variables can either be shared or private.
- All threads see the same copy of shared variables.
- All threads can read or write shared variables.
- Each thread has its own copy of private variables: these are invisible to other threads.
- A private variable can only be read or written by its own thread.
	- May be possible to access another thread's private data, but behaviour is unspecified, and very bad coding style!

- In a parallel region, all threads execute the same code.
- OpenMP also has directives which indicate that work should be divided up between threads, not replicated.
	- This is called worksharing.

**Synchronisation**
- The main synchronisation concepts used in OpenMP are:
 - Barrier
	 - All threads must arrive at a barrier before any thread can proceed past it.
	 - E.g. end of parallel region, end of parallel loop.
 - Critical region
	 - A section of code which only one thread at a time can enter.
	 - E.g. modification of shared variables.
 - Atomic accesses
	 - An update/read/write of a variable which can be performed only by one thread at a time.
	 - E.g. modification of shared variables (special case).


**Compiling and running OpenMP programs**
- OpenMP is built-in to most of the compilers you are likely to use.
- To compile an OpenMP program, you need to add a (compiler-specific) flag to your compile and link commands.
```
-fopenmp for gcc/gfortran, clang, cray.
-h omp for Cray Fortran compilers.
-mp for flang compiler.
-qopenmp for intel compilers.
```

- The number of threads which will be used is determined at runtime by the $\text{OMP\_NUM\_THREADS}$ environment variable.
	- Set this before you run the program.
	- E.g. export OMP_NUM_THREADS=4.
- Run in the same way you would a sequential program.

**Parallel region directive**
- Code within a parallel region is executed by all threads.

**Shared and private**
- On entry to a parallel region, private variables are uninitialised.
- Variables declared inside the scope of the parallel region are automatically private.
- After the parallel region ends, the original variable is unaffected by any changes to private copies.
- In C++, private objects are created using the default constructor.
- Not specifying a $\text{default}$ clause is the same as specifying $\text{default(shared)}$.
- **Danger**
	- Always use $\text{default(none)}$

**Multi-line directives**
- C / C++:
```c
#pragma omp parallel default(none) \ private(i, myid) shared(a, n)
```

**Initialising private variables**
- Private variables are uninitialised at the start of the parallel region.
- If we wish to initialise them, we use the $\text{firstprivate}$ clause instead of $\text{private}$:
	- C / C++: $\text{firstprivate(list)}$
- Private copies are initialised with the value in the original variable at the start of the parallel region.
- Note: use cases for this are surprisingly uncommon.
- In C++ the default copy constructor is called to create and initialise the new object.

**Work sharing directives**
- Directives should appear inside a parallel region and indicate how work should be shared out between threads.
	- Parallel for loops.
	- Single directive.
	- Master directive.

**Parallel for loops**
- Loops are the most common source of parallelism in most codes. Parallel loop directives are therefore very important.
- A parallel for loop divides up the iterations of the loop between threads.
- The loop directive appears inside a parallel region and indicates that the work should be shared out between threads, instead of replicated.
- There is a synchronisation point at the end of the loop: all threads must finish their iterations before any thread can proceed.

Syntax:
```c
#pragma omp for [clauses]
for loop
```

**Restrictions in C / C++**
- Because the for loop in C is a general while loop, there are restrictions on the form it can take.
- It has to have a determinable trip count - it must be of the form:
	- $\text{for ( var = a; var logical-op b; incr-exp)}$

**Clauses**
- $\text{for}$ directive can take $\text{private, firstprivate}$ and $\text{reduction}$ clauses which refer to the scope of the loop.
- Note that the parallel loop index variable is private by default.
- $\text{parallel for}$ direction can take all clauses available for $\text{parallel}$ directive.
- $\textbf{Beware!}\text{ parallel for}$ is not the same as $\text{for}$ or the same as $\text{parallel}$.

**Parallel for loops**
- With no additional clauses, the $\text{for}$ directive will partition the iterations as equally as possible between the threads.
- However, this is implementation dependent, and there is still some ambiguity:
	e.g. 7 iterations, 3 threads. Could partition as 3+3+1 or 3+2+2.

**Schedule clause**
- The SCHEDULE clause gives a variety of options for specifying which loops iterations are executed by which thread.
- Syntax:
  C / C++: $\text{schedule (kind, chunksize)}$
	where kind is one of:
		$\text{static, dynamic, guided, auto or runtime}$.
	and $\text{chunksize}$ is an integer expression with positive value.
	- e.g. $\text{\#pragma omp for schedule(dynamic, 4)}$

**Static schedule**
- With no chunk size specified, the iteration space is divided into (approximately) equal chunks, and one chunk is assigned to each thread in order (**block** schedule).
- If chunk size is specified, the iteration space is divided into chunks, each of chunk size iterations, and the chunks are assigned cyclically to each thread in order (**block cyclic** schedule).

**Dynamic schedule**
- **dynamic** schedule divides the iteration space up into chunks of size chunk size, and assigns them to threads on a first-come-first-served basis.
- I.e. as a thread finishes a chunk, it is assigned the next chunk in the list.
- When no chunk size is specified, it defaults to 1.

**Guided schedule**
- **guided** schedule is similar to **dynamic**, but the chunks start off large and get smaller exponentially.
- The size of the next chunk is proportional to the number of remaining iterations divided by the number of threads.
- The chunk size specifies the minimum size of the chunks.
- When no chunk size is specified, it defaults to 1.

**Auto schedule**
- Lets the runtime have full freedom to choose its own assignment of iterations to threads.
- If the parallel loop is executed many times, the runtime can evolve a good schedule which has good load balance and low overheads.

**Runtime schedule**
- Allows the schedule to be set using the environment variable $\text{OMP\_SCHEDULE}$ 
	- E.g. $\text{export OMP\_SCHEDULE="dynamic, 1"}$
- Convenient for experimenting with schedules and chunk sizes without having to recompile.

**When to use which schedule?**

- $\text{static}$ usually best for load balanced loops - least overhead.
- $\text{static, n}$ good for loops with mild or smooth load imbalance, but can induce overheads for small chunk sizes.
- $\text{dynamic}$ useful if iterations have widely varying loads, but ruins data locality.
- $\text{guided}$ often less expensive than $\text{dynamic}$, but beware of loops where the first iterations are the most expensive!
- $\text{auto}$ allows compiler-specific options.

**Single directive**
- Indicates that a block of code is to be executed by a single thread only.
- The first thread to reach the $\text{single}$ directive will execute the block.
- There is a synchronisation point at the end of the block: all the other threads wait until block has been executed.

Syntax:
```c
#pragma omp single [clauses]
	structured block
```

- Construct must contain a structured block: cannot branch into or out of it.

Visual example:
![[Pasted image 20250623145313.png]]

**Nowait clause**
- The implicit barrier synchronisation at the end of worksharing directive ($\text{for}$ or $\text{single}$) can be removed by adding a $\text{nowait}$ clause.
	Use with care, easy to introduce race conditions....

```c
#pragma omp for nowait
	for loop
#pragma omp single nowait
	structured block
```

**Master directive**
- Indicates that a block of code should be executed by the master thread (thread 0) only.
- There is no synchronisation at the end of the block: other threads skip the block and continue executing: N.B. different from $\text{single}$ in this respect.
- Latest versions of OpenMP have deprecated the name and replaced it with $\text{masked}$.

Syntax:
```c
#pragma omp master
	structured block
```

**Orphaned directives**
- Directives can be present in functions called from inside parallel regions.

Example:
```c
#pragma omp parallel
{
	fred();
}
void fred() {
#pragma omp for
	for(int i = 0; i < N; ++i) {
		a[i] += 23.5;
	}
}
```

- This is very useful, as it allows a modular programming style...
- But it can also be rather confusing if the call tree is complicated (what happens if $\text{fred}$ is also called from outside a parallel region? - the worksharing loop is all executed by the master thread).

**Data scoping rules**
When we call a subroutine/function from inside a parallel region:
- Variables passed by reference/address in the argument list inherit their data scope attribute from the calling routine.
- Global variables in C / C++ are shared unless declared $\text{threadprivate}$.
- $\text{static}$ local variables in C / C++ are shared.
- All other local variables are private.

**Synchronisation**

**Why is it required?**
Recall:
- Need to synchronise actions on shared variables.
- Need to ensure correct ordering of reads and writes.
- Need to protect updates to shared variables (not atomic by default).

**Barrier directive**
- No thread can proceed past a barrier until all the other threads have arrived.
- Remember that there is an *implicit* barrier at the end of $\text{for}$ and $\text{single}$ directives.
Syntax:
```c
#pragma omp barrier
```

- Either all threads or none must encounter the barrier: otherwise deadlock!

Code example:
![[Pasted image 20250623151322.png]]

**Critical sections**
- A critical section is a block of code which can be executed by only one thread at a time.
- Can be used to protect updates to shared variables.
- Mutual exclusion is enforced between all critical sections in the code.

Syntax:
```c
#pragma omp critical
```

Code example:
![[Pasted image 20250623151501.png]]

**Atomic directive**
- Used to protect a single update to a shared scalar variable (or array element) of basic type.
- Applies only to a single statement.

Syntax:
```c
#pragma omp atomic
	statement
```

where statement must have one of the forms:
$\text{x binop = expr, x++, ++x, x--, or --x}$.
and $\text{binop}$ is one of $\text{+ ,*, -, /, \&, \^ , <<, or >>}$.
**"Note that the evaluation of `expr` is not atomic."**

- This is a crucial point. In `x binop= expr`, only the `x binop= ...` part that involves the update to `x` is atomic. The `expr` itself (the value being added, subtracted, etc.) is evaluated _before_ the atomic operation begins. If `expr` itself involves reading or modifying other shared variables, those reads/modifications are _not_ automatically made atomic by this directive.

- Should be more efficient than using $\text{critical}$ directives, e.g. if different array elements can be protected separately.
- No interaction with $\text{critical}$ directives.

**Lock routines**
- Sometimes we need more flexibility than is provided by $\text{critical}$ or $\text{atomic}$ directives.
- A lock is a special variable that may be set by a thread. No other thread may set the lock until the thread which set the lock has unset it.
- Setting a lock can either be blocking or non-blocking.
- A lock must be initialised before it is used, and may be destroyed when it is not longer required.
- Lock variables should not be used for any other purpose.
- OpenMP locks are equivalent to mutexes in other APIs.
- A critical construct is equivalent to setting a lock on entry to the block of code and unsetting it on exit.

Syntax:
```c
#include <omp.h>
void omp_init_lock(omp_lock_t* lock);
void omp_set_lock(omp_lock_t* lock);
int omp_test_lock(omp_lock_t* lock);
void omp_unset_lock(omp_lock_t* lock);
void omp_destroy_lock(omp_lock_t* lock);
```

**Summary in my own words:**
Shared memory parallel programming models use threads.
Threads are, by default, executed asynchronously.
Must watch out for ordering of instructions/execution of threads as instructions we will use are not atomic.



**Further reading (questions & resources):**
*Using OpenMP : Portable Shared Memory Parallel Programming*


**References**
*EPCC HPC Summer School*
**Lecturers: Mark Bull**

[^1]: Non-blocking, the program can continue to run whilst the asynchronous operation is taking place in the background.

[^2]: Nota Bene, it means to pay attention to this detail.
