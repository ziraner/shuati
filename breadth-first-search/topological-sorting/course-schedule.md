Course Schedule 解题报告

There are a total ofncourses you have to take, labeled from`0`to`n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair:`[0,1]`

Given the total number of courses and a list of prerequisite**pairs**, is it possible for you to finish all courses?

For example:

```
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

```
2, [[1,0],[0,1]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

Idea:

这个题目可以用数组表示indegree和graph因为每个数字只能对应一个点且数字连续，可以建一整块的数组表示。如果不连续或者一个数字对应多个node的话需要用hashmap表示graph和indegree

1.根据edges变量构造出graph的adjacency list和indegree两个数组。  
2.将indegree为0的先入q  
3.对graph按照indegree做BFS，将indegree减少到0的node入列，统计pop的数目和最后的numCourses对比

```py
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        if numCourses == 0 or not prerequisites:
            return True
        indegree = [0 for _ in xrange(numCourses)]
        graph = [[] for _ in xrange(numCourses)]
        q = []
        for u, v in prerequisites:
            indegree[u] += 1
            graph[v].append(u)
        for i in xrange(numCourses):
            if indegree[i] == 0:
                q.append(i)
        cnt = 0
        while q:
            tmp = q.pop(0)
            cnt += 1
            for course in graph[tmp]:
                indegree[course] -= 1
                if indegree[course] == 0:
                    q.append(course)
        return cnt == numCourses
```

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses == 0 || prerequisites == null || prerequisites.length == 0) {
            return true;
        }

        Map<Integer, Integer> indegree = new HashMap<>();
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int[] prerequisite: prerequisites) {
            int count = indegree.containsKey(prerequisite[0]) ? indegree.get(prerequisite[0]) : 0;
            indegree.put(prerequisite[0], count + 1);

            if (!graph.containsKey(prerequisite[1])) {
                graph.put(prerequisite[1], new HashSet<>());
            }
            graph.get(prerequisite[1]).add(prerequisite[0]);    
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (!indegree.containsKey(i)) {
                queue.offer(i);
            }
        }

        int pollTimes = 0;
        while(!queue.isEmpty()) {
            int element = queue.poll();
            pollTimes++;
            if (!graph.containsKey(element)) {
                continue;
            }
            for (int neighbor: graph.get(element)) {
                int count = indegree.get(neighbor);
                if (count == 1) {
                    queue.offer(neighbor);
                }
                indegree.put(neighbor, count - 1);
            }
        }

        return pollTimes == numCourses;
    }
}
```
