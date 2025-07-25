# Bridge Crossing Using DFS

```
class BridgeCrossingDFS:
    def __init__(self):
        self.times = {'Amogh': 5, 'Ameya': 10, 'Grandmother': 20, 'Grandfather': 25}
        self.people = set(self.times.keys())

    def initial(self):
        return (frozenset(self.people), frozenset(), 'left', 0)

    def is_goal(self, state):
        left, right, umbrella, time = state
        return left == frozenset() and time <= 60

    def nextmove(self, state):
        left, right, umbrella, time = state
        moves = []
        if umbrella == 'left':
            for p1 in left:
                for p2 in left:
                    if p1 <= p2:
                        new_left = left - {p1, p2}
                        new_right = right | {p1, p2}
                        new_time = time + max(self.times[p1], self.times[p2])
                        if new_time <= 60:
                            moves.append((new_left, new_right, 'right', new_time))
        else:
            for p in right:
                new_left = left | {p}
                new_right = right - {p}
                new_time = time + self.times[p]
                if new_time <= 60:
                    moves.append((new_left, new_right, 'left', new_time))
        return moves

def dfs(problem):
    stack = [(problem.initial(), [])]
    visited = set()
    while stack:
        state, path = stack.pop()
        if problem.is_goal(state):
            return path + [state]
        if state in visited:
            continue
        visited.add(state)
        for next_state in problem.nextmove(state):
            stack.append((next_state, path + [state]))
    return None

dfs_problem = BridgeCrossingDFS()
result_dfs = dfs(dfs_problem)

print("DFS Solution:\n")
if result_dfs:
    for idx, state in enumerate(result_dfs):
        left, right, side, time = state
        print(f"Step {idx+1}: Left={set(left)}, Right={set(right)}, Umbrella='{side}', Time={time}")
else:
    print("No solution found using DFS.")
```

DFS Solution:

Step 1: Left={'Ameya', 'Grandfather', 'Grandmother', 'Amogh'}, Right=set(), Umbrella='left', Time=0

Step 2: Left={'Grandfather', 'Grandmother'}, Right={'Ameya', 'Amogh'}, Umbrella='right', Time=10

Step 3: Left={'Grandfather', 'Grandmother', 'Amogh'}, Right={'Ameya'}, Umbrella='left', Time=15

Step 4: Left={'Amogh'}, Right={'Ameya', 'Grandfather', 'Grandmother'}, Umbrella='right', Time=40

Step 5: Left={'Ameya', 'Amogh'}, Right={'Grandfather', 'Grandmother'}, Umbrella='left', Time=50

Step 6: Left=set(), Right={'Ameya', 'Grandfather', 'Grandmother', 'Amogh'}, Umbrella='right', Time=60
