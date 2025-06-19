2025-06-17 

Tags:  [[programming]] 

# **Python and Numpy** 

```
import numpy as np
// load text using numpy
data = np.loadtxt(fname="locationandnameoffile", delimiter=",", skiprows=1)

// to find the type of data in numpy array
data.dtype

// cool notation fact
A[: , :1] != A[:][:1]
The first one means to take all indices of x along the first axis, but take only index 1 along the second. The second one means to take all indices of x along the first axis, but only take index 1 along the first axis of the result.

import matplotlib.pyplot as mp

fig = mp.figure(figsize=(10,3))
// adding a subplot, first number represents the number of rows, second is the number of columns and third represents the specific position of the subplot within that grid.
axes1 = fig.add_subplot(1,3,1)


```

**Key Ideas:**
Make sure to understand how numpy deals with NaN values.
Scientific data is often stored in NetCDF files.
Glob is a useful library used for finding all the path names matching a specified pattern according to the rules used by the Unix shell.

**References**
*EPCC HPC Summer School*
**Lecturers: Chris Wood, Evgenij Belikov**
