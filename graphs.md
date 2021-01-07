# Graphs
<img src="imgs/graph.png" alt="graph diagram" height=300 />

Graphs are abstract data types that models relationships between different elements. **Directed** graphs have edges that are arrows, thus conveying a direction of the connection between two vertices. **Undirected** graphs have edges that don't have a direction, thus conveying a two-way relationship. The graph shown above is an undirected graph. A graph is **connected** when there is a set of edges (a **path**) connecting every pair of vertices. 

### Trees
Trees are undirected, acyclic, and connected graphs. They have |V| - 1 edges, where |V| is the number of vertices (any more would create a cycle and any less would result in an unconnected graph). As a result, there is a unique path between any two vertices. 

## Shortest Paths Tree
Given a graph _G_ and a vertex _v_, the shortest paths tree of _G_ starting at _v_ is a tree where the distance from _v_ to every other vertex is minimized. The shortest paths tree of a graph is specific to the starting vertex, since it included the edges that would minimize the distance from the root vertex to all other vertices in the graph. Therefore, if we chose a different starting vertex, we would create a different shortest paths tree. Since every vertex in _G_ is included in its shortest paths trees, the shortest paths tree **spans** the graph. Below colored in red are the edges included in the shortest paths tree of the graph rooted at vertex _a_. 

<img src="imgs/spt.png" alt="shortst paths tree" height=300 />

### Dijkstra's Algorithm 
Dijksta's is an algorithm used to find the shortest path tree of a graph _G_ given a starting vertex _v_. It uses a minimum priority queue data structure to keep track of each vertex and its current known distance to the source. At the beginning of the algorithm, every vertex is infinitely far from the source, since the graph has not been explored. 

At each step of the algorithm, we visit the next closest vertex _u_ to the source vertex _s_ and _relax_ its edges, meaning we update the distance to _s_ of unvisited vertices adjacent to _u_. Below is the pseudocode of Dijkstra's. The `fringe` is the minimum priority queue. The `edgeTo` array keeps track of the edges used in the shortest paths tree so far (`edgeTo[v]` is the vertex adjacent to _v_ such that the edge to _v_ is used in the path from the _s_ to _v_ in the shortest paths tree). The `distTo` array keeps track of the distances of the vertices from the source (`distTo[v]` is the distance from _s_ to _v_.)
```
visited = {} \\ keep track of set of visited vertices
fringe.add(source, 0) \\ the source has priority 0, since it has a distance of 0 to itself
for all other vertices v:
  fringe.add(v, infinity)
  
while fringe is not empty:
  v = fringe.removeSmallest()
  for each edge v --> u with weight w where u is not in visited:
    visited.add(u)    
    if distTo[v] + w < distTo[u]: \\ a shorter path to u is found
      distTo[u] = distTo[v] + w
      edgeTo[u] = v
      fringe.changePriority(u, distTo[u])
```

#### Negative Edges 
Notice that once a vertex is removed from the fringe, it is never readded. As a result, once a vertex is removed, its distance from the source is never updated again. This means that Dijkstra's assumes the distance from the source to a vertex cannot decrease as more edges are added. Each step of the algorithm we remove the vertex that is closest to the source with the assumption that any other path we find to that vertex would be greater that what is currently found. This assumption may fail with the presence of negative edges. To illustrate, consider the example below. When forming the shortest paths tree from vertex _a_ with Dijkstra's algorithm, we determine that the shortest path from a to c is a-->c with a distance of 3, but we can see that the actual shortest path from a to c is a-->b-->c with a distance of 2. 

<img src="imgs/dijkstras-fail.png" alt="shortst paths tree fail with dijkstra's" height=300 />

#### Runtime
When deriving the runtime of algorithms in general, we can break it down into its different operations and data structures. Dijkstra's algorithm consists of adding to, removing from, and changing priorities in a heap. 

_Add/Removing:_

Each vertex is added to the priority queue once and also removed once. Therefore there are V add operations and V remove operations, where V is the number of vertices. <br/>
A single add takes O(logV), so adding V times takes `O(VlogV)`
A single remove takes O(logV), so removing V times takes `O(VlogV)`

_Change Priority:_

Change priority operations can occur at most E times, since this is the number of edges in the graph. In the worst case, every time we relax an edge, we could  update the shortest distance to a vertex. <br/>
A single change priority takes O(logV), so changing priority at most E times takes `O(ElogV)`

_Overall Runtime:_

To get the overall runtime, we add the runtime for each set of operations. <br/>
Overall runtime is `O(VlogV) + O(VlogV) + O(ElogV) = O((V + E)logV)` <br/>
We often see the runtime written as just `O(ElogV)` when we assume that there are more edges than vertices, which is usually the case in connected graphs. 

#### Examples
1. [Prof. Hug's walkthrough]()
2. [CSM worksheet example]()
### A* Algorithm 

A* has the same runtime as Dijkstra's and it can also fail with negative edges. 

#### Heuristics

#### Examples
1. [Prof. Hug's walkthrough]()
2. [CSM worksheet example]()

## Minimum Spanning Tree
- uniqueness 

### Prim's Algorithm 

#### Cut Property 

#### Examples
1. [Prof. Hug's walkthrough]()
2. [CSM worksheet example]()

### Kruskal's Algorithm 

#### Examples
1. [Prof. Hug's walkthrough]()
2. [CSM worksheet example]()
