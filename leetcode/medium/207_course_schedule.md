# 207 Course Schedule

**Medium**

There are a total of `numCourses` courses you have to take, labeled from 0 to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

- For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return true if you can finish all courses. Otherwise, return `false`.

## Concept

This is a recursive DFS problem.

The idea is to be able to cycle detect. Using `prerequisites`, we can make a map where the key is the course and the values are the courses that need to be completed to complete that course. To detect if a course is achievable, we check if there are cycles in the current course's prerequisites.

## Code

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:

        # Getting mapping of course: [prereq1, prereq2, ...]
        preMap = {i:[] for i in range }
        for crs, pre in prerequisites:
            preMap[crs].append(pre)

        # To prevent cycles
        visit = set()

        def dfs(crs):

            # If the course has already been seen in the current traversal
            if crs in visit: return False

            # If the course has no prerequisites, then it is completeable
            if not preMap[crs]: return True

            visit.add(crs)
            # Run recursion on all prerequisites. If one of the prerequisite is unachievable starting at crs, then it False
            for pre in preMap[crs]:
                if not dfs(pre): return False

            visit.remove(crs)
            preMap[crs] = []

            return True

        for crs in range(numCourses):
            if not dfs(crs): return False

        return True
```
