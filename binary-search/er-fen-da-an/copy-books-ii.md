Lintcode 438: Copy Books II  解题报告

Given n books\( the page number of each book is the same\) and an array of integer with size k means k people to copy the book and the i th integer is the time i th person to copy one book\). You must distribute the continuous id books to one people to copy. \(You can give book A\[1\],A\[2\] to one people, but you cannot give book A\[1\], A\[3\] to one people, because book A\[1\] and A\[3\] is not continuous.\) Return the number of smallest minutes need to copy all the books.

**Example**

Given n =`4`, array A =`[3,2,4]`, .

Return`4`\( First person spends 3 minutes to copy book 1, Second person spends 4 minutes to copy book 2 and 3, Third person spends 4 minutes to copy book 4. \)

Idea:

二分答案

```
class Solution:
    """
    @param: n: An integer
    @param: times: an array of integers
    @return: an integer
    """
    def copyBooksII(self, n, times):
        # write your code here
        if not times:
            return 0
        start, end = 0, max(times) * n
        while start + 1 < end:
            mid = (start + end) / 2
            if self.check(n, times, mid):
                end = mid
            else:
                start = mid
        if self.check(n, times, start):
            return start
        return end
    def check(self, n, times, minute):
        books = 0
        for time in times:
            books += minute / time
        return books >= n
```



