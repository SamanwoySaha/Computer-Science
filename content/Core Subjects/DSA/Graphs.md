---
title: Graphs
draft: false
tags: 
date: 19-Aug-2025
---
1. [graph editor](https://csacademy.com/app/graph_editor/)

# Theory

- Graphs
    
    A graph is a non-linear data structure consisting of nodes that have data and are connected to other nodes through edges.
    
    ![image.png](image%2067.png)
    
- Vertices and Edges
    
    **Nodes** are circles represented by numbers. Nodes are also referred to as vertices. They store the data. The numbering of the nodes can be done in any order, no specific order needs to be followed. 
    
    Two nodes are connected by a horizontal line called **Edge**. Edge can be directed or undirected. Basically, pairs of vertices are called edges.
    
    ![image.png](image%2068.png)
    
- Types of graphs
    - Directed Graph
        
        ![image.png](image%2069.png)
        
        ![image.png](image%2070.png)
        
        ![image.png](image%2071.png)
        
    - Undirected Graph
        
        ![image.png](image%2072.png)
        
        ![image.png](image%2073.png)
        
    - Simple Diagraph
        
        ![image.png](image%2074.png)
        
    - Non-connected Graph
        
        ![image.png](image%2075.png)
        
    - Connected Graph
        
        ![image.png](image%2076.png)
        
    - Strongly Connected Graph
        
        ![image.png](image%2077.png)
        
    - Directed Acyclic Graph (DAG)
        
        ![image.png](image%2078.png)
        
    - Topological ordering
        
        ![image.png](image%2079.png)
        
- Cycle
    
    ![image.png](image%2080.png)
    
    ![image.png](image%2081.png)
    
- Path
    
    ![image.png](image%2082.png)
    
    - 1 2 3 5 is a path
    - 1 2 3 2 1 is not a path, because a node can’t appear twice in a path.
    - 1 3 5 is not a path, as adjacent nodes must have an edge and there is no edge between 1 and 3.
- Degree
    
    It is the number of edges that go inside or outside that node.
    
    For **undirected graphs**, the degree is the number of edges attached to a node.
    
    ![image.png](image%2083.png)
    
    For **directed graphs,** we’ve Indegree and Outdegree. **The indegree** of a node is the number of incoming edges. **The outdegree** of a node is the number of outgoing edges.
    
    ![image.png](image%2084.png)
    
- Edge weight
    
    It is often referred to as the cost of the edge. If weights are not assigned then we assume the unit weight, i.e, 1. In applications, weight may be a measure of the cost of a route. For example, if vertices A and B represent towns in a road network, then weight on edge AB may represent the cost of moving from A to B, or vice versa.
    
    ![image.png](image%2085.png)
    
- Components
    
    ![image.png](image%2086.png)
    

# Graph Representation

- Adjacency Matrix
    
    ![image.png](image%2087.png)
    
    - First input: N (number of nodes) = 6
    - Second input: E (number of edges) = 6
    
    ![image.png](image%2088.png)
    
    ![image.png](image%2089.png)
    
    ![image.png](image%2090.png)
    
    ![image.png](image%2091.png)
    
    ```cpp
    // O(n^2) O(n^2) 
    int n, e;
    cin >> n >> e;
    vector<vector<int>> mat(n+1, vector<int>(n+1, 0));
    // memset(mat, 0, sizeof(mat));
    
    while (e--) {
        int a, b;
        cin >> a >> b;
        // for weighted graph
    	  // cin >> a >> b >> w;
        mat[a][b] = 1; 
        mat[b][a] = 1; // remove in case of directed graph
        // for weighted graph
        // mat[a][b] = w;
    }
    
    if (mat[3][1] == 1)	cout << "connection ache";
    else cout << "connection nai";
    ```
    
- Adjacency Lists
    
    ![image.png](image%2092.png)
    
    ![image.png](image%2093.png)
    
    ```cpp
    // undirected graph O(2e) O(2e)
    // directed graph O(e) O(e)
    int n, e;
    cin >> n >> e;
    vector<vector<int>> mat(n+1, vector<int>(n+1, 0));
    // vector<vector<pair<int, int>>> mat; // for weighted graph
    
    while (e--) {
      int a, b;
      cin >> a >> b;
      // for weighted graph
      // cin >> a >> b >> w;
      mat[a].push_back(b); 
      mat[b].push_back(a); // remove in case of directed graph
      // for weighted graph
      // mat[a].push_back({b, w}); 
    }
    
    for (int i = 0; i < mat[3].size(); i++) {
    	cout << mat[3][i] << " ";
    }
    
    ```
    
- Edge List
    
    ![image.png](image%2094.png)
    
    ![image.png](image%2095.png)
    
    ```cpp
    int n, e;
    cin >> n >> e;
    vector<pair<int, int>> v;
    
    while (e--) {
    	int a, b;
    	cin >> a >> b;
    	v.push_back({a, b});
    }
    
    for (auto p : v) {
    	cout << p.first << " " << p.second << endl;
    }
    ```
    
# Data Stucture
```python
# Matrix (2D Grid)
grid = [[0, 0, 0, 0],
        [1, 1, 0, 0],
        [0, 0, 0, 1],
        [0, 1, 0, 0]]

# Adjacency matrix
adjMatrix = [[0, 0, 0, 0],
             [1, 1, 0, 0],
             [0, 0, 0, 1],
             [0, 1, 0, 0]]        
        
from collections import deque

# GraphNode used for adjacency list
class GraphNode:
    def __init__(self, val):
        self.val = val
        self.neighbors = []

# Or use a HashMap
adjList = { "A": [], "B": [] }

# Given directed edges, build an adjacency list
edges = [["A", "B"], ["B", "C"], ["B", "E"], ["C", "E"], ["E", "D"]]

adjList = {}

for src, dst in edges:
    if src not in adjList:
        adjList[src] = []
    if dst not in adjList:
        adjList[dst] = []
    adjList[src].append(dst)
 
```
# Format

## 1D

```cpp
const int N = 1e6;
vector<int> v[N];
bool vis[N];

int main() {
    int n, e;
    cin >> n >> e;
    while (e--) {
        int a, b;
        cin >> a >> b;
        v[a].push_back(b);
        v[b].push_back(a);
    }
	  
	  int src;
	  cin >> src;
    memset(vis, false, sizeof(vis));
    return 0;
}
```

# 2D

```cpp
int v[20][20];
bool vis[20][20];
vector<pair<int, int>> d = {{0, 1}, {0, -1}, {-1, 0}, {1, 0}};
int n, m;

int main() {
    cin >> n >> m;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            cin >> v[i][j];

    int si, sj;
    cin >> si >> sj;
    memset(vis, false, sizeof(vis));
    return 0;
}
```

# Problems

- https://leetcode.com/problems/number-of-provinces/
    
    ```cpp
    // O(V+2E) O(n)
    int findCircleNum(vector<vector<int>>& isConnected) {
       int n = isConnected.size();
       
       for (int i = 0; i < n; i++) {
           for (int j = 0; j < n; j++) {
               if (i != j && isConnected[i][j] == 1) {
                   v[i].push_back(j);
               }
           }
       }
       
       int provinces = 0;
       for (int i = 0; i < n; i++) {
           if (!vis[i]) {
               dfs(i);
               provinces++;
           }
       }
       
       return provinces;
    }
    ```
    

# DFS

- DFS implementation
    
    ```cpp
    // undirected O(n+2e) O(n)
    // directed O(n+e) O(n)
    
    // 1d
    void dfs(int src) {
        cout << src << endl;
        vis[src] = true;
        for (int child : v[src]) {
    				if (vis[child] == false)
                dfs(child);
    		}    
    }
    
    // 2d
    void dfs(int si, int sj) {
        cout << si << " " << sj << endl;
        vis[si][sj] = true;
        for (int i = 0; i < 4; i++) {
    				auto [dx, dy] = d[i];
            int ci = si + dx;
            int cj = sj + dy;
            if (ci >= 0 && ci < n && cj >= 0 && cj < m && !vis[ci][cj])
                dfs(ci, cj);
        }
    }
    ```
    
#### count unique paths
```python
# in matrix

# Matrix (2D Grid)
grid = [[0, 0, 0, 0],
        [1, 1, 0, 0],
        [0, 0, 0, 1],
        [0, 1, 0, 0]]

# Count unique paths (backtracking)
def dfs(grid, r, c, visit):
    ROWS, COLS = len(grid), len(grid[0])
    if (min(r, c) < 0 or
        r == ROWS or c == COLS or
        (r, c) in visit or grid[r][c] == 1):
        return 0
    if r == ROWS - 1 and c == COLS - 1:
        return 1

    visit.add((r, c))

    count = 0
    count += dfs(grid, r + 1, c, visit)
    count += dfs(grid, r - 1, c, visit)
    count += dfs(grid, r, c + 1, visit)
    count += dfs(grid, r, c - 1, visit)

    visit.remove((r, c))
    return count


# in adjacency list

# Count paths (backtracking)
def dfs(node, target, adjList, visit):
    if node in visit:
        return 0
    if node == target:
        return 1
    
    count = 0
    visit.add(node)
    for neighbor in adjList[node]:
        count += dfs(neighbor, target, adjList, visit)
    visit.remove(node)

    return count
```
# BFS (Unweighted Graph)   

- BFS implementation
    
    ```cpp
    // undirected O(n+2e) O(n^2)
    // directed O(n+e) O(n^2)
    
    // 1d
    void bfs(int src) {
    		queue<int> q;
    		q.push(src);
    		vis[src] = true;
    		
    		while (!q.empty()) {
    				int par = q.front();
    				q.pop();
    				cout << par << endl;
    				for (int child : v[par]) {
    						if (!vis[child]) {
    								q.push(child);
    								vis[child] = true;
    						}
    				}
    		}
    }
    
    // 2d
    void bfs(int si, int sj) {
        queue<pair<int, int>> q;
        q.push({si, sj});
        vis[si][sj] = true;
        while (!q.empty()) {
            auto[x, y] = q.front();
            q.pop();
    
            for (int i = 0; i < 4; i++) {
    						auto [dx, dy] = d[i];
                int ci = x + dx;
                int cj = y + dy;
                if (ci >= 0 && ci < n && cj >= 0 && cj < m && !vis[ci][cj]) {
                    q.push({ci, cj});
                    vis[ci][cj] = true;
                }
            }
        }
    }
    ```

#### Shortest path from top left to bottom right
```python
# in matrix

from collections import deque

# Matrix (2D Grid)
grid = [[0, 0, 0, 0],
        [1, 1, 0, 0],
        [0, 0, 0, 1],
        [0, 1, 0, 0]]

# Shortest path from top left to bottom right
def bfs(grid):
    ROWS, COLS = len(grid), len(grid[0])
    visit = set()
    queue = deque()
    queue.append((0, 0))
    visit.add((0, 0))

    length = 0
    while queue:
        for i in range(len(queue)):
            r, c = queue.popleft()
            if r == ROWS - 1 and c == COLS - 1:
                return length

            neighbors = [[0, 1], [0, -1], [1, 0], [-1, 0]]
            for dr, dc in neighbors:
                if (min(r + dr, c + dc) < 0 or
                    r + dr == ROWS or c + dc == COLS or
                    (r + dr, c + dc) in visit or grid[r + dr][c + dc] == 1):
                    continue
                queue.append((r + dr, c + dc))
                visit.add((r + dr, c + dc))
        length += 1


# in adjacency list

from collections import deque

# Shortest path from node to target
def bfs(node, target, adjList):
    length = 0
    visit = set()
    visit.add(node)
    queue = deque()
    queue.append(node)

    while queue:
        for i in range(len(queue)):
            curr = queue.popleft()
            if curr == target:
                return length

            for neighbor in adjList[curr]:
                if neighbor not in visit:
                    visit.add(neighbor)
                    queue.append(neighbor)
        length += 1
    return length

```
# Union Find (Disjoint Sets)
```python
# find connected components
# find cycle in a graph

class UnionFind:
    def __init__(self, n):
        self.par = {}
        self.rank = {}

        for i in range(1, n + 1):
            self.par[i] = i
            self.rank[i] = 0
    
    # Find parent of n, with path compression.
    def find(self, n):
        p = self.par[n]
        while p != self.par[p]:
			# path compression
            self.par[p] = self.par[self.par[p]]
            p = self.par[p]
        return p

    # Union by height / rank.
    # Return false if already connected, true otherwise.
    def union(self, n1, n2):
        p1, p2 = self.find(n1), self.find(n2)
        if p1 == p2:
            return False
        
        if self.rank[p1] > self.rank[p2]:
            self.par[p2] = p1
        elif self.rank[p1] < self.rank[p2]:
            self.par[p1] = p2
        else:
            self.par[p1] = p2
            self.rank[p2] += 1
        return True
```

# Dijkstra's Algorithm (Weighted Graph) 
#### Given a connected graph represented by a list of edges, where edge[0] = src, edge[1] = dst, and edge[2] = weight, find the shortest path from src to every other node in the graph. There are n nodes in the graph.  
```python
import heapq

# O(E * logV), O(E * logE) is also correct.
def shortestPath(edges, n, src):
    adj = {}
    for i in range(1, n + 1):
        adj[i] = []
        
    # s = src, d = dst, w = weight
    for s, d, w in edges:
        adj[s].append([d, w])

    shortest = {}
    minHeap = [[0, src]]
    while minHeap:
        w1, n1 = heapq.heappop(minHeap)
        if n1 in shortest:
            continue
        shortest[n1] = w1

        for n2, w2 in adj[n1]:
            if n2 not in shortest:
                heapq.heappush(minHeap, [w1 + w2, n2])
    return shortest
```
# Topological Sort
#### Given a directed acyclical graph, return a valid topological ordering of the graph.  
```python
def topologicalSort(edges, n):
    adj = {}
    for i in range(1, n + 1):
        adj[i] = []
    for src, dst in edges:
        adj[src].append(dst)

    topSort = []
    visit = set()
    for i in range(1, n + 1):
        dfs(i, adj, visit, topSort)
    topSort.reverse()
    return topSort

def dfs(src, adj, visit, topSort):
    if src in visit:
        return
    visit.add(src)
    
    for neighbor in adj[src]:
        dfs(neighbor, adj, visit, topSort)
    topSort.append(src)
```

# Minimum Spanning Tree
## Prim's Algorithm
####  Given a list of edges of a connected undirected graph, with nodes numbered from 1 to n, return a list edges making up the minimum spanning tree. 
```python
# tc - O(ElogV), sc - O(E)
import heapq

def minimumSpanningTree(edges, n):
    adj = {}
    for i in range(1, n + 1):
        adj[i] = []
    for n1, n2, weight in edges:
        adj[n1].append([n2, weight])
        adj[n2].append([n1, weight])

    # Initialize the heap by choosing a single node
    # (in this case 1) and pushing all its neighbors.
    minHeap = []
    for neighbor, weight in adj[1]:
        heapq.heappush(minHeap, [weight, 1, neighbor])

    mst = []
    visit = set()
    visit.add(1)
    while len(visit) < n:
        weight, n1, n2 = heapq.heappop(minHeap)
        if n2 in visit:
            continue

        mst.append([n1, n2])
        visit.add(n2)
        for neighbor, weight in adj[n2]:
            if neighbor not in visit:
                heapq.heappush(minHeap, [weight, n2, neighbor])
    return mst
```

## Kruskal's Algorithm   
#### Given an list of edges of a connected undirected graph, with nodes numbered from 1 to n, return a list edges making up the minimum spanning tree.   
```python
import heapq 

class UnionFind:
    def __init__(self, n):
        self.par = {}
        self.rank = {}

        for i in range(1, n + 1):
            self.par[i] = i
            self.rank[i] = 0
    
    # Find parent of n, with path compression.
    def find(self, n):
        p = self.par[n]
        while p != self.par[p]:
            self.par[p] = self.par[self.par[p]]
            p = self.par[p]
        return p

    # Union by height / rank.
    # Return false if already connected, true otherwise.
    def union(self, n1, n2):
        p1, p2 = self.find(n1), self.find(n2)
        if p1 == p2:
            return False
        
        if self.rank[p1] > self.rank[p2]:
            self.par[p2] = p1
        elif self.rank[p1] < self.rank[p2]:
            self.par[p1] = p2
        else:
            self.par[p1] = p2
            self.rank[p2] += 1
        return True


def minimumSpanningTree(edges, n):
    minHeap = []
    for n1, n2, weight in edges:
        heapq.heappush(minHeap, [weight, n1, n2])

    unionFind = UnionFind(n)
    mst = []
    while len(mst) < n - 1:
        weight, n1, n2 = heapq.heappop(minHeap)
        if not unionFind.union(n1, n2):
            continue
        mst.append([n1, n2])
    return mst
```
