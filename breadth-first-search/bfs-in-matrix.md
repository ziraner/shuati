bfs in matrix:

基本上都是简单图的bfs

如果return是true/false那么维持一个二位数组boolean[][] visited记录当前点有没有被访问过。

如果return是distance那么维持一个二位数组int[][] distances初始化为-1既可以记录当前distance又可以记录有没有被访问过。

matrix当中的bfs一般来说不需要固定size进行for循环因为已经有一个二维矩阵记录当前visited/distance。
