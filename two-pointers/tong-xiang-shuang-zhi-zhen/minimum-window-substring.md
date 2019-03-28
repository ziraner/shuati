Minimum Window Substring 解题报告

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O\(n\).

For example,  
**S**=`"ADOBECODEBANC"`  
**T**=`"ABC"`

Minimum window is`"BANC"`.

**Note:**  
If there is no such window in S that covers all characters in T, return the empty string`""`.

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

Idea:

同向双指针问题。将target和source出现的char存进两个对应的dictionary中

对source进行同向双指针。遍历i--窗口的起点，每次移动j直到窗口可以cover target。然后更新窗口起点找到最小的长度同时更新source的dictionary

```
class Solution(object):
    from collections import defaultdict
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        s_dict, t_dict = defaultdict(int), defaultdict(int)
        for c in t:
            t_dict[c] += 1
        n, j = len(s), 0
        from sys import maxint
        ans, minWd = '', maxint
        for i in xrange(n):
            while j < n and not self.check(s_dict, t_dict):
                s_dict[s[j]] += 1
                j += 1
            if check(s_dict, t_dict):
                if minWd > j - i:
                    minWd = j - i
                    ans = s[i : j]
            s_dict[s[i]] -= 1
        return ans

        def check(self, s_dict, t_dict):
            for key in t_dict.keys():
                if key not in s_dict or s_dict[key] < t_dict[key]:
                    return False
            return True
```



