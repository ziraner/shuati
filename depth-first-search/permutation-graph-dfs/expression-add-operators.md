Expression Add Operators 解题报告

Given a string that contains only digits`0-9`and a target value, return all possibilities to add **binary **operators \(not unary\)`+`,`-`, or`*`between the digits so they evaluate to the target value.

Examples:

```
"123", 6 -> ["1+2+3", "1*2*3"] 
"232", 8 -> ["2*3+2", "2+3*2"]
"105", 5 -> ["1*0+5","10-5"]
"00", 0 -> ["0+0", "0-0", "0*0"]
"3456237490", 9191 -> []
```

Idea:

需要新引入两个变量val & lastF

DFS乘法的时候 新的val = val - lastF + lastF \* num; 新的lastF = lastF \* num

DFS加法的时候 新的val = val + num; 新的lastF = num

DFS减法的时候 新的val = val - num; 新的lastF = -num

注意corner case是05不是一个valid的数所以要加条件剔除这种情况；另外的Corner case是开始的第一个数

```
class Solution(object):
    def addOperators(self, num, target):
        """
        :type num: str
        :type target: int
        :rtype: List[str]
        """
        self.num = num
        self.target = target
        eq, ans = '', []
        self.helper(0, 0, 0, eq, ans)
        return ans
    def helper(self, pos, lastF, val, eq, ans):
        if pos == len(self.num):
            if val == self.target:
                ans.append(eq)
            return
        for i in xrange(pos, len(self.num)):
            if i != pos and self.num[pos] == '0':
                break
            num = int(self.num[pos: i + 1])
            if pos == 0:
                self.helper(i + 1, num, num, "%s" % num, ans)
            else:
                self.helper(i + 1, num, val + num, eq + "+%d" % num, ans)
                self.helper(i + 1, -num, val - num, eq + "-%d" % num, ans)
                self.helper(i + 1, lastF * num, val - lastF + lastF * num, \
                           eq + "*%s" % num, ans)
```



