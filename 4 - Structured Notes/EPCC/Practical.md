2025-06-18 

Tags: [[programming]] 

# **Practical**
Simple parallel image sharpening exercise.

**Image sharpening**
Images can be fuzzy for two main reasons:
- random noise
- blurring

Aim to improve image quality by:
- smoothing to remove noise 
- detecting edges
- sharpening up the image with the edges

**Technicalities**
Each pixel replaced by a weighted average of its neighbours.
- weighted by a 2D Gaussian
- averaged over a square region

Using:
- Gaussian width of 1.4
- a large square region
Then apply a Laplacian:
- This detects edges
- a 2D second-derivative $\delta^2$

Combine both operations:
- produces a single convolution filter.

**Implementation**
For over every pixel in the image, loop over all the pixels in a large area surrounding it.
- Up to distanced d away in each direction: $(2d+1)^2$ square
	- We use d = 8, so 17 x 17 square.
Add in the value of the pixel weighted by a filter.

$\large edge(i ,j) = \sum_{k = -d, d} \sum_{l = -d, d} \text{image (i + k, j + l) x  filter(k, l)}$ 

This gives the edges:
- Add the edges back into the image with some scaling factor.
	- S.F. 2.0
- Re-scale the sharpened image so pixels lie in the range 0-255.

**Existing parallelisation**

Parallelisation:
- Each pixel can be processed independently.
- A master process reads the image
- Broadcast the whole image to every process
- Each process computes edges for a subset of pixels:
	- Scan the image line by line
	- With four processes, each process computes every fourth pixel
- Combine the edges back onto a master process
	- Add back into original image and re-scale.
	- Save to disk.
- Reports two times:
	- Calculation time for just computing edges on each process.
	- Overall time for the whole program including IO.

Parallelisation is achieved using message-passing model.
Implemented using MPI.
- The message-passing interface.

Another version parallelised using shared-variables model
Implemented using OpenMP.
- HPC standard for threaded programming

MPI Data Collected:
$\textbf{1 Core}\text{, Overall Run Time = 1.604864s, Calculation Time = 1.454321s.}$
$\text{IO Time  }\approx \text{ 0.15s, Total CPU Time = 1.454321s.}$
$\textbf{2 Cores}\text{, Overall Run Time = 0.882633s, Calculation Time = 0.744741s.}$
$\text{IO Time } \approx \text{ 0.14s, Total CPU Time = 1.489482s.}$
$\textbf{4 Cores}\text{, Overall Run Time = 0.539499s, Calculation Time = 0.391560s.}$
$\text{IO Time } \approx \text{ 0.14s, Total CPU Time = 1.56624s.}$
$\textbf{7 Cores}\text{, Overall Run Time = 0.398807s, Calculation Time = 0.234224s.}$
$\text{IO Time } \approx \text{ 0.15s, Total CPU Time = 1.639568s.}$
$\textbf{10 Cores}\text{, Overall Run Time = 0.328071s, Calculation Time = 0.172544s.}$
$\text{IO Time} \approx \text{ 0.15s, Total CPU Time = 1.72544s.}$
$\textbf{36 Cores}\text{, Overall Run Time = 0.221618s, Calculation Time = 0.055260s.}$
$\text{IO Time} \approx \text{ 0.17s, Total CPU Time =  1.98936s.}$
$\textbf{72 Cores}\text{, Overall Run Time = 0.214168s, Calculation Time = 0.029350s.}$
$\text{IO Time } \approx \text{ 0.19s, Total CPU Time = 2.1132s.}$
$\textbf{108 Cores}\text{, Overall Run Time = 0.197936s, Calculation Time = 0.020607s.}$
$\text{IO Time } \approx \text{ 0.17s, Total CPU Time = 2.225556s.}$
$\textbf{144 Cores}\text{, Overall Run Time = 0.196509s, Calculation Time = 0.015874s.}$
$\text{IO Time } \approx \text{ 0.18s, Total CPU Time = 2.285856s}$

OpenMP Data Collection:
$\textbf{1 Core}\text{, Overall Run Time = 1.629717s, Calculation Time = 1.515646s.}$
$\text{IO Time }\approx \text{ 0.11s, Total CPU Time = 1.515646s.}$
$\textbf{2 Cores}\text{, Overall Run Time =  0.883056s, Calculation Time = 0.741331s.}$
$\text{IO Time } \approx \text{ 0.14s, Total CPU Time = 1.482662s.}$
$\textbf{4 Cores}\text{, Overall Run Time = 0.636374, Calculation Time = 0.470732s.}$
$\text{IO Time } \approx \text{ 0.16s, Total CPU Time = 1.882928s.}$
$\textbf{7 Cores}\text{, Overall Run Time = 0.469369s, Calculation Time = 0.297455.}$
$\text{IO Time } \approx \text{ 0.17s, Total CPU Time = 2.082185s.}$
$\textbf{10 Cores}\text{, Overall Run Time = 0.354399s, Calculation Time = 0.187095s.}$
$\text{IO Time } \approx \text{ 0.17s, Total CPU Time = 1.87095s.}$
$\textbf{12 Cores}\text{, Overall Run Time = 0.343299s, Calculation Time = 0.226674s.}$
$\text{IO Time } \approx \text{ 0.12s, Total CPU Time = 2.720088s.}$
$\textbf{18 Cores}\text{, Overall Run Time  = 0.313213s, Calculation Time = 0.163421s.}$
$\text{IO Time } \approx \text{ 0.15s, Total CPU Time = 2.941578s.}$
$\textbf{24 Cores}\text{, Overall Run Time = 0.385432s, Calculation Time = 0.196071s.}$
$\text{IO Time } \approx \text{ 0.19s, Total CPU Time = 4.705704s.}$
$\textbf{36 Cores}\text{, Overall Run Time = 0.258476s, Calculation Time = 0.093817s.}$
$\text{IO Time } \approx \text{ 0.16s, Total CPU Time = 3.377412s.}$

