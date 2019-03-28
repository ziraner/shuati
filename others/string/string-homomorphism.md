String Homomorphism

Given two strings**s**and**t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

  
**Example**

Given s =`"egg"`, t =`"add"`, return`true`.

Given s =`"foo"`, t =`"bar"`, return`false`.

Given s =`"paper"`, t =`"title"`, return`true`.

  
这个题是一个一一映射，需要建两个map，map过来且map过去都是唯一的

```
class Solution:
    """
    @param: s: a string
    @param: t: a string
    @return: true if the characters in s can be replaced to get t or false
    """
    def isIsomorphic(self, s, t):
        # write your code here
        map1 = {}
        map2 = {}
        if len(s) != len(t):
            return False
        n = len(s)
        for i in xrange(n):
            if s[i] not in map1:
                map1[s[i]] = t[i]
            else:
                if t[i] != map1[s[i]]:
                    return False
            
            if t[i] not in map2:
                map2[t[i]] = s[i]
            else:
                if s[i] != map2[t[i]]:
                    return False
        return True
```



