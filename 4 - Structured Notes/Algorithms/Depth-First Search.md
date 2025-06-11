2025-06-02 

Tags: [[leetcode]] [[algorithms]]

# **Depth-First Search**

Depth-First Search (DFS) traversal is a technique for traversing non-linear data structures such as Trees and Graphs. In DFS, we explore one branch as far as possible before backtracking and exploring other branches. 

DFS can be used to traverse both a **Tree** or **Graph**.

DFS is implemented via **Stack** (last in, first out data structure).

The main types of DFS traversals include:

- **Pre-order traversal**: Visit the root node first, then the left subtree, and finally the right subtree.

- **In-order traversal**: Visit the left subtree first, then the root node, and finally the right subtree.

- **Post-order traversal**: Visit the left and right subtrees first, and then the root node.

Example diagram:
![[Pasted image 20250602161649.png]]

To solve DFS-based problems, the approach generally involves:

- **Recursive approach**: Leverages call stack to traverse the tree.

- **Iterative approach**: Uses in memory stack to mimic recursion

**Common Pitfalls**:
- Not adding to the seen array and getting into infinite loops when traversing graphs.

**References**
*James Peralta's*
**Coding Patterns: Depth-First Search:** https://www.youtube.com/watch?v=2tNQUaq3Y7E
