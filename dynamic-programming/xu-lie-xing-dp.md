坐标型/序列型DP包括1维2维

一般来说定义：

1维f\[i\]表示0到i XXXX（不需要多定义一位），或者表示前i个数XXXX（需要多定义一位）  
2维f\[i\]\[j\]表示到\(i, j\)咋地咋地，或者以i,j 为末尾咋地咋地。

一般都可以优化空间：

1维可以优化到O\(1\)的space  
2维滚动数组优化到O\(n\)的space

一般来说初始化：

1维初始化前1个或者前几个数  
2维初始化第一行和第一列

一般来说返回：

1维f\[n - 1\]或者f\[n\]  
2维f\[m\]\[n\]或者f\[m - 1\]\[n - 1\]
