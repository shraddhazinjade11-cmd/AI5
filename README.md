#Program 5


from collections import deque

start = [1, 2, 3,
         4, 0, 6,
         7, 5, 8]

goal = [1, 2, 3,
        4, 5, 6,
        7, 8, 0]

def neighbors(state):
    moves = {
        0:[1,3], 1:[0,2,4], 2:[1,5],
        3:[0,4,6], 4:[1,3,5,7], 5:[2,4,8],
        6:[3,7], 7:[4,6,8], 8:[5,7]
    }

    pos = state.index(0)
    result = []

    for m in moves[pos]:
        new = state[:]
        new[pos], new[m] = new[m], new[pos]
        result.append(new)

    return result

queue = deque([start])
visited = []

while queue:
    current = queue.popleft()

    print(current)

    if current == goal:
        print("\nGoal Reached")
        break

    visited.append(current)

    for n in neighbors(current):
        if n not in visited and n not in queue:
            queue.append(n)


#program 6
# DFS for Water Jug Problem

visited = set()

def dfs(a, b):
    if (a, b) in visited:
        return

    visited.add((a, b))
    print((a, b))

    if a == 2 or b == 2:
        print("Goal Reached")
        return

    dfs(4, b)          # Fill Jug1
    dfs(a, 3)          # Fill Jug2
    dfs(0, b)          # Empty Jug1
    dfs(a, 0)          # Empty Jug2

    transfer = min(a, 3-b)
    dfs(a-transfer, b+transfer)

    transfer = min(b, 4-a)
    dfs(a+transfer, b-transfer)

dfs(0, 0)
