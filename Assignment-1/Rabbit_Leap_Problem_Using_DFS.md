# Rabbit Leap problem Using DFS

```
class RabbitLeapDFS:
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


dfs_problem = RabbitLeapDFS()
dfs_result = dfs(dfs_problem)

print("DFS Path:")
for step in dfs_result:
    print(step)
```
DFS Path:

('W', 'W', 'W', '_', 'E', 'E', 'E')

('W', 'W', 'W', 'E', '_', 'E', 'E')

('W', 'W', '_', 'E', 'W', 'E', 'E')

('W', '_', 'W', 'E', 'W', 'E', 'E')

('W', 'E', 'W', '_', 'W', 'E', 'E')

('W', 'E', 'W', 'E', 'W', '_', 'E')

('W', 'E', 'W', 'E', 'W', 'E', '_')

('W', 'E', 'W', 'E', '_', 'E', 'W')

('W', 'E', '_', 'E', 'W', 'E', 'W')

('_', 'E', 'W', 'E', 'W', 'E', 'W')

('E', '_', 'W', 'E', 'W', 'E', 'W')

('E', 'E', 'W', '_', 'W', 'E', 'W')

('E', 'E', 'W', 'E', 'W', '_', 'W')

('E', 'E', 'W', 'E', '_', 'W', 'W')

('E', 'E', '_', 'E', 'W', 'W', 'W')

('E', 'E', 'E', '_', 'W', 'W', 'W')
