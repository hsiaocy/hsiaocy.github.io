---
image:
  teaser: Leetcode.jpg

layout: article
title: Leet Code Two Sum
date: 2019-02-05
categories: notes
author: chunyi_hsiao
tags: [Python, LeetCode]
share: true
---

- **Title**: #1 Two Sum
- **Diffculity**: Easy 
- **Description**: Given an array of integer and returned two indexes of two numbers that they add up to a specific target.

Example: 

|nums = [2, 7, 11, 15], target = 9, then return [0, 1]|


My solution-1:
```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        l = len(nums)
        for i, j in enumerate(nums):            
            a = target - j
            ii = i
            while True:
                ii += 1
                if ii < l:
                    if a == nums[ii]:
                        return [i, ii]
                    
                elif ii >= l:
                    break
```
- Runtime: **4540  ms**
- Memory Usage: **7.2 MB**


[Solution-2](https://leetcode.com/problems/two-sum/discuss/231600/Simple-Python-solution.-36ms-faster-than-99.75):
```python
        seen = {}
        for i, j in enumerate(nums):
            if (target - j) in seen:
                return [seen[target - j], i]
            else:
                seen[j] = i
        else:
            return []
```
- Runtime: **4540  ms**, faster than **99.75%** of Python3 online submissions
- Memory Usage: **7.2 MB**, less than **62.13%** of Python3 online 

**Ideas**: Obtain the difference then find it in the list. If not, start again from the second number.


Reference:
1. [LeetCode Discussion by awrogers14](https://leetcode.com/problems/two-sum/discuss/231600/Simple-Python-solution.-36ms-faster-than-99.75)


