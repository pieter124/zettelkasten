2025-06-08 

Tags: [[leetcode]] [[algorithms]]

# **Greedy Algorithm**

A greedy algorithm is a simple algorithm used in optimization problems. The algorithm **picks the locally most optimal move at each step.** Greedy algorithms do not guarantee the best solution given the problem and are often used to give **heuristics** [^1] to **NP [^2] problems**. In simpler terms, depending on the problem, they are able to give the best solution and under other circumstances they give a good heuristic.

Let us consider the **knapsack problem:**
	Suppose you're a greedy thief. You're in a store with a knapsack, and there are all these items you can steal. But you can only take what you can fit in your knapsack. The knapsack can hold **35 pounds**.
		You are trying to **maximise the value** of the items you put in your knapsack. 
		The greedy algorithm is pretty simple:
			1. Pick the most expensive thing that will fit in your knapsack.
			2. Pick the next most expensive thing that will fit in your knapsack.
	The greedy algorithm doesn't give the optimal solution for this problem, sometimes it even gives poor results but sometimes it can get you close.



**References**
*Aditya Y. Bhargava's*
**Grokking Algorithms**

[^1]: **Heuristic:** a solution that is satisfactory rather than the absolute best.

[^2]: **NP (nondeterministic polynomial time)**: A class of decision problems where a "yes" solution can be verified in polynomial time.
