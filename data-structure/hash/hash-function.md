Hash Function 解题报告

In data structure Hash, hash function is used to convert a string\(or any other type\) into an integer smaller than hash size and bigger or equal to zero. The objective of designing a hash function is to "hash" the key as unreasonable as possible. A good hash function can avoid collision as less as possible. A widely used hash function algorithm is using a magic number 33, consider any string as a 33 based big integer like follow:

hashcode\("abcd"\) = \(ascii\(a\) \* 333+ ascii\(b\) \* 332+ ascii\(c\) \*33 + ascii\(d\)\) % HASH\_SIZE

```
                          = \(97\* 333+ 98 \* 332 + 99 \* 33 +100\) % HASH\_SIZE

                          = 3595978 % HASH\_SIZE
```

here HASH\_SIZE is the capacity of the hash table \(you can assume a hash table is like an array with index 0 ~ HASH\_SIZE-1\).

Given a string as a key and the size of hash table, return the hash value of this key.f

**Clarification**

For this problem, you are not necessary to design your own hash algorithm or consider any collision issue, you just need to implement the algorithm as described

**Example**

For key="abcd" and size=100, return 78

Idea:

这个题是一个特别基本的写hash function的实现。注意判断ans小于0的情况，防止越界。

```
class Solution:
    """
    @param key: A String you should hash
    @param HASH_SIZE: An integer
    @return an integer
    """
    def hashCode(self, key, HASH_SIZE):
        # write your code here
        ans = 0
        for i in xrange(len(key)):
            ans = (ans * 33 + ord(key[i])) % HASH_SIZE
            if ans < 0:
                ans += HASH_SIZE
        return ans
```



