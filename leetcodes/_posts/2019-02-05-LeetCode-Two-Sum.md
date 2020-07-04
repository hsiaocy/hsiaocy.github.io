---
image:
  teaser: leetcodes.jpg

layout: article
title: LeetCode - 1
date: 2020-03-08
categories: notes
author: chunyi_hsiao
tags: [Programming]
share: true
---
# #1 Two Sum ![Leetcode](https://img.shields.io/badge/Easy-Leetcode-green.svg)

- **Description**: Given an array of integer and returned two indexes of two numbers that they add up to a specific target.

- **Example**: 
|nums = [2, 7, 11, 15], target = 9, then return [0, 1]|

- **Explanation**: Obtain the difference then find it in the list. If not, start again from the second number.

Solution-1:
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // if (nums == [])
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i=0; i<nums.length; i++){
            if (map.containsKey(target - nums[i])){
                return new int [] { map.get(target - nums[i]), i};
            }
            map.put(nums[i], i);
        }
        return null;
    }
}
```
- Time&Space Complexity: $$O(n), O(n)$$

Solution-2:
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        k = 0
        res = {}
        for i in range(len(nums)):
            k = target - nums[i]
            if k in res:
                return [res.get(k), i]
            res[nums[i]] = i
```
- Time&Space Complexity: $$O(n), O(n)$$


[Solution-2](https://leetcode.com/problems/two-sum/discuss/231600/Simple-Python-solution.-36ms-faster-than-99.75):
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        ''' We can alternatively use "enumerate" to try...'''
        seen = {}
        for i, j in enumerate(nums):
            if (target - j) in seen:
                return [seen[target - j], i]
            else:
                seen[j] = i
```
- Time&Space Complexity: $$O(n), O(n)$$



Reference:
1. [LeetCode Discussion by awrogers14](https://leetcode.com/problems/two-sum/discuss/231600/Simple-Python-solution.-36ms-faster-than-99.75)


