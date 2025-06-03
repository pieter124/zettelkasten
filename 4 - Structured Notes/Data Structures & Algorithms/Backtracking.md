2025-06-02 

Tags: [[leetcode]] [[algorithms]]

# **Backtracking**

Backtracking is essentially **brute forcing** a problem. Conceptually, one can imagine the procedure of backtracking as a **tree traversal on a decision tree** - we take a path towards a solution and then "back track" and try another path in the tree as soon as we determine that the current path cannot lead to a valid solution or reach a base case.

Almost the same as **[[Depth-First Search]]** but we have the backtrack step.

Tips for identifying backtracking:
- Question has **"generate all"**.
- You need to search all paths for a solution.

Most backtracking questions have the same boiler plate:
1. Base cases
2. Add choice to solution
3. Recurse
4. Undo/Revert choice from solution (backtrack)

**Common Pitfalls**:
- Ensuring you "undo" the state correctly on each backtrack.
- Not handling base case.

**References**
*James Peralta's*
**Coding Patterns: Backtracking:** https://www.youtube.com/watch?v=H12S1xeQyxA