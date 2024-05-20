
# Kruskal's Algorithm Implementation in C++

## Introduction

Kruskal's algorithm is a greedy algorithm used to find the Minimum Spanning Tree (MST) of a connected, undirected graph. The MST is a subset of the edges that connects all vertices together, without any cycles and with the minimum possible total edge weight.

## Algorithm Description

1. **Sort all the edges**: First, sort all the edges in non-decreasing order of their weight.
2. **Initialize a forest**: Create a forest (a set of trees), where each vertex is its own tree.
3. **Add edges**: Pick the smallest edge. If adding the edge does not form a cycle in the MST, include it in the result. Repeat this until there are (V-1) edges in the result, where V is the number of vertices in the graph.

## Pseudocode

```
KruskalMST(graph):
    result = []  # This will store the resultant MST
    i, e = 0, 0  # Initialize count of edges

    # Step 1: Sort all the edges in non-decreasing order of their weight
    graph.edges.sort(key=lambda edge: edge.weight)

    parent = []  # Parent array for union-find
    rank = []    # Rank array for union-find

    # Create V subsets with single elements
    for vertex in range(graph.V):
        parent.append(vertex)
        rank.append(0)

    # Number of edges to be taken is equal to V-1
    while e < graph.V - 1:
        # Step 2: Pick the smallest edge and increment the index for next iteration
        u, v, w = graph.edges[i]
        i = i + 1
        x = find(parent, u)
        y = find(parent, v)

        # If including this edge does not cause a cycle
        if x != y:
            e = e + 1
            result.append((u, v, w))
            Union(parent, rank, x, y)

    return result
```

## C++ Implementation

Below is the C++ implementation of Kruskal's algorithm for a directed, weighted graph using an adjacency list.

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Graph class
class Graph {
private:
    int V; // Number of vertices
    vector<list<pair<int, int>>> adj; // Adjacency list (vertex, weight)
    vector<Edge> edges; // List of all edges for Kruskal's algorithm

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w, int weight); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
    void KruskalMST(); // Function to perform Kruskal's algorithm

    // Utility functions for Kruskal's algorithm
    int findParent(vector<int>& parent, int i);
    void unionSets(vector<int>& parent, vector<int>& rank, int x, int y);
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w, int weight) {
    adj[v].push_back(make_pair(w, weight)); // Add w to v’s list with weight
    edges.push_back({v, w, weight}); // Add the edge to the edge list
}

void Graph::printGraph() {
    for (int v = 0; v < V; ++v) {
        cout << "Adjacency list of vertex " << v << "\nhead ";
        for (auto x : adj[v])
            cout << "-> (" << x.first << ", " << x.second << ")";
        cout << endl;
    }
}

int Graph::findParent(vector<int>& parent, int i) {
    // Find the parent of a node i using path compression technique
    if (parent[i] != i) {
        parent[i] = findParent(parent, parent[i]);
    }
    return parent[i];
}

void Graph::unionSets(vector<int>& parent, vector<int>& rank, int x, int y) {
    // Perform union of two sets x and y using rank
    int rootX = findParent(parent, x);
    int rootY = findParent(parent, y);

    if (rank[rootX] < rank[rootY]) {
        parent[rootX] = rootY;
    } else if (rank[rootX] > rank[rootY]) {
        parent[rootY] = rootX;
    } else {
        parent[rootY] = rootX;
        rank[rootX]++;
    }
}

void Graph::KruskalMST() {
    // Resultant MST
    vector<Edge> result;
    int e = 0; // An index variable for result[]
    int i = 0; // An index variable for sorted edges

    // Step 1: Sort all the edges in non-decreasing order of their weight
    sort(edges.begin(), edges.end(), [](Edge a, Edge b) {
        return a.weight < b.weight;
    });

    // Allocate memory for creating V subsets
    vector<int> parent(V);
    vector<int> rank(V, 0);

    // Create V subsets with single elements
    for (int v = 0; v < V; ++v) {
        parent[v] = v;
    }

    // Number of edges to be taken is equal to V-1
    while (e < V - 1 && i < edges.size()) {
        // Step 2: Pick the smallest edge. Check if it forms a cycle with the spanning tree formed so far.
        Edge next_edge = edges[i++];

        int x = findParent(parent, next_edge.src);
        int y = findParent(parent, next_edge.dest);

        // If including this edge does not cause a cycle, include it in the result
        // and increment the index of the result for the next edge
        if (x != y) {
            result.push_back(next_edge);
            e++;
            unionSets(parent, rank, x, y);
        }
    }

    // Print the constructed MST
    cout << "Following are the edges in the constructed MST\n";
    for (auto edge : result) {
        cout << edge.src << " -- " << edge.dest << " == " << edge.weight << endl;
    }
}

int main() {
    Graph g(5); // Create a graph with 5 vertices

    g.addEdge(0, 1, 10);
    g.addEdge(0, 4, 20);
    g.addEdge(1, 2, 30);
    g.addEdge(1, 3, 40);
    g.addEdge(1, 4, 50);
    g.addEdge(2, 3, 60);
    g.addEdge(3, 4, 70);

    g.printGraph();

    g.KruskalMST();

    return 0;
}
```

## How to Run

1. **Compile the code**: Use a C++ compiler like `g++` to compile the code.
    ```
    g++ kruskal_algorithm.cpp -o kruskal_algorithm
    ```

2. **Run the executable**: Run the compiled program.
    ```
    ./kruskal_algorithm
    ```

## Conclusion

Kruskal's algorithm is efficient for finding the Minimum Spanning Tree of a graph. It uses a greedy approach to ensure that the tree formed is the minimum weight spanning tree. This implementation demonstrates the use of an adjacency list and the union-find data structure to achieve this efficiently.
