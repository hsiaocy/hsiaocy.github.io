---
image:
  teaser: Python.jpeg

layout: article
title: Learn Python
date: 2020-07-15
categories: notes
author: chunyi_hsiao
tags: [Python]
share: true
---

In regard with the [LC #438](https://hsiaocy.github.io/leetcodes/notes/LeetCode-438/), I learned how different from collections.Counter() and dict()

```python
from collections import Counter, defaultdict 
x = 'abcabd'
cnt_x = Counter(x)
print(cnt_x, ',', type(cnt_x))
# Counter({'a': 2, 'b': 2, 'c': 1, 'd': 1}) , <class 'collections.Counter'>

dict_x = {}
for _x in x:
    if not dict_x.get(_x):
        dict_x.setdefault(_x, 1)
    else:
        dict_x[_x] += 1
print(dict_x, ',', type(dict_x))
# {'a': 2, 'b': 2, 'c': 1, 'd': 1} , <class 'dict'>
```
Similar outputs but totally different insides and processing.

As collections.Counter(x) returns its own 'collections.Counter' class, dict() return 'dict' class.

It will return **KeyError** if we want to calculate a value with an non-existed key in dict_x, but not for Counter()

```python
toBeAdd = 'e'

print(cnt_x)
# Counter({'a': 2, 'b': 2, 'c': 1, 'd': 1})
cnt_x[toBeAdd] -= 1
print(cnt_x)
# Counter({'a': 2, 'b': 2, 'c': 1, 'd': 1, 'e': -1})

print(dict_x)
dict_x[toBeAdd] -= 1
print(dict_x)
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# KeyError: 'e'
```

In this case, Counter() saving the condition written in the code makes it possible to calculate directly, instead setting the key and value needed before calculation like dict().

***Reference***  
[8.3. collections — Container datatypes](https://docs.python.org/3.3/library/collections.html#collections.defaultdict)  
[Python O(n) sliding window, DON'T need to compare Counter](https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/736141/Python-O(n)-sliding-window-DON'T-need-to-compare-Counter)
