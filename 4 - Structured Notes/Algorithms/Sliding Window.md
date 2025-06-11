2025-06-01 

Tags: [[leetcode]] [[algorithms]]

# **Sliding Window**

Sliding Window is an algorithmic technique used to solve problems when we need to calculate something for subarrays of a given size or find the optimal contiguous subarray in an array. Also used for string questions and they will ask you to find some "substring".

**Tips:**
- In an interview if they ask to find an **optimal subarray** ask if it's **contiguous.**
- When you hear "contiguous" you should think if there's a sliding window solution.

**Sliding window** *can be:*
- **Static:** You know the exact window size in advance. i.e.
- **Dynamic:** Expanding and shrinking the window based on some constraint.

**Sliding Window vs. Two-Pointer Approach**

**Both** *maintain two pointers but:*
- **Two-Pointer:** Usually refers to having two independent pointers and we don't care about the elements between those pointers.
- **Sliding Window:** Implies you're maintaining a contiguous window of interest between the two pointers.

*Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold*

Code Example
```
def numOfSubarrays(self, arr: List[int], k: int, threshold: int) -> int:
	i, j = 0, 0
	res = 0
	current = 0
	stack = []
	while j < len(arr):
		while j - i < k:
			current += arr[j]
			j += 1
		if current / k >= threshold:
			res += 1
		current -= arr[i]
		i += 1
	return res
```

**Common Pitfalls:**
- Not expanding/shrinking the window correctly.
- Updating the result at the right time:
	- For a **fixed-size** window, only update the result once the window reaches the required size.
	- For a **dynamic** window, update result only if your window meets the conditions. Usually you grow your window until it breaks the condition then you shrink from the left until it meets the condition again.

**References**
*James Peralta*'s
**Coding Patterns: Sliding Window:** https://www.youtube.com/watch?v=Buv4oAmlY4M

