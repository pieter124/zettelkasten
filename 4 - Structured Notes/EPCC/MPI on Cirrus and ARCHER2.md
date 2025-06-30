2025-06-26 

Tags: [[parallel]] [[programming]]

# **MPI on Cirrus and ARCHER2**

**Key ideas:**
Typical HPC system layout:
![[Pasted image 20250626101802.png]]

**Useful files and templates**
- Take a copy of $\textbf{MPP-templates.tar}$.
	- See the course web pages.
- Unpack: $\textbf{tar -xvf MPP-templates.tar}$.

**Compiling MPI Programs on Cirrus**
- C programmers use: $\text{mpicc -cc=icc}$.
- C++ programmers use: $\text{mpicxx -cxx=icpc}$.

- There is nothing magic about these MPI compilers!
	- Simply wrappers which automatically include various libraries, etc.
	- Compilation done by standard (e.g. Intel) compilers.
		- icc, icpc.

**Running interactively on Cirrus**
- Timings will not be reliable..
	- Shared with other users, many more processes than processors.
	- But $\textbf{very useful}$ during development and for debugging.
- $\textbf{mpirun -n 4  ./mpiprog.exe}$
	- Runs your code on 4 processes.
- NOTE:
	- Output might be buffered.
	- If your program crashes, you may see no output at all.
- It may help to explicitly flush prints to screen.
	- $\textbf{fflush(stdout)};$



**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**
