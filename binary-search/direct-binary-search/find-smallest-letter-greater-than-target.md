Lintcode 1056: Find Smallest Letter Greater Than Target

**Problem:**

Given a list of sorted characters `letters` containing only lowercase letters, and given a target letter `target`, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is `target = 'z'` and `letters = ['a', 'b']`, the answer is`'a'`.

**Examples:**

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output:"f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output:"j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output:"c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output:"c"
```

**Idea:**

LinkedIn高频。面试时候不会告诉corner case，要自己问清楚比如字符大于等于最后一个字符怎么办

Solution:

```python
class Solution(object):
    def nextGreatestLetter(self, letters, target):
        """
        :type letters: List[str]
        :type target: str
        :rtype: str
        """
        start, end = 0, len(letters) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if letters[mid] <= target:
                start = mid
            else:
                end = mid
        if letters[start] > target:
            return letters[start]
        if letters[end] > target:
            return letters[end]
        return letters[0]
```
