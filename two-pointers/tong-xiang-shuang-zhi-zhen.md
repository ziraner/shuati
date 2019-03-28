同向双指针模板：

```
for i in xrange(n):
    while j < n:
        # 有时候也可以把if写在while中
        if 满足条件:
            j += 1
            更新j状态
        else:
            break
    更新i状态
```



