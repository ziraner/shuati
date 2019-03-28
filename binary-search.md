# Binary Search

二分法的本质是用O\(1\)的时间将T\(n\)的问题转化成T\(n/2\)的问题，时间复杂度为O\(logn\)

1. 基本二分法：find first/last position of a number in a sorted array
2. OOOXXX数组找边界：题目没有很明显的提示要用二分法，但是问题可以转换为一个OOOXXX的数组找O和X的边界
3. 二分答案：没有一个可以二分的数组，二分答案，找到满足某个条件的最大值/最小值

Two Templates:

基本二分法的模板

```
def binarySearch(self, A):
    # 确定 start 和 end 的初始值
    start, end = ...
    # 写二分法时，相邻退出，避免死循环。和quicksort等题目的退出条件不大一样
    while start + 1 < end: 
        # python可以不用判断溢出，否则需要写成 mid = (end - start) / 2 + start，防止start和end很大相加溢出
        mid = (start + end) / 2
        # 比较A[mid]和target，判断应该丢掉哪一半；通常会把==合并在其中一个区间里面
        if A[mid] == target:
            ...
        elif A[mid] < target:
            start/end = mid
        else:
            end/start = mid
    # 退出时一定只有离target最近的两个点，判断取哪个点，start和end谁在前判断根据具体情况决定
    if A[start] ... target:
        ...
    if A[end] ... target:
        ...
```

进阶的二分法模板

```
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



