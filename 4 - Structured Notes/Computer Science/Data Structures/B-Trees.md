2025-06-10 

Tags: [[data structures]] [[computer science]]

# **B-Trees**

A B-Tree is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions and deletions in logarithmic time.

The idea behind a B-tree is to store a tree with nodes that can hold more than one key.
If our search key is less than all of the keys, we look to the left most child. If our search key is greater than all of the keys, we look to the right most child. Otherwise depending on where the search key falls between in the number of keys stored at the parent node, we look at the child in between those two keys.

B-trees optimize data storage by allowing nodes to hold multiple keys, enhancing search performance.

**Rules of B-trees:**
- The leaves of the B-tree have to be at the same level of the tree. We are not allowed to have some leaves deeper in the tree than others.
- Every node has a maximum and a minimum number of keys. The minimum is always half of the maximum number of keys (truncated).

**Insertion into a B-tree:**
The root node is the only exception to the number of keys required for a node. Each time we add a key to the root node, it gets added in sorted order. If we add a key that results in the maximum being exceeded, we need to split the node up. Because each node needs a minimum of $\large\frac{max}{2}$ nodes, assuming we have a maximum of 4 keys and we try adding a 5th to the root node, we take the two smallest keys and make one node and take the two largest and make another node. The middle value becomes the new root that points to the left and right nodes we had just made.

When we add a new element, we always add them at the bottom level of the B-tree. So when a new element comes along, we use the root node to decide which node to visit next and then insert the key at the appropriate spot at the bottom level.

**Now we have to handle the case where we completely fill up a node and then try to add a new key there:**

We perform the same 'split' procedure and push the middle value up to the root.

**But what if the parent/root node becomes full as well?**

Due to the recursive nature of the 'split procedure', this case is handled elegantly whilst keeping the properties of the B-tree.

**Deletion from a B-tree:**

Let's say there is a key we want to delete; we start by searching through the tree as usual, once we find it, we can just remove it from the node.

**What happens if we try to delete a key from a node that has the minimum key count?**
This is not allowed. So the *naive* workaround would be to take a key from the sibling node next to it, so the smallest from the right and the largest from the left node.

But we can't just take the key from the sibling and fill in the missing spot in our node,
because that would make the parent key in between these two nodes wrong. 

So instead of taking the key from our sibling node, we let that key become part of the parent keys and take the parent key separating our node and the sibling as our new key to preserve the rules.

**But what happens if our sibling nodes are also already at the minimum?**

We can merge our node, our *separator* (the parent key) and the sibling node into a single full node.
 
**Yet another edge case... What if the parent node has too few keys?**

The recursive nature of this 'merge' procedure handles this as well.

**What happens if we delete a key from the middle of the tree rather than from a leaf?**

In this case, we need a new separator which needs to be greater than everything in the left subtree and smaller than everything in the right subtree. So we have two options for the new separator:
- Take the largest value from the left subtree.
- Take the smallest value from the right subtree.

It is also possible that the node we took the key from will now not meet the minimum amount of keys required. But we know how to handle this case now.

This data structure is frequently seen in databases and file systems due to their searching efficiency.

**References**
*Wikipedia's*
**B-tree:**
https://en.wikipedia.org/wiki/B-tree

*Spanning Tree's*
**Understanding B-Trees: The Data Structure Behind Modern Databases:**
https://www.youtube.com/watch?v=K1a2Bk8NrYQ