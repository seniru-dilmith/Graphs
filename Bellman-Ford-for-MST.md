
# Bellman-Ford Algorithm in C++

## Introduction

The Bellman-Ford algorithm is used for finding the shortest paths from a single source vertex to all other vertices in a weighted graph. Unlike Dijkstra's algorithm, Bellman-Ford can handle graphs with negative weight edges.

## Code Explanation

Below is the C++ implementation of the Bellman-Ford algorithm with detailed comments.

```cpp
#include <iostream>
#include <vector>
#include <climits>

// A structure to represent an edge in the graph
struct Edge {
    int src, dest, weight;
};

// A structure to represent a graph
struct Graph {
    int V, E; // V is the number of vertices, E is the number of edges
    std::vector<Edge> edges; // Vector of edges
};

// Function to print the shortest distance array
void printArr(const std::vector<int>& dist, int V) {
    std::cout << "Vertex Distance from Source\n";
    for (int i = 0; i < V; ++i)
        std::cout << i << "\t\t" << dist[i] << "\n";
}

// The main function that finds shortest distances from src to all other vertices using Bellman-Ford algorithm
void BellmanFord(const Graph& graph, int src) {
    int V = graph.V;
    int E = graph.E;
    std::vector<int> dist(V, INT_MAX);

    // Step 1: Initialize distances from src to all other vertices as INFINITE
    dist[src] = 0;

    // Step 2: Relax all edges |V| - 1 times.
    // A simple shortest path from src to any other vertex can have at most |V| - 1 edges
    for (int i = 1; i <= V - 1; ++i) {
        for (int j = 0; j < E; ++j) {
            int u = graph.edges[j].src;
            int v = graph.edges[j].dest;
            int weight = graph.edges[j].weight;
            if (dist[u] != INT_MAX && dist[u] + weight < dist[v])
                dist[v] = dist[u] + weight;
        }
    }

    // Step 3: Check for negative-weight cycles.
    // If we get a shorter path, then there is a cycle.
    for (int i = 0; i < E; ++i) {
        int u = graph.edges[i].src;
        int v = graph.edges[i].dest;
        int weight = graph.edges[i].weight;
        if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
            std::cout << "Graph contains negative weight cycle\n";
            return;
        }
    }

    printArr(dist, V);
}

int main() {
    int V = 5; // Number of vertices in graph
    int E = 8; // Number of edges in graph
    Graph graph = {V, E, {
        {0, 1, -1}, {0, 2, 4}, {1, 2, 3},
        {1, 3, 2}, {1, 4, 2}, {3, 2, 5},
        {3, 1, 1}, {4, 3, -3}
    }};

    BellmanFord(graph, 0); // Function call

    return 0;
}
```

## Explanation

1. **Edge and Graph Structures**:
   - The `Edge` structure represents an edge with a source (`src`), destination (`dest`), and weight (`weight`).
   - The `Graph` structure represents a graph with `V` vertices and `E` edges, and a vector of edges.

2. **printArr Function**:
   - This utility function prints the shortest distance from the source vertex to all other vertices.

3. **BellmanFord Function**:
   - This function takes the graph and the source vertex as input.
   - It initializes the distances from the source to all other vertices as infinite, except the source itself which is set to 0.
   - It then relaxes all edges |V| - 1 times. The shortest path from the source to any other vertex can have at most |V| - 1 edges.
   - Finally, it checks for negative-weight cycles. If a shorter path is found, it indicates a negative-weight cycle.

4. **main Function**:
   - This is the entry point of the program.
   - It initializes the graph with vertices and edges, and calls the `BellmanFord` function to find and print the shortest paths.

## Conclusion

The Bellman-Ford algorithm is a robust algorithm for finding the shortest path in a weighted graph, capable of handling graphs with negative weights. This C++ implementation demonstrates the core concepts of edge relaxation and cycle detection.
