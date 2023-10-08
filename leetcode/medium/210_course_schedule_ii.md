# 210 Course Schedule II

**Medium**

There are a total of `numCourses` courses you have to take, labeled from 0 to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course bi first if you want to take course ai.

- For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

## Concept

The question teaches about topolocial sort.

Using a direct graph setup, go through each course and see if it leads to an end `node` or in this question a course without any prerequisites. Its very similar to **Course Schedule** but every time you complete a path, you add the start of that path to the output..

## Code

```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:

        # Create an adjacency list
        preMap = {crs:[] for crs in range(numCourses)}
        for crs, pre in prerequisites:
            preMap[crs].append(pre)

        output = []

        # visit indicates that it has already been added to the output
        # cycle indicates it has already been seen while exploring the current path (cycle detection)
        visit, cycle = set(), set()

        def check(crs):

            if crs in cycle: return False

            # We can return True since if its in the output, we know it can be completed
            if crs in visit: return True

            # Build the path while traversing through the prerequisites
            cycle.add(crs)
            for pre in preMap[crs]:
                if not check(pre): return False
            cycle.remove(crs)

            # If nothing led to a deadend, then add crs to the output
            visit.add(crs)
            output.append(crs)
            return True

        # Check if any of the courses failed. If so then return empty
        for crs in range(numCourses):
            if not check(crs): return []

        return output
```
