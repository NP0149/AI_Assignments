# Rabbit Leap problem using BFS

```
rom collections import deque

class RabbitLeapBFS:
    def initial(self):
        return ('W', 'W', 'W', '_', 'E', 'E', 'E')

    def is_goal(self, state):
        return state == ('E', 'E', 'E', '_', 'W', 'W', 'W')

    def nextmove(self, state):
        moves = []
        state = list(state)
        for i in range(len(state)):
            if state[i] == 'W':
                if i+1 < len(state) and state[i+1] == '_':
                    new = state[:]
                    new[i], new[i+1] = new[i+1], new[i]
                    moves.append(tuple(new))
                elif i+2 < len(state) and state[i+1] in ['E','W'] and state[i+2] == '_':
                    new = state[:]
                    new[i], new[i+2] = new[i+2], new[i]
                    moves.append(tuple(new))
            elif state[i] == 'E':
                if i-1 >= 0 and state[i-1] == '_':
                    new = state[:]
                    new[i], new[i-1] = new[i-1], new[i]
                    moves.append(tuple(new))
                elif i-2 >= 0 and state[i-1] in ['E','W'] and state[i-2] == '_':
                    new = state[:]
                    new[i], new[i-2] = new[i-2], new[i]
                    moves.append(tuple(new))
        return moves

def bfs(problem):
    start = problem.initial()
    queue = deque([(start, [])])
    visited = set()

    while queue:
        state, path = queue.popleft()
        if problem.is_goal(state):
            return path + [state]
        if state in visited:
            continue
        visited.add(state)
        for next_state in problem.nextmove(state):
            queue.append((next_state, path + [state]))
    return None



bfs_problem = RabbitLeapBFS()
bfs_result = bfs(bfs_problem)

print("\nBFS Path:")
for step in bfs_result:
    print(step)

```


BFS Path:
('W', 'W', 'W', '_', 'E', 'E', 'E')
('W', 'W', '_', 'W', 'E', 'E', 'E')
('W', 'W', 'E', 'W', '_', 'E', 'E')
('W', 'W', 'E', 'W', 'E', '_', 'E')
('W', 'W', 'E', '_', 'E', 'W', 'E')
('W', '_', 'E', 'W', 'E', 'W', 'E')
('_', 'W', 'E', 'W', 'E', 'W', 'E')
('E', 'W', '_', 'W', 'E', 'W', 'E')
('E', 'W', 'E', 'W', '_', 'W', 'E')
('E', 'W', 'E', 'W', 'E', 'W', '_')
('E', 'W', 'E', 'W', 'E', '_', 'W')
('E', 'W', 'E', '_', 'E', 'W', 'W')
('E', '_', 'E', 'W', 'E', 'W', 'W')
('E', 'E', '_', 'W', 'E', 'W', 'W')
('E', 'E', 'E', 'W', '_', 'W', 'W')
('E', 'E', 'E', '_', 'W', 'W', 'W')
