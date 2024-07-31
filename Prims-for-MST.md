# Prim's Algorithm in C++

## Introduction

Prim's algorithm is used for finding the Minimum Spanning Tree (MST) of a graph. It works by starting from an arbitrary vertex and growing the MST one edge at a time by selecting the smallest edge that connects a vertex in the MST to a vertex outside the MST.

## Code Explanation

Below is the C++ implementation of Prim's algorithm with detailed comments.

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

// Function to print the constructed MST
void printMST(const std::vector<int>& parent, const std::vector<std::vector<Node>>& graph) {
    std::cout << "Edge \tWeight\n";
    for (int i = 1; i < graph.size(); ++i)
        std::cout << parent[i] << " - " << i << "\t" << graph[i][parent[i]].weight << "\n";
}

// The main function that constructs MST using Prim's algorithm
void PrimMST(const std::vector<std::vector<Node>>& graph) {
    int V = graph.size();
    std::vector<int> parent(V, -1);  // Array to store constructed MST
    std::vector<int> key(V, INT_MAX); // Key values used to pick minimum weight edge in cut
    std::vector<bool> inMST(V, false); // To represent set of vertices not yet included in MST

    // Priority queue to pick the minimum key vertex
    std::priority_queue<Node, std::vector<Node>, std::greater<Node>> pq;
    key[0] = 0;
    pq.push({0, 0});

    while (!pq.empty()) {
        int u = pq.top().vertex;
        pq.pop();

        inMST[u] = true;

        // Update key value and parent index of the adjacent vertices of the picked vertex
        for (const auto& neighbor : graph[u]) {
            int v = neighbor.vertex;
            int weight = neighbor.weight;

            if (!inMST[v] && key[v] > weight) {
                key[v] = weight;
                pq.push({v, key[v]});
                parent[v] = u;
            }
        }
    }

    printMST(parent, graph);
}

int main() {
    int V = 5;
    std::vector<std::vector<Node>> graph(V);
    
    // Adding edges to the graph
    graph[0].push_back({1, 2});
    graph[0].push_back({3, 6});
    graph[1].push_back({0, 2});
    graph[1].push_back({2, 3});
    graph[1].push_back({3, 8});
    graph[1].push_back({4, 5});
    graph[2].push_back({1, 3});
    graph[2].push_back({4, 7});
    graph[3].push_back({0, 6});
    graph[3].push_back({1, 8});
    graph[4].push_back({1, 5});
    graph[4].push_back({2, 7});

    PrimMST(graph); // Function call

    return 0;
}
```

# Explanation

1. **Node Structure**:
   - The `Node` structure represents a node in the priority queue with a vertex and its associated weight. The `operator>` is overridden to facilitate the priority queue operations.

2. **printMST Function**:
   - This utility function prints the edges of the constructed MST and their weights.

3. **PrimMST Function**:
   - This function takes the graph as input and constructs the MST using Prim's algorithm.
   - It initializes the `parent`, `key`, and `inMST` arrays. The `parent` array stores the MST, `key` values are used to pick the minimum weight edge, and `inMST` keeps track of vertices included in the MST.
   - A priority queue is used to repeatedly select the vertex with the smallest known key value.
   - The algorithm updates the shortest paths to each vertex by exploring the neighbors of the current vertex.

4. **main Function**:
   - This is the entry point of the program.
   - It initializes the graph with vertices and edges, and calls the `PrimMST` function to construct and print the MST.

# Conclusion

Prim's algorithm is an efficient algorithm for finding the Minimum Spanning Tree of a graph. It uses a greedy approach by selecting the smallest edge that connects a vertex in the MST to a vertex outside the MST. This C++ implementation demonstrates the core concepts of using a priority queue to manage and update the MST dynamically.
