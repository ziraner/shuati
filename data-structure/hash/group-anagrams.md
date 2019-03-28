Group Anagrams 解题报告

Given an array of strings, group anagrams together.

For example, given:`["eat", "tea", "tan", "ate", "nat", "bat"]`,  
Return:

```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**All inputs will be in lower-case.

Idea:

把每个单词转换成list，排序，将新的单词作为key保存在hashmap中

最后遍历hashmap将每个key对应的单词输出

```
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        hm = {}
        for word in strs:
            word_list = list(word)
            word_list.sort()
            new_word = ''.join(word_list)
            if new_word not in hm:
                hm[new_word] = [word]
            else:
                hm[new_word].append(word)
        ans = []
        for key in hm.keys():
            ans.append(hm[key][:])
        return ans
```

  


