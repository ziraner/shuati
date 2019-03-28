Merge Sorted Array 解题报告

Given two sorted integer arraysnums1andnums2, mergenums2intonums1as one sorted array.

**Note:**  
You may assume thatnums1has enough space \(size that is greater or equal tom+n\) to hold additional elements fromnums2. The number of elements initialized innums1andnums2aremandnrespectively.

Idea:

从大到小合并。最后只需要检验j无需检验i

```
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        i, j, k = m - 1, n - 1, m + n - 1
        while i >= 0 and j >= 0:
            if nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                i -= 1
            else:
                nums1[k] = nums2[j]
                j -= 1
            k -= 1
        while j >= 0:
            nums1[k] = nums2[j]
            k -= 1
            j -= 1
```



