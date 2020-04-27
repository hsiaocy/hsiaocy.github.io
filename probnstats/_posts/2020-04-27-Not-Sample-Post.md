---
image:
  teaser: probnstats.jpg

layout: article
title: Leet Code Squares of a Sorted Array
date: 2019-02-05
categories: notes
author: chunyi_hsiao
tags: [Python, LeetCode]
share: true
---

- **Title**: #977 Squares of a Sorted Array
- **Diffculity**: Easy 
- **Description**: Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

Example: 

|nums = [-4, -1, 0, 3, 10], then return [0, 1, 9, 16, 100]|


My solution:
```python
class Solution:
    def sortedSquares(self, A: 'List[int]') -> 'List[int]':
        q = []
        [q.append(i**2) for i in A]
        return sorted(q)
        pass

```

- Runtime: **164 ms**, faster than **55.49%** of Python3 online submissions 
- Memory Usage: **12.2 MB**, less than **100.00%** of Python3 online 


**Ideas**: Square the integer in list then sort the list.
