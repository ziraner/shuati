Lintcode 437: Copy Books 解题报告

Given\_n\_books and the\_i\_th book has`A[i]`pages. You are given\_k\_people to copy the\_n\_books.

\_n\_books list in a row and each person can claim a continous range of the\_n\_books. For example one copier can copy the books from\_i\_th to\_j\_th continously, but he can not copy the 1st book, 2nd book and 4th book \(without 3rd book\).

They start copying books at the same time and they all cost 1 minute to copy 1 page of a book. What's the best strategy to assign books so that the slowest copier can finish at earliest time?

**Example**

Given array A =`[3,2,4]`, k =`2`.

Return`5`\( First person spends 5 minutes to copy book 1 and book 2 and second person spends 4 minutes to copy book 3. \)

Idea:

二分答案

```
class Solution:
    # @param pages: a list of integers
    # @param k: an integer
    # @return: an integer
    def copyBooks(self, pages, k):
        # write your code here
        if not pages:
            return 0
        start, end = max(pages), sum(pages)
        while start + 1 < end:
            mid = (start + end) / 2
            if self.check(pages, mid, k):
                end = mid
            else:
                start = mid
        if self.check(pages, start, k):
            return start
        return end
    def check(self, pages, t, k):
        copier, remain = 1, t
        for page in pages:
            if page > remain:
                copier += 1
                remain = t - page
            else:
                remain -= page
        return copier <= k
```



