2025-06-09 

Tags: [[data structures]] [[leetcode]]

# **Heaps**

Heaps are **tree-based data structures constrained by a heap property.**

There are **two** types of heaps:
- **Min heap**
- **Max heap**

Max heap is essentially the reverse of min heap.

In a min heap, **all the elements are smaller than their children so the root node will be the very smallest element**

**Insertion:**
Adding to a min heap, the element always goes in the next empty spot looking top to bottom, left to right. If it is out of order, it swaps positions with its parent and continues this process until it is in the right order.

**Removing the minimum element:**
We remove the minimum element (root node), then swap the value with the last element added. This element might be out of order so we swap with the smaller child and continue this process until it is in the right order.

**Array representation** of a **binary tree**:

If a **Node** is at index **i**:

- Its **left child** is at index **2 * i + 1**.

- Its **right child** is at index **2 * i + 2**.

- Its **parent** is at index **$\dfrac{i - 1}{2}$**

If a binary tree has a height of **h**, then a full binary tree can have **$\large2^{h + 1} - 1$** as the maximum number of nodes.

**References**
*Abdul Bari's*
**2.6.3 Heap - Heap Sort - Heapify - Priority Queues:**
https://www.youtube.com/watch?v=HqPJF2L5h9U

*HackerRank's*
**Data Structures: Heaps:** https://www.youtube.com/watch?v=t0Cq6tVNRBA