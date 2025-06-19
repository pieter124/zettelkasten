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
