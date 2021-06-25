graph的表示数据结构：
adjacencyList: Map<Node, Set<Node>>
if Node is non-duplicate Integer, then Map<Integer, Set<Integer>>, potentially becomes List<Set<Integer>>

bfs in graph:
graph本身的ajacencyList + 
Queue + Set<Node>去保存访问过的点，因为跟树相比图可能存在环，有多次被访问到的情形发生。
