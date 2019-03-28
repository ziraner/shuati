一般来说，iterator题目会要求实现hasNext和next两个函数

主函数逻辑放在hasNext中进行，next只进行输出处理，但是也要具体情况具体分析。

一般来说，如果iterator题目有原题，那么原题的写法应该是:

```
while Iterator.hasNext():
    ans.append(Iterator.next())
```

也就是说如果能对应到原题其实就是把循环拆开的过程，拆开之后把逻辑部分放进hashNext把输出部分放进next

