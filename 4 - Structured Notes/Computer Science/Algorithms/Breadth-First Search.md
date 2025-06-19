2025-06-02 

Tags: [[leetcode]] [[algorithms]]

# **Breadth-First Search**

Breadth-First Search (BFS) traversal is a technique for traversing non-linear data structures such as Trees and Graphs. In BFS we prioritize breadth over depth - it explores the level by level instead of exploring one branch all the way down like DFS does.

BFS can be used to traverse both a **Tree** or **Graph**.

BFS is implemented via **Queue** (First in, first out data structure).

BFS helps us find the **shortest path in a graph *where the edges have no weight/or equal weight**.

**Time Complexity**: **O(V + E)**, where V is the number of **vertices** and E is the number of **edges**. You visit each vertex and explore each edge at most once.

**Space Complexity**: **O(V**) in the worst case, since all nodes could be in the queue if the branching factor is high.

**Common Pitfalls**:
- Forgetting to mark nodes visited before enqueuing them, which can lead to duplicates or infinite loops.
- Not handling disconnected graphs; make sure you either run BFS from each unvisited node or confirm that your starting node can actually reach everything.

**References**
*James Peralta's*
**Coding Patterns: Breadth-First Search:** https://www.youtube.com/watch?v=bhD6NhLeQlQ
