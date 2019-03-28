Simplify Path

Given an absolute path for a file \(Unix-style\), simplify it.

For example,  
**path**=`"/home/"`, =&gt;`"/home"`  
**path**=`"/a/./b/../../c/"`, =&gt;`"/c"`  
**Corner Cases:**

* Did you consider the case where **path **= `"/../"`? In this case, you should return `"/"`.

* Another corner case is the path might contain multiple slashes`'/'`together, such as`"/home//foo/"`. In this case, you should ignore redundant slashes and return `"/home/foo"`.

Idea:

根据题目提示需要考虑的一些corner case为

//, ../, ./

先split\('/'\)如果遇到''或者'.'则什么都不做；如果遇到..则需要去掉之前的那个item，所以这里要用stack，pop掉之前的元素；其他情况压栈

最后返回的时候最前面要有一个/，其他的/链接stack中元素既可

```
class Solution(object):
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        stack = []
        for item in path.strip().split('/'):
            if item == '.':
                continue
            elif item == '..':
                if stack:
                    stack.pop()
            else:
                stack.append(item)
        return '/' + '/'.join(stack)
```



