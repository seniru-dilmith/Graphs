# Kruskal's Algorithm in C++

## Introduction

Kruskal's algorithm is used for finding the Minimum Spanning Tree (MST) of a graph. It works by sorting all the edges in non-decreasing order of their weights and adding the smallest edge to the MST, ensuring that no cycles are formed.

## Code Explanation

Below is the C++ implementation of Kruskal's algorithm with detailed comments.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// A structure to represent an edge in the graph
struct Edge {
    int src, dest, weight;
};

// A structure to represent a graph
struct Graph {
    int V, E; // V is the number of vertices, E is the number of edges
    std::vector<Edge> edges; // Vector of edges
};

// A structure to represent a subset for union-find
struct Subset {
    int parent;
    int rank;
};

// Function prototypes
int find(std::vector<Subset>& subsets, int i);
void Union(std::vector<Subset>& subsets, int x, int y);
void KruskalMST(Graph& graph);

// Function to find set of an element i (uses path compression technique)
int find(std::vector<Subset>& subsets, int i) {
    if (subsets[i].parent != i)
        subsets[i].parent = find(subsets, subsets[i].parent);
    return subsets[i].parent;
}

// Function to do union of two sets x and y (uses union by rank)
void Union(std::vector<Subset>& subsets, int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;
    else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// Function to compare two edges according to their weights
bool compareEdges(const Edge& a, const Edge& b) {
    return a.weight < b.weight;
}

// The main function to construct MST using Kruskal's algorithm
void KruskalMST(Graph& graph) {
    std::vector<Edge> result;  // Store the resultant MST
    int V = graph.V;

    // Step 1: Sort all the edges in non-decreasing order of their weight
    std::sort(graph.edges.begin(), graph.edges.end(), compareEdges);

    // Allocate memory for creating V subsets
    std::vector<Subset> subsets(V);
    for (int v = 0; v < V; ++v) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    int e = 0; // Index used to pick the next edge
    int i = 0; // Index used to iterate through sorted edges

    // Number of edges to be taken is equal to V-1
    while (e < V - 1 && i < graph.edges.size()) {
        // Step 2: Pick the smallest edge. Check if it forms a cycle with the spanning tree
        // formed so far. If not, include it in the result. Otherwise, discard it.
        Edge next_edge = graph.edges[i++];

        int x = find(subsets, next_edge.src);
        int y = find(subsets, next_edge.dest);

        // If including this edge doesn't cause a cycle, include it in the result
        // and increment the index of the result for the next edge
        if (x != y) {
            result.push_back(next_edge);
            Union(subsets, x, y);
            e++;
        }
    }

    // Print the constructed MST
    std::cout << "Following are the edges in the constructed MST\n";
    for (auto& edge : result)
        std::cout << edge.src << " -- " << edge.dest << " == " << edge.weight << "\n";
}

int main() {
    int V = 4; // Number of vertices in graph
    int E = 5; // Number of edges in graph
    Graph graph = {V, E, {
        {0, 1, 10}, {0, 2, 6}, {0, 3, 5}, {1, 3, 15}, {2, 3, 4}
    }};

    KruskalMST(graph);

    return 0;
}
```

# Explanation

1. **Edge and Graph Structures**:
   - The `Edge` structure represents an edge with a source (`src`), destination (`dest`), and weight (`weight`).
   - The `Graph` structure represents a graph with `V` vertices and `E` edges, and a vector of edges.

2. **Subset Structure**:
   - The `Subset` structure represents a subset for the union-find data structure, which includes a parent and a rank.

3. **find Function**:
   - This function finds the set of an element using the path compression technique. Path compression helps in flattening the structure of the tree whenever `find` is called, making future operations faster.

4. **Union Function**:
   - This function performs the union of two sets using the union by rank technique. It attaches the smaller tree under the root of the deeper tree to keep the tree as flat as possible.

5. **compareEdges Function**:
   - This function compares two edges according to their weights and is used to sort the edges.

6. **KruskalMST Function**:
   - This function constructs the Minimum Spanning Tree using Kruskal's algorithm.
   - It sorts all the edges in non-decreasing order of their weights.
   - It uses the union-find data structure to ensure that adding an edge to the MST does not form a cycle.
   - It includes the edge in the result if it does not cause a cycle and repeats until the MST contains \( V-1 \) edges.

7. **main Function**:
   - This is the entry point of the program.
   - It initializes the graph with vertices and edges, and calls the `KruskalMST` function to construct and print the MST.

# Conclusion

Kruskal's algorithm is an efficient algorithm for finding the Minimum Spanning Tree of a graph. It uses a greedy approach by selecting the smallest edges first and a union-find data structure to avoid cycles. This C++ implementation demonstrates the core concepts of edge sorting, union-find, and cycle detection to build the MST.
