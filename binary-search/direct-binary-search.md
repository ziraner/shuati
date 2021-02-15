直接使用二分法\
the question will directly tell you to find first/last position of a number in a sorted array

Template
```python
def binarySearch(self, A):
    # 确定 start 和 end 的初始值
    start, end = ...
    # 写二分法题目时，相邻退出，避免死循环
    # 和quicksort等题目的退出条件不一样
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
