# Dijkstra's Algorithm in C++

## Introduction

Dijkstra's algorithm is used for finding the shortest paths from a single source vertex to all other vertices in a graph with non-negative weights. It is a widely used algorithm due to its efficiency and simplicity.

## Code Explanation

Below is the C++ implementation of Dijkstra's algorithm with detailed comments.

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

// A structure to represent a node in the priority queue
struct Node {
    int vertex, weight;
    bool operator>(const Node& other) const {
        return weight > other.weight;
    }
};

// Function to print the shortest distance array
void printArr(const std::vector<int>& dist, int V) {
    std::cout << "Vertex Distance from Source\n";
    for (int i = 0; i < V; ++i)
        std::cout << i << "\t\t" << dist[i] << "\n";
}

// The main function that finds shortest distances from src to all other vertices using Dijkstra's algorithm
void Dijkstra(const std::vector<std::vector<Node>>& graph, int src) {
    int V = graph.size();
    std::vector<int> dist(V, INT_MAX);
    dist[src] = 0;
    
    // Priority queue to select the vertex with the smallest distance
    std::priority_queue<Node, std::vector<Node>, std::greater<Node>> pq;
    pq.push({src, 0});

    while (!pq.empty()) {
        int u = pq.top().vertex;
        pq.pop();
        
        for (const auto& neighbor : graph[u]) {
            int v = neighbor.vertex;
            int weight = neighbor.weight;
            
            if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({v, dist[v]});
            }
        }
    }

    printArr(dist, V);
}

int main() {
    int V = 5;
    std::vector<std::vector<Node>> graph(V);
    
    // Adding edges to the graph
    graph[0].push_back({1, 9});
    graph[0].push_back({2, 6});
    graph[0].push_back({3, 5});
    graph[0].push_back({4, 3});
    graph[2].push_back({1, 2});
    graph[2].push_back({3, 4});

    Dijkstra(graph, 0); // Function call

    return 0;
}
```

# Explanation

1. **Node Structure**:
   - The `Node` structure represents a node in the priority queue with a vertex and its associated weight. The `operator>` is overridden to facilitate the priority queue operations.

2. **printArr Function**:
   - This utility function prints the shortest distance from the source vertex to all other vertices.

3. **Dijkstra Function**:
   - This function takes the graph and the source vertex as input.
   - It initializes the distances from the source to all other vertices as infinite, except the source itself which is set to 0.
   - A priority queue is used to repeatedly select the vertex with the smallest known distance.
   - The algorithm updates the shortest paths to each vertex by exploring the neighbors of the current vertex.

4. **main Function**:
   - This is the entry point of the program.
   - It initializes the graph with vertices and edges and calls the `Dijkstra` function to find and print the shortest paths.

# Conclusion

Dijkstra's algorithm is an efficient algorithm for finding the shortest paths in a graph with non-negative weights. This C++ implementation demonstrates the core concepts of using a priority queue to manage and update the shortest paths dynamically.
