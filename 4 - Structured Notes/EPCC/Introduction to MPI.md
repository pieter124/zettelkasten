2025-06-26 

Tags: [[parallel]] [[programming]]

# **Introduction to MPI**

**Key Ideas:**
- MPI's prime goals are:
	- To provide source-code portability.
	- To allow efficient implementation.
- It also offers:
	- A great deal of functionality
	- Support for heterogeneous parallel architectures.

```
// header file for C/C++
#include <mpi.h>
```

C:
```
error = MPI_Xxxxx(param, ...);
MPI_Xxxxx(param, ...);

// If successful, return value is MPI_SUCCESS.
```

**Handles**
- MPI controls its own internal data structures.
- MPI releases 'handles' to allow programmers to refer to these.
- C handles are of defined typedefs.

**Initialising MPI**
```
int MPI_Init(int *argc, char***argv)
```
- Must be the first MPI procedure called.
	- But multiple processes are already running before $\text{MPI\_Init}$.

**Rank**
- How do you identify different processors in a communicator?
```
MPI_Comm_rank(MPI_Comm comm, int* rank)
```

- The rank is not the physical processor number
	- Numbering is always 0, 1, 2, ..., N - 1.

**Size**
- How many processes are contained within a communicator?
```
MPI_Comm_size(MPI_Comm comm, int* size)
```

**Exiting MPI**
```c
int MPI_Finalise()
```
- Must be the last MPI procedure called.

**What machine am I on?**
- Can be useful on a cluster.
	- E.g. to confirm mapping of processes to nodes/processors/cores,
```c
int namelen;
char procname[MPI_MAX_PROCESSOR_NAME];
MPI_Get_processor_name(procname, &namelen);
printf("rank %d is on machine %s\n", rank, procname);
```

**Summary**
- Have covered basic MPI calls..
	- But no explicit message-passing yet.
- Can still write useful programs.
	- E.g. a task farm of independent jobs.
- Need to compile and launch parallel jobs.
	- Procedure is not specified by MPI.

**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**