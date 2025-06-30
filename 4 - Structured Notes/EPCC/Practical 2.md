2025-06-20 

Tags: [[programming]] [[parallel]]

# **Practical 2**

**CFD exercise**
Regular domain decomposition

**Computational Fluid Dynamics**

- Study of the mechanics of fluid flow, liquids and gases in motion.
- Commonly requires HPC.
- Continuous systems typically described by partial differential equations.
- For a computer to simulate these systems, these equations must be discretised[^2] onto a grid.
- One such discretisation approach is the *finite difference* method.
- This method states that the value at any point in the grid is some combination of the neighbouring points.

**The problem**
- Determining the flow pattern of a fluid in a cavity.
	- A square box.
	- Inlet on one side
	- Outlet on the other.

Model:
![[Pasted image 20250620104811.png]]
- For simplicity, we assume zero viscosity for this exercise.

**The Maths**
- In two dimensions, easiest to work with the stream function $\large \psi$.
- At zero viscosity, $\large \psi$ satisfies:

$\large \nabla^2\Psi = \frac{\partial^2\Psi}{\partial x^2} + \frac{\partial^2\Psi}{\partial y^2} = 0$

- With finite difference form:

$\large \psi_{i - 1, j} + \psi_{i + 1, j} + \psi_{i, j - 1} + \psi_{i, j + 1} - 4 \psi_{i, j} = 0$
2
- Jacobi iterative method can be used to find solutions.
- With boundary values fixed, stream function can be calculated for each point by averaging value at that point with its four nearest neighbours.
	- Process continues until the algorithm converges on a solution which stays unchanged by the averaging.
	- Iterative methods are a very common computational approach for solving system of equations.

**Jacobi iterative method**
To solve: $\large \psi_{i - 1, j} + \psi_{i + 1, j} + \psi_{i, j - 1} + \psi_{i, j + 1} - 4 \psi_{i, j} = 0$

Repeat for many iterations, loop over all points *i* and *j*:
``` 
psinew[i][j] = 0.25 * ( psi[i+ 1][j] + psi[i - 1][j] + psi[i][j + 1] + psi[i][j - 1] )
```
Copy $\text{psinew}$ back to $\text{psi}$ for next iteration.

**Notes**
- Finite viscosity gives more realistic flows
	- Introduces a new field zeta related to the vorticity[^1].
- Terminating the process
	- Larger problems require more iterations.
	- Fixed number of iterations OK for performance measurement but not if we want an accurate answer.
	- Compute the RMS change in $\psi$ and stop when it is small enough.

**Grids**
- The algorithm involves calculating the value at each grid by combining it with the value of its neighbours.
- Same amount of work needed to calculate each grid point - ideal for the geometric decomposition approach.
- Grid is broken up into smaller grids and one is allocated to each process.

**Halo Swapping**
- Points on the edge of a grid present a challenge. Required data is shipped to a remote processor. Processes must therefore communicate.
- Solution is for processor grid to have a boundary layer on adjoining sides.
- Layer is not writable by the local process.
- Updated by another process which in turn will have a boundary updated by the local process.
- Layer is generally known as a *halo* and the inter-process communication which ensures their data is correct and up to date is a *halo swap*.
![[Pasted image 20250620114550.png]]


[^1]: A vector field that describes the local spinning motion of a fluid==.

[^2]: Computers cannot handle continuous infinities. So CFD converts these continuous PDEs into a finite-dimensional problem that a computer can understand.
