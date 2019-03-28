图的拓补排序可能是有向图的唯一考察点

数据结构

一个q

一个图的表达方式（要么是一个存边edges的list要么是一个图的adjacency list）

一个indegree hashmap

实现方法

1算出图中每个node的indegree保存在indegree hashmap中

2把所有indegree为0的进queue

3bfs q中的node，把跟该node相邻的node的indegree都减一，然后把indegree为0的都入队列

应用

一般不会裸考拓补排序

一切跟stuff先后顺序有紧密关联的题目都可以考虑一下拓补排序

比如说上课的先后顺序：course schedule I & II

比如说字符串中字符的先后顺序sequence reconstruction

比如说字典中单词（字母）的先后顺序alien dictionary

