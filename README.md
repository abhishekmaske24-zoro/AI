# AI
Praca
1 . DFS : def dfs(graph, node, visited):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        for neighbour in graph[node]:
            dfs(graph, neighbour, visited)

# Undirected graph
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A'],
    'D': ['B'],
    'E': ['B']
}

visited = set()
dfs(graph, 'A', visited)

2. BFS : def bfs_recursive(graph, queue, visited):
    if not queue:
        return
    node = queue.pop(0)
    print(node, end=" ")
    for neighbour in graph[node]:
        if neighbour not in visited:
            visited.add(neighbour)
            queue.append(neighbour)
    bfs_recursive(graph, queue, visited)

graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A'],
    'D': ['B']
}

visited = set(['A'])
queue = ['A']
bfs_recursive(graph, queue, visited)


3. A* ALGO : import heapq

def astar(start, goal, graph, heuristic):
    open_list = []
    heapq.heappush(open_list, (0, start))
    cost = {start: 0}
    parent = {start: None}

    while open_list:
        _, current = heapq.heappop(open_list)

        if current == goal:
            break

        for neighbor, weight in graph[current]:
            new_cost = cost[current] + weight
            if neighbor not in cost or new_cost < cost[neighbor]:
                cost[neighbor] = new_cost
                priority = new_cost + heuristic[neighbor]
                heapq.heappush(open_list, (priority, neighbor))
                parent[neighbor] = current

    path = []
    while goal:
        path.append(goal)
        goal = parent[goal]
    return path[::-1]

graph = {
    'A': [('B', 1), ('C', 3)],
    'B': [('D', 1)],
    'C': [('D', 1)],
    'D': []
}

heuristic = {'A': 4, 'B': 2, 'C': 2, 'D': 0}
print(astar('A', 'D', graph, heuristic))

4. Prims MST : import sys

def prim(graph, vertices):
    selected = [False] * vertices
    selected[0] = True
    edges = 0

    while edges < vertices - 1:
        minimum = sys.maxsize
        x = y = 0
        for i in range(vertices):
            if selected[i]:
                for j in range(vertices):
                    if not selected[j] and graph[i][j]:
                        if graph[i][j] < minimum:
                            minimum = graph[i][j]
                            x, y = i, j
        print(f"{x} - {y} : {graph[x][y]}")
        selected[y] = True
        edges += 1

graph = [
    [0, 2, 0, 6],
    [2, 0, 3, 8],
    [0, 3, 0, 0],
    [6, 8, 0, 0]
]

prim(graph, 4)


5. kruskals MST : class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = []

    def add_edge(self, u, v, w):
        self.graph.append([u, v, w])

    def find(self, parent, i):
        if parent[i] == i:
            return i
        return self.find(parent, parent[i])

    def union(self, parent, rank, x, y):
        xroot = self.find(parent, x)
        yroot = self.find(parent, y)
        if rank[xroot] < rank[yroot]:
            parent[xroot] = yroot
        else:
            parent[yroot] = xroot

    def kruskal(self):
        self.graph.sort(key=lambda x: x[2])
        parent = []
        rank = []
        for node in range(self.V):
            parent.append(node)
            rank.append(0)

        for u, v, w in self.graph:
            x = self.find(parent, u)
            y = self.find(parent, v)
            if x != y:
                print(f"{u} - {v} : {w}")
                self.union(parent, rank, x, y)

g = Graph(4)
g.add_edge(0, 1, 10)
g.add_edge(0, 2, 6)
g.add_edge(0, 3, 5)
g.add_edge(1, 3, 15)
g.add_edge(2, 3, 4)
g.kruskal()

6. n Queens : def solve_n_queens(board, row):
    if row == len(board):
        print(board)
        return
    for col in range(len(board)):
        if is_safe(board, row, col):
            board[row] = col
            solve_n_queens(board, row + 1)
            board[row] = -1

def is_safe(board, row, col):
    for i in range(row):
        if board[i] == col or abs(board[i] - col) == abs(i - row):
            return False
    return True

n = 4
board = [-1] * n
solve_n_queens(board, 0)

7. Chatbot: def chatbot():
    print("Chatbot: Hello! Type 'bye' to exit.")
    while True:
        user = input("You: ").lower()
        if user == "bye":
            print("Chatbot: Goodbye!")
            break
        elif "hello" in user:
            print("Chatbot: Hi there!")
        elif "price" in user:
            print("Chatbot: Please visit our pricing page.")
        else:
            print("Chatbot: Sorry, I didn't understand.")

chatbot()
