2025-06-01 

Tags: [[leetcode]] [[algorithms]] 

# **Two Pointers**

Two pointers is an algorithmic technique which uses two (or more) indices to traverse a data structure (often an array) usually used to solve a question optimally without using extra space. Depending on the problem, the pointers may move in the same direction, toward each other, or away from each other.

**Move same direction**: Common for linked list cycle detection or removing duplicates in arrays.

Code example:
```
def cycle_det(linkedlist):
	slow, fast = linkedlist.head, linkedlist.head
    while fast and fast.next:
		slow = slow.next
		fast = fast.next.next
		if slow == fast:
			return True

    return False
```

**Move toward the center**: Finding a pair of optimal elements in a sorted array.

Code example:
```
Assume sorted array
def two_sum(nums, target):
	n = len(nums)
	left, right = 0, n - 1
	while left < right:
		total = nums[left] + nums[right]
		if total == target:
			return [left, right]
		elif total < target:
			left += 1
		else:
			right -= 1
```

**Away from each other**: Checking palindromes.

Code example:
```
def is_palindrome(word):
	n = len(word)
	left, right = n // 2 - 1, n // 2 + 1
	if n % 2 == 0:
		left, right = n // 2 - 1, n // 2
	while left > 0 and right < n:
		if word[left] != word[right]:
			return False
		left -= 1
		right += 1
	return True
```



**References**
*James Peralta's* 
**Coding Patterns: Two Pointer:** https://www.youtube.com/watch?v=UF4vuE1ahII