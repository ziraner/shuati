# Binary Search

二分法的本质是用O\(1\)的时间将T\(n\)的问题转化成T\(n/2\)的问题，进而时间复杂度为O\(logn\)

2. OOOXXX数组找边界：题目没有很明显的提示要用二分法，但是问题可以转换为一个OOOXXX的数组找O和X的边界
3. 二分答案：没有一个可以二分的数组，二分答案，找到满足某个条件的最大值/最小值

Two Templates:

基本二分法的模板


进阶的二分法模板

```python
def binarySearch(self, A):
    # 确定 start 和 end 的初始值
    start, end = ...
    # 跟精度有关的delta要取精度，跟整数有关的delta通常取1
    while start + delta < end:
        mid = (start + end) / 2
        # check函数检验当前解是否可行，二分答案时候根据情况写check函数
        if self.check(mid):
            start/end = mid
        else:
            end/start = mid
    if self.check(start):
        ...
    if self.check(end):
        ...
```
