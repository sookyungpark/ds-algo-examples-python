## GCD
```
def gcd(a, b):
    if a == 0 or b == 0:
        return max(a, b)
    if a < b:
        (a, b) = (b, a)
    return gcd(b, a % b)
```

## LCM
```
def lcm(a, b):
    gcdVal = gcd(a, b)
    if gcdVal == 0:
        return 0
    return (a * b) / gcdVal
```

## DFS
```
def dfs(node, visited):
    if not node or visited[node]:
        return False
    visited[node] = True
    if isResult(node):
        return True
    return dfs(node.left, visited) or dfs(node.right, visited)
```

## BFS
```
import Queue

def bfs(root):
    q = Queue.Queue()
    q.put(root)
    while q:
        node = q.pop()
        if isResult(node):
            return True
        if item.left:
            q.put(item.left)
        if item.right:
            q.put(item.right)
    return False
```

## Union Find
```
sLen = len(s)
conn = [i for i in range(sLen)]
      
def union(idx):
    while conn[idx] != idx:
        conn[idx] = conn[conn[idx]]
        idx = conn[idx]
    return idx

for pair in pairs:
    conn[union(pair[0])] = union(pair[1])

groups = {i:[] for i in range(sLen)}
for i in range(sLen):
    groups[union(i)].append(i)
```

## Cycle Detection
```
def detectCycle:
    # dfs
    def isCyclic(graph, v, visited, recStack):
        visited[v] = True
        recStack[v] = True # recursionStack

        for neighbour in graph[v]:
            if visited[neighbour]:
                continue
            if isCyclic(neighbour, visited, recStack) or recStack[neighbour]:
                return True
        recStack[v] = False
        return False

    for node in range(n):
        if visited[node]:
            continue
        if isCyclic(node, [False] * n, [False] * n):
            return True
    return False
```

## Topological Sort
```
def sort(v, visited, graph, stk):
    visited[v] = True
    for i in graph[v]:
        if visited[i]:
            continue
        sort(i, visited, graph, stk)
    stk.insert(0, v)

def topologicalSort(n, graph):
    visited = [False] * n
    stk = []
    for i in range(n):
        if visited[i]:
            continue
        sort(i, visited, graph, stack)
    return stk
```

## Binary Search
### Bisect Left
```
def bisect_left(arr, value, begin, end):
    if begin >= end:
        return begin
    mid = begin + (end - begin) // 2
    if arr[mid] < value:
        return bisect_left(arr, value, mid + 1, end)
    else:
        return bisect_left(arr, value, begin, mid)
```
### Bisect Right
```
def bisect_right(arr, value, begin, end):
    if begin >= end:
        return begin
    mid = begin + (end - begin) // 2
    if value < arr[mid]:
        return bisect_right(arr, value, begin, mid)
    else:
        return bisect_right(arr, value, mid + 1, end)
```

## QuickSort
```
def quicksort(x):
   if len(x) <= 1:
       return x

   pivot = x[len(x) // 2]
   less, more, equal = [], [], []
   for a in x:
       if a < pivot:
           less.append(a)
       elif a > pivot:
           more.append(a)
       else:
           equal.append(a)

   return quicksort(less) + equal + quicksort(more)
```

## MergeSort
```
def mergesort(arr):
    arr_len = len(arr)
    if arr_len <= 1:
        return arr
  
    mid = arr_len // 2
    left, right = mergesort(arr[:mid]), mergesort(arr[mid:])
  
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result += left[i:] + right[j:]
    return result
```

## Shortest Path
### Dijkstra
O(E logV + V)
From one node to another nodes. No negative edge.
```
from queue import PriorityQueue

def Dijkstra(g, startNode):
    dist, prev = {}, {}
    Q = PriorityQueue()

    dist[startNode] = 0
    prev[startNode] = None
  
    for n in g.nodes():
        if n != startNode:
            dist[n] = float('Inf')
            prev[n] = None
        Q.put((dist[n], n))
  
    while Q.size() > 0:
        p, u = Q.pop()
        for v in g.neighbors(u):
            alt = dist[u] + g[u][v].get('weight', 1)
            if alt < dist[v]:
                dist[v], prev[v] = alt, u
                Q.put((dist[v], v))
              
    return dist, prev
```
### Bellman Ford
O(V * E) 
From one node to another nodes. Allows negative edge.
```
def initialize(graph, source):
    d = {} # Stands for destination
    p = {} # Stands for predecessor
    for node in graph:
        d[node] = float('Inf')
        p[node] = None
    d[source] = 0
    return d, p

def bellman_ford(graph, source):
    d, p = initialize(graph, source)
    for i in range(len(graph) - 1):
        for u in graph:
            for v in graph[u]: #For each neighbour of u
                if d[v] > d[u] + graph[u][v]:
                    d[v] = d[u] + graph[u][v]
                    p[v] = u

    # check for negative-weight cycles exist
    for u in graph:
        for v in graph[u]:
            # if update can occur, there is negative weight cycle
            assert d[v] <= d[u] + graph[u][v]

   return d, p
```

### Floyd Warshall
O(V^3)
From every node to every node
```
#       graph[][] = { {0,   1,  INF, 10},
#                    {INF,  0,  2,  INF},
#                    {INF, INF, 0,   1},
#                    {INF, INF, INF, 0} }
def floydWarshall(graph):
    dist = map(lambda i : map(lambda j: j, i), graph)

    for k in range(V):
        for i in range(V): 
            for j in range(V):
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
```