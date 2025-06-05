2025-06-03 

Tags: [[leetcode]] [[algorithms]]

# **Binary Search**

Binary search is a commonly used searching algorithm that is an efficient way to search for a target in a data structure. Instead of scanning through elements one by one (Linear Search), binary search starts by comparing the target value to the middle element.

The comparison allows us to get rid of half the search space on each comparison. Repeatedly cut the search space in half on each iteration which leads to a **O(log(n))** solution.

You can **binary search for:**
- An element in a data structure
- A value

**Common Pitfalls:**
- Only works on sorted data.
- Infinite loops.
- Not updating the bounds correctly.
- Overflow in mid calculation.

**References**
*James Peralta's*
**Coding Patterns: Binary Search:** https://www.youtube.com/watch?v=Kz9JVIIaXmM