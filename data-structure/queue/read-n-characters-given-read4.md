Read N Characters Given Read4 解题报告

The API:`int read4(char *buf)`reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the`read4`API, implement the function`int read(char *buf, int n)`that readsncharacters from the file.

**Note:**  
The`read`function will only be called once for each test case.

Idea:

用一个buf4作为q存储每次read进来的数

判断条件1.是否读不进来了2.是否读够了

```
# The read4 API is already defined for you.
# @param buf, a list of characters
# @return an integer
# def read4(buf):

class Solution(object):
    def read(self, buf, n):
        """
        :type buf: Destination buffer (List[str])
        :type n: Maximum number of characters to read (int)
        :rtype: The number of characters read (int)
        """
        i = 0
        buf4 = ['' for _ in xrange(4)]
        while i < n:
            size = read4(buf4)
            if size == 0:
                break
            j = 0
            while i < n and j < size:
                buf[i] = buf4[j]
                i += 1
                j += 1
        return i
```



