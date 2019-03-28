BFS in Tree: 每次扩展的时候是node的左儿子和右儿子；一般来说一个q就OK，看情况建hashmap

BFS in Graph:每次扩展的时候是node的联通neighbors；一般来说需要建hashmap保存访问过的点

BFS in Matrix:每次扩展的时候是上下左右数组 delta = \[\[0, 1\], \[0, -1\], \[-1, 0\], \[1, 0\]\]；一般来说需要建hashmap保存访问过的点，但是也可以直接在数组中改某些特殊值代表访问过

