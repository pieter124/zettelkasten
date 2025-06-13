2025-06-13 

Tags: [[data structures]] [[computer science]] [[mathematics]] 

# **Graphs**

To grasp the idea:

Imagine a small town, with some houses and some roads between them.

A **node** (or **vertex**) represents a single house.

An **edge** represents a road, a connection between nodes.

A **graph** is the town itself.

Two nodes are **adjacent** if there's an edge between them. Alternatively, those two nodes are **neighbours**.

A **path** between two nodes is a list of adjacent nodes leading from one node to another.

Nodes are also **not allowed to repeat** on the path. So B -> A -> C -> D -> A is not a path as A **repeats**.

A **cycle** is a path that starts and ends at the same node. For example, A -> C -> D -> A is a cycle.

Two nodes are **connected** if there's at least one path between them. Note that connectivity is **transitive**.

A **connected component** is a **maximal**[^1] group of nodes that are all connected to each other.

Graphs can be **directed** or **undirected**. If a graph is directed, its edges point from one node to another. In a directed graph, a node X can **reach** another node Y if there's a path from X to Y.

Graphs can also be **weighted** or **unweighted**. In a weighted graph, each edge has a weight associated with it.

A **simple** graph has no duplicate edges 

A **complete** graph has every node adjacent to every other node. Every possible edge exists.

A **connected** graph has only 1 connected component. So every node is connected to every other node.

An **acyclic** graph has no cycles (also known as a **forest**).

**Adjacency Matrices** are used to check if two nodes are adjacent by storing whether there exists an edge between two nodes. But it's O(v ^ 2) in memory (v = number of vertices), which is just infeasible for many graph problems.

**Adjacency List** stores a list of each nodes' neighbours. This is usually an array of lists.
For checking if two nodes are adjacent, it can be O(e) where e is the number of edges. or O(log e) if you use a set, so a matrix is better.

But it's O(v + e) in memory (v = number of vertices), which can be must better than the matrix, and you can iterate over all neighbours in just O(number of neighbours) instead of O(v) with the matrix.

This works for basically every graph problem, probably would be used for everything.



**References**
*Colin Galen's*
**Fundamental Graphs Knowledge:** https://www.youtube.com/watch?v=awqss7Kjt2Y

[^1]: Maximal: If a node is able to be in the component, then it must be.
