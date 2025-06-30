2025-06-25 

Tags:  [[programming]] [[parallel]] 

# **OpenMP Data Movement** 

**Key Ideas:**

**Basics of data movement**
- The "traditional" GPU model has separate, non-unified memory on the host and on the device(s).
	- Host memory is the CPU memory.
		- Where all our "normal" code and variables live.
			- Where our program actually executes.
	- Device memory is the GPU memory.
		- Can copy data to and from this memory from the host memory.
		- Individual GPU kernels are spawned from the CPU program and run here.
-  NVIDIA Grace Hopper and AMD MI300A have superchip designs.
	- "Unified Memory"
	- Can affect approach to data movement.
		- And potentially remove the need to deal with this altogether.

- This means that any data the GPU will work on needs to be present in the GPU's memory.

Why is this important? **Data movement is slow**

**Implicit data movement**

- All data used in GPU work needs to be in memory visible to the GPU.
	- Otherwise, what will the GPU do work on?
	- This traditionally means the GPU's own memory, separate from CPU memory.
	- Newer unified memory designs in some way combine CPU and GPU memory.
- OpenMP keeps track of what data is available on GPU.
- If an array used in $\text{\#pragma omp target/\$omp target}$ region isn't already on the GPU, then it is implicitly copied in at the beginning and copied back out at the end i.e. $\text{map(tofrom:..)}$.
- Scalars are implicitly $\text{firstprivate}$.

With C/C++, need to provide sizes with dynamic arrays.
![[Pasted image 20250625120618.png]]
**Introduction to structured data regions**
Consider this example:
![[Pasted image 20250625120757.png]]
- This code is not efficient!
	- Both $\text{B}$ and $\text{C}$ are copied to the GPU on entry to each $\text{parallel for}$.
- If they don't change in the meantime why not just copy once and leave the data there for both kernels?
- It is often the case that we want to run multiple kernels on the GPU while keeping data there.

Consider the reworked example:
![[Pasted image 20250625121113.png]]
- Use a $\text{data}$ construct to define a larger data offload region.
- Provide a $\text{map}$ clause to the construct to tell it, just as before, what to do with the variables inside the region.
- Now $\text{B}$ and $\text{C}$ are only copied in once on entry to the data region.

**Reference counts**
- It can be difficult to tell for a given target region whether data has been mapped already (e.g. using data regions) or not.
	- With structured and especially with unstructured (later) data regions!
- We want to be able to write $\text{map}$ clauses that are always correct but do not do unnecessary copies.
- OpenMP uses reference counts to track whether a data item is already mapped to the device.
	- If it is, $\text{map}$ clauses for the data item will have no effect.
	- ...but we can override this behaviour if we need to with $\text{always}$.

- OpenMP tracks reference counts to the list items in the $\text{map}$ clauses.
- A $\text{map(to:...)}$ clause increments the count by 1 on entry, and $\text{map(from:...)}$ likewise decrements it by 1 on exit.
- If a count is 0 on exiting a region, the variable is deallocated.
- For example:
	- With a prior reference count of 0, on entering $\text{map(to:...)}$ will allocate counterparts of the listed host variables on the device memory, give them a reference count of 1, and copy their values in from the host memory.
	- With a prior reference count of 1, $\text{map(from:...)}$ will copy values from the listed variables on device memory back to their counterparts on the host, decrement their reference counts to 0, and then deallocate them from the device.

- OpenMP tracks reference counts to the variables in offload regions.
- Generally, but not specifically, if a variable is in an offload region:
	- Its reference count increments by 1 on entry to the region, and decrements by 1 on exit from the region.
- Allows OpenMP to do a presence check: is a device counterpart to the host variable already present?
	- This can occur with nested offload data regions as we'll see.
- If already present, behaviour of $\text{to, from and tofrom}$ change: they copy no data and instead only check that sizes are correct.
	- $\text{target update}$ will always transfer data, irrespective of the reference count.
- If the ref count = 0 on exit, OpenMP knows it can safely deallocate.

**Map modifiers**
- Add even further control with these modifiers to be used in $\text{map()}$.
- $\text{always}$ - Always copy data $\text{to, from and tofrom}$ from the device. These otherwise don't copy data if it's already present (ref count $\geq 1$).
- $\text{close}$ - A hint to allocate memory $\text{close}$ to the target device.
- $\text{mapper}$ - Create with $\text{declare mapper}$ and then use in $\text{map}$ to choose how derived types and structs should be mapped.
- $\text{present}$ - Run a $\text{map}$ with $\text{present}$ first before any without.
- $\text{iterator}$ - Control indexing of variables, e.g. map every second element of $\text{A}$:
	- $\text{map(iterator(int i = 0:N:2), to: A[i])}$

**Update in data region**

- Map clauses like $\text{map(to: A)}$ would not do anything inside a data region like this 
as $\text{A}$ already exists (we'll come back to this).
- If a change is needed, could use $\text{map(always to: A)}$, or $\text{update}$.
![[Pasted image 20250625183113.png]]

- Can potentially make update even more performant by adding $\text{if, depend and/or nowait clauses}$.
- Of course, this makes code more complex and more prone to bugs.
	- Probably best to code without these initially, then try to introduce them for more performance once you're sure everything's working.
- $\text{if}$ : provide an expression and only update if true.
	- $\text{\#pragma omp target update if(i >= 100) to (A)}$.
- $\text{nowait}$:
	- Can be added to target regions in general to enable asynchronous execution.

**Unstructured data regions**
- The prior $\text{data}$ regions were structured: they began, OpenMP offloaded work to the GPU, then the data region ended.
- There is a requirement also for unstructured $\text{data}$ regions: define a region of code where data is created on the device, and a region of code where that data is copied back to host or deleted.
- Necessary e.g. in OOP: we might want to copy data to GPU memory in an object's constructor, later on do work with that data, then delete the data from the GPU memory in the object destructor.
- Use the $\text{enter data and exit data}$ constructs.
	- Often use $\text{enter}$ right after allocating, and $\text{exit}$ right before freeing.

**Data regions in objects (C++)**
![[Pasted image 20250625183756.png]]
**Tips:**
- When mapping data, think of all words like 'to' and 'from' as being from the CPU's perspective, looking out towards the GPU.
- When keeping data consistent between host and device, remember a simple $\text{map(to:..)}$ or $\text{map(from:...)}$ will be ignored if data is already present on device.
	- Either use $\text{update}$ or force a $\text{map}$ with the $\text{always}$ modifier.
- If your compiler produces debugging or verbose output, check it:
![[Pasted image 20250625184132.png]]

**Further reading (questions & resources):**
*Using OpenMP : Portable Shared Memory Parallel Programming*


**References**
*EPCC HPC Summer School*
**Lecturers: David Henty**
