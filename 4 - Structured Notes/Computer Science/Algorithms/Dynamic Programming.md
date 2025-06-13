2025-06-07 

Tags: [[leetcode]] [[algorithms]]

# **Dynamic Programming**

**What is "Dynamic Programming"?**

At the starting level, "**Dynamic Programming (DP)**"  is mostly just recursion (brute force) with a few optimisations. We will save time by not doing the same thing multiple times by discarding useless information.

**Iterative Approach:**
When solving a dynamic programming problem, considering the order of iteration is important when computing the sub-problems' correct output.  Essentially, when processing a node, make sure that the nodes that it depends on have also been processed.

**Recursive Approach:**
We use **memoization** to store previously computed sub-problems to avoid re-computing the same sub-problem if required.

You can change from recursive to iterative pretty easily, below is an example:
![[Pasted image 20250607171802.png]]

**Time complexity** would be the **size of the input rather than the amount of permutations.**

**Clarifying on vocabulary:**
- **States:** Represents the value(s) that the discarded information was compressed to, and also represents the subproblems we solve to build up to the main problem. 
- **Transitions:** Represent the way states interact with each other.
- **Base cases:** Similar to recursion. The easiest states, for which we immediately know the answers to. 
- **Pull DP:** "Pull" answers from previous DP values (our recursive solution). AKA Top-Down.
- **Push DP:** "Push" our answers to future DP values (our iterative solution). AKA Bottom-Up.

In the grid example in *Colin Galen's Video*, the iterative method's transitions are pushing the answers to the downward and rightward cells: 
	dp(r +1, c) += dp(r, c);
	dp(r, c + 1) += dp(r, c);

The recursive transitions are given by the formula: 
	dp(r, c) = dp(r - 1, c) + dp(r, c - 1);
	

Recursive DP can **only be pull DP.** If we try push DP, we can run into the order of iteration issue mentioned earlier.

For pull DP recursively, the order of iteration doesn't matter. If we don't have the answer for some state, we can just compute that answer recursively, then use that answer where it's needed. 

For iterative pull DP, the answers we pull need to be complete. The **order of iteration always matters** for any iterative DP.

**How does it differ from [[Greedy Algorithm]]?**

**Similarities:**
- They are both used to solve optimization problems.

**Differences:**
- Greedy algorithm takes the **local optimal choice** at each step, doesn't always guarantee the best overall result, whereas Dynamic Programming **guarantees the most optimal solution by principle of optimality**.

What is the **principle of optimality?**
The principle of optimality is a fundamental aspect of dynamic programming, which states that the optimal solution to a dynamic optimization problem can be found by **combining the optimal solutions to its sub-problems**.

Let us revisit the **knapsack problem** ([[Greedy Algorithm]]):
	You're a thief with a knapsack that can carry **4 lbs** of goods.
	You have three items that you can put into the knapsack:
		1. Stereo -> $3000 -> 4 lbs.
		2. Laptop -> $2000 -> 3 lbs.
		3. Guitar -> $1500 -> 1 lbs.
	Dynamic programming stats by solving subproblems and builds up to solving the big problem. For the knapsack problem, you'll start by solving the problem for smaller knapsacks and then work up to solving the original problem.

Every dynamic problem algorithm starts with a grid. Here's a grid for the knapsack problem:

![[Pasted image 20250609225203.png]]
The rows of the grid are the items, and the columns are knapsack weights from 1 lbs to 4 lbs. You need all of those columns because they will help you calculate the value of the sub-knapsacks. 
The grid starts out empty. You're going to fill in each cell of the grid. Once the grid is filled in, you'll have your answer to this problem. 

Start with the first row:
	This is the *guitar* row, which means you're trying to fit the guitar into the knapsack. At each cell, there's a simple decision: Do you steal the guitar or not? 
	The first cell has a knapsack of capacity 1 lbs. The guitar is also 1 lbs so it can fit into the knapsack. This means the value of this cell is $1,500 and it contains a guitar.
	This is what the first row looks like after computing all the cells:

![[Pasted image 20250609225559.png]]

Let's do the next row:
	Now that you're on the second row, you can steal the stereo or the guitar. At every row, you can either steal the item at that row or the items in the rows above it. So you can't choose to steal the laptop right now, but you can steal the stereo and/or the guitar. Let's start with the first cell, a knapsack of capacity 1 lbs. The current max value you can fit into a knapsack of 1 lbs is $1,500. 
	You have a knapsack of capacity of 1 lbs. Will the stereo fit in there? Nope, it's too heavy. Because you can't fit the stereo, $1,500 remains the max guess for a 1 lbs knapsack. This continues for the next 2 cells. 
	

What if you have a knapsack of capacity 4 lbs? The stereo finally fits. The old max value was $1,500, but if you put the stereo in there instead, the value is $3,000! Let's take the stereo.
![[Pasted image 20250609231706.png]]

Now for the final row:
	As the laptop weighs 3 lbs, the first 2 cells stay the same and the third cell gets updated to $2,000 as the laptop cost more than the guitar. At 4 lbs, the current estimate is $3,000. You can put the laptop in the knapsack, but it's only worth $2,000.
	But we can fit in both the laptop and the guitar which would give us the maximum value of $3,500.
The formula used here is:
```
cell[i][j] = max(cell[i-1][j], current_item + cell[i - 1][j - item's weight])
```

Here is the final grid:
![[Pasted image 20250610000343.png]]
	
**References**
*Colin Galen's*
**A Deep Understanding of Dynamic Programming:
https://www.youtube.com/watch?v=Clp5c7HvLqs

*Abdul Bari's*
**4 Principle of Optimality - Dynamic Programming introduction:**
https://www.youtube.com/watch?v=5dRGRueKU3M

*arxiv.org's*
**The Principle of Optimality in Dynamic Programming:**
https://arxiv.org/abs/2302.08467

*Aditya Y. Bhargava's*
**Grokking Algorithms**
