Lintcode 63: Search in Rotated Sorted Array II 解题报告

Follow up for Search in Rotated Sorted Array

What if**duplicates**are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.

Idea:

有重复的直接loop

```
class Solution:
    """
    @param A : an integer ratated sorted array and duplicates are allowed
    @param target : an integer to be searched
    @return : a boolean
    """
    def search(self, A, target):
        # write your code here
        for a in A:
            if a == target:
                return True
        return False
```



