Course Schedule II 解题报告

There are a total ofncourses you have to take, labeled from`0`to`n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair:`[0,1]`

Given the total number of courses and a list of prerequisite**pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:

```
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is`[0,1]`

```
4, [[1,0],[2,0],[3,1],[3,2]]
```

There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is`[0,1,2,3]`. Another correct ordering is`[0,2,1,3]`.



Idea:

这个题目和I的区别在于要输出上课的顺序。用ans数组记录pop出来的数，最后比较ans的lengh和courseNums如果相等则输出，如果不等说明不能够上完课，则输出空数组

```py
class Solution(object):
    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        graph = [[] for _ in xrange(numCourses)]
        indegree = [0 for _ in xrange(numCourses)]
        q = []
        for u, v in prerequisites:
            indegree[u] += 1
            graph[v].append(u)
        for i in xrange(numCourses):
            if indegree[i] == 0:
                q.append(i)
        ans = []
        while q:
            tmp = q.pop(0)
            ans.append(tmp)
            for neighbor in graph[tmp]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    q.append(neighbor)
        if len(ans) == numCourses:
            return ans
        return []
```

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {        
        Map<Integer, Integer> indegree = new HashMap<>();
        Map<Integer, Set<Integer>> graph = new HashMap<>();

        for (int[] prereq: prerequisites) {
            int count = indegree.containsKey(prereq[0]) ? indegree.get(prereq[0]) : 0;
            indegree.put(prereq[0], count + 1);

            if (!graph.containsKey(prereq[1])) {
                graph.put(prereq[1], new HashSet<>());
            }
            graph.get(prereq[1]).add(prereq[0]);
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (!indegree.containsKey(i)) {
                queue.offer(i);
            }
        }

        int pollTimes = 0;
        int[] result = new int[numCourses];
        while (!queue.isEmpty()) {
            int element = queue.poll();
            result[pollTimes] = element;
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

        if (pollTimes == numCourses) {
            return result;
        }
        return new int[0];
    }
}
```
