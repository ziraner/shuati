记忆化搜索：一般来说从大到小搜索。先从一个特别大的状态去搜，然后一点一点递归往小了搜。一般来说画一个搜索树，可以很清晰的做出来

什么时候用记忆化搜索：  
1。初始状态不是很容易确定，比方说滑雪问题  
2。状态转移不是那种从小到大的，有可能是有些从大到小有些从小到大，也有可能根本不知道。

咋记忆化搜索：  
1。定义dp矩阵，一般来说还要定义一个flag矩阵判断当前点是否被遍历过了。  
2。带着dp矩阵和flag矩阵做DFS，如果被访问过直接返回dp矩阵中的值。

区间类DP特点：

1. 求一段区间的解max/min/count

2. 转移方程通过区间更新

3. 从大到小的更新



