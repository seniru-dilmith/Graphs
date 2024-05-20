
# Prim's Algorithm for Minimum Spanning Tree

## Introduction

Prim's algorithm is a popular algorithm used to find the Minimum Spanning Tree (MST) of a graph. A Minimum Spanning Tree of a graph is a subset of its edges that connect all vertices together without any cycles and with the minimum possible total edge weight.

## Algorithm Description

Prim's algorithm works as follows:

1. Initialize all vertices' key values to infinity and their parents to NIL.
2. Set the key value of the starting vertex (root) to 0.
3. While there are vertices not yet included in the MST:
    - Extract the vertex `u` with the minimum key value.
    - For each adjacent vertex `v` of `u`, if `v` is not in the MST and the weight of the edge `(u, v)` is less than the key value of `v`, update `v`'s key value and set its parent to `u`.

## Implementation

Here's the implementation of Prim's algorithm for a directed, weighted graph using an adjacency list in C++:

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <queue>
#include <utility>
#include <climits>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<list<pair<int, int>>> adj; // Adjacency list (vertex, weight)

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w, int weight); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
    void PrimMST(); // Function to perform Prim's algorithm
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w, int weight) {
    adj[v].push_back(make_pair(w, weight)); // Add w to v’s list with weight
}

void Graph::printGraph() {
    for (int v = 0; v < V; ++v) {
        cout << "Adjacency list of vertex " << v << "
head ";
        for (auto x : adj[v])
            cout << "-> (" << x.first << ", " << x.second << ")";
        cout << endl;
    }
}

void Graph::PrimMST() {
    // Priority queue to store vertices that are being preprocessed
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // Vector to store the minimum edge weight to reach each vertex
    vector<int> key(V, INT_MAX);

    // Array to store constructed MST
    vector<int> parent(V, -1);

    // To keep track of vertices included in the MST
    vector<bool> inMST(V, false);

    // Start from the first vertex
    key[0] = 0;
    pq.push(make_pair(0, 0)); // (weight, vertex)

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        inMST[u] = true;

        // Traverse all adjacent vertices of u
        for (auto x : adj[u]) {
            int v = x.first;
            int weight = x.second;

            // If v is not in MST and weight of (u,v) is smaller than the current key of v
            if (!inMST[v] && key[v] > weight) {
                key[v] = weight;
                pq.push(make_pair(key[v], v));
                parent[v] = u;
            }
        }
    }

    // Print the constructed MST
    cout << "Edge \tWeight\n";
    for (int i = 1; i < V; ++i)
        cout << parent[i] << " - " << i << "\t" << key[i] << endl;
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

    g.PrimMST();

    return 0;
}
```

This code implements Prim's algorithm to find the Minimum Spanning Tree for a directed, weighted graph. The adjacency list representation is used to store the graph, and a priority queue is used to efficiently find the next vertex to process.
