Read N Characters Given Read4 II - Call multiple times 解题报告

The API:`int read4(char *buf)`reads 4 characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the`read4`API, implement the function`int read(char *buf, int n)`that readsncharacters from the file.

**Note:**  
The`read`function may be called multiple times.

Idea:

需要定义类变量记录读在哪里了，这里定义了一个head和tail

如果head == tail则可以继续读，如果不相等需要把上次剩的写进buf先

```
# The read4 API is already defined for you.
# @param buf, a list of characters
# @return an integer
# def read4(buf):

class Solution(object):
    def __init__(self, ):
        self.head = 0
        self.tail = 0
        self.buf4 = ['' for _ in xrange(4)]
    def read(self, buf, n):
        """
        :type buf: Destination buffer (List[str])
        :type n: Maximum number of characters to read (int)
        :rtype: The number of characters read (int)
        """
        i = 0
        while i < n:
            if self.head == self.tail:
                self.head = 0
                self.tail = read4(self.buf4)
                if self.tail == 0:
                    break
            while i < n and self.head < self.tail:
                buf[i] = self.buf4[self.head]
                i += 1
                self.head += 1
        return i
```



