Topological Sorting 解题报告

Given an directed graph, a topological order of the graph nodes is defined as follow:

* For each directed edge`A -> B`in graph, A must before B in the order list.
* The first node in the order can be any node in the graph with no nodes direct to it.

Find any topological order for the given graph.

##### Notice

You can assume that there is at least one topological order in the graph.

**Example**

For graph as follow:

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThE9AgZZszyhwe0o9qpp3VyizdIj9kWwMY50HiQEysXvkSLsoZ "picture")

The topological order can be:

```
[0, 1, 2, 3, 4, 5]
[0, 2, 3, 1, 5, 4]
...
```

Idea:  
拓补排序可能是面试考的为数不多有向图题目的热门。构造一个indegree的hashmap记录每个node的indegree，没有在hashmap中的node即为indegree为0的node；BFS的时候每加入一个q中node的neighbor，将该node的indegree减一；将indegree减为0的node加入q
