# 841 Keys and Rooms

**Medium**

There are `n` rooms labeled from `0` to `n - 1` and all the rooms are locked except for room `0`. Your goal is to visit all the rooms. However, you cannot enter a locked room without having its key.

When you visit a room, you may find a set of distinct keys in it. Each key has a number on it, denoting which room it unlocks, and you can take all of them with you to unlock the other rooms.

Given an array `rooms` where `rooms[i]` is the set of keys that you can obtain if you visited room `i`, return `true` if you can visit all the rooms, or `false` otherwise.

## Concept

The algorithm relys on a queue and an array to track progress. The array will indicate the rooms that you have visited and the queue will indicate the room you will be visiting. Everytime you enter a room, you add all the keys into the queue and you go visit that queue. Anytime we enter a room, the array should indicate that as well.

## Code

```python
class Solution:
    def canVisitAllRooms(self, rooms: List[List[int]]) -> bool:
        visited = [False] * len(rooms)
        q = deque()
        q.append(0) # We start by visiting room 0

        while q:
            curRoom = q.popleft()
            for toVisit in rooms[curRoom]:
                if not visit[toVisit]:
                    q.append(toVisit)   # Only add it to visit if we have not seen the room b4
        return all(visit)


```
