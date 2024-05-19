
# Graph Implementation Using Adjacency List with BFS

This document provides a simple implementation of a graph using an adjacency list in C++. It includes methods to add edges, print the graph, and perform Breadth-First Search (BFS).

## Full Code

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <queue>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<list<int>> adj; // Adjacency list

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
    void BFS(int startVertex); // Function to perform BFS
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list.
    adj[w].push_back(v); // Add v to w’s list (since the graph is undirected).
}

void Graph::printGraph() {
    for (int v = 0; v < V; ++v) {
        cout << "Adjacency list of vertex " << v << "\n head ";
        for (auto x : adj[v])
            cout << "-> " << x;
        cout << endl;
    }
}

void Graph::BFS(int startVertex) {
    vector<bool> visited(V, false); // Vector to keep track of visited vertices
    queue<int> q; // Queue for BFS

    visited[startVertex] = true;
    q.push(startVertex);

    while (!q.empty()) {
        int vertex = q.front();
        q.pop();
        cout << vertex << " ";

        // Get all adjacent vertices of the dequeued vertex
        for (auto i = adj[vertex].begin(); i != adj[vertex].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                q.push(*i);
            }
        }
    }
    cout << endl;
}

int main() {
    Graph g(5); // Create a graph with 5 vertices

    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    g.printGraph();

    cout << "Breadth First Traversal starting from vertex 2: ";
    g.BFS(2);

    return 0;
}
```

## BFS Function

```cpp
void Graph::BFS(int startVertex) {
    vector<bool> visited(V, false); // Vector to keep track of visited vertices
    queue<int> q; // Queue for BFS

    visited[startVertex] = true;
    q.push(startVertex);

    while (!q.empty()) {
        int vertex = q.front();
        q.pop();
        cout << vertex << " ";

        // Get all adjacent vertices of the dequeued vertex
        for (auto i = adj[vertex].begin(); i != adj[vertex].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                q.push(*i);
            }
        }
    }
    cout << endl;
}
```

### Explanation

The `BFS` function performs a Breadth-First Search starting from a given vertex. It uses a queue to manage the traversal and a vector to keep track of visited vertices. Here’s a step-by-step breakdown:

1. **Initialization**:
    - `vector<bool> visited(V, false)`: A vector to keep track of which vertices have been visited.
    - `queue<int> q`: A queue to manage the order of vertex visits.

2. **Start BFS**:
    - Mark the starting vertex as visited: `visited[startVertex] = true`.
    - Enqueue the starting vertex: `q.push(startVertex)`.

3. **BFS Loop**:
    - While the queue is not empty:
        - Dequeue a vertex from the front of the queue: `int vertex = q.front(); q.pop()`.
        - Print the dequeued vertex: `cout << vertex << " "`.

4. **Visit Adjacent Vertices**:
    - For each adjacent vertex of the dequeued vertex:
        - If the adjacent vertex has not been visited:
            - Mark it as visited: `visited[*i] = true`.
            - Enqueue it: `q.push(*i)`.

5. **End of BFS**:
    - Print a newline at the end of the traversal: `cout << endl;`.

This BFS implementation ensures that each vertex is visited in the order of their distance from the starting vertex, making it suitable for finding the shortest path in unweighted graphs.

