
# Graph Implementation Using Adjacency List with DFS

This document provides a simple implementation of a graph using an adjacency list in C++. It includes methods to add edges, print the graph, and perform Depth-First Search (DFS).

## Full Code

```cpp
#include <iostream>
#include <vector>
#include <list>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<list<int>> adj; // Adjacency list

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
    void DFS(int startVertex); // Function to perform DFS
    void DFSUtil(int v, vector<bool>& visited); // Utility function for DFS
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

void Graph::DFS(int startVertex) {
    vector<bool> visited(V, false); // Vector to keep track of visited vertices
    DFSUtil(startVertex, visited); // Call the utility function to start DFS
    cout << endl;
}

void Graph::DFSUtil(int v, vector<bool>& visited) {
    visited[v] = true; // Mark the current node as visited
    cout << v << " "; // Print the current node

    // Recur for all the vertices adjacent to this vertex
    for (auto i = adj[v].begin(); i != adj[v].end(); ++i) {
        if (!visited[*i]) {
            DFSUtil(*i, visited);
        }
    }
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

    cout << "Depth First Traversal starting from vertex 0: ";
    g.DFS(0);

    return 0;
}
```

## DFS and DFSUtil Functions

```cpp
void Graph::DFS(int startVertex) {
    vector<bool> visited(V, false); // Vector to keep track of visited vertices
    DFSUtil(startVertex, visited); // Call the utility function to start DFS
    cout << endl;
}

void Graph::DFSUtil(int v, vector<bool>& visited) {
    visited[v] = true; // Mark the current node as visited
    cout << v << " "; // Print the current node

    // Recur for all the vertices adjacent to this vertex
    for (auto i = adj[v].begin(); i != adj[v].end(); ++i) {
        if (!visited[*i]) {
            DFSUtil(*i, visited);
        }
    }
}
```

### Explanation

The `DFS` function initiates the Depth-First Search from a given starting vertex. It uses a utility function `DFSUtil` to perform the actual traversal. Here's a step-by-step breakdown:

1. **DFS Function**:
    - **Initialization**: 
        - `vector<bool> visited(V, false)`: A vector to keep track of which vertices have been visited.
    - **Start DFS**:
        - Call the utility function `DFSUtil` with the starting vertex and the visited vector: `DFSUtil(startVertex, visited)`.
    - **Print a newline**:
        - Print a newline at the end of the traversal: `cout << endl;`.

2. **DFSUtil Function**:
    - **Mark as Visited**:
        - Mark the current vertex as visited: `visited[v] = true`.
    - **Print the Vertex**:
        - Print the current vertex: `cout << v << " "`.
    - **Recur for Adjacent Vertices**:
        - For each adjacent vertex of the current vertex:
            - If the adjacent vertex has not been visited, recursively call `DFSUtil` for the adjacent vertex: `DFSUtil(*i, visited)`.

This implementation ensures that each vertex is visited once and in depth-first order, exploring as far as possible along each branch before backtracking.

