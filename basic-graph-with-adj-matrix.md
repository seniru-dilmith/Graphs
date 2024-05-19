
# Graph Implementation Using Adjacency Matrix in C++

This document provides a simple implementation of a graph using an adjacency matrix in C++. This graph is equally(1) weighted and undirected. It includes methods to add edges and print the graph.

## Code

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjMatrix; // Adjacency matrix

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
};

Graph::Graph(int V) {
    this->V = V;
    adjMatrix.resize(V, vector<int>(V, 0)); // Initialize matrix with zeros
}

void Graph::addEdge(int v, int w) {
    adjMatrix[v][w] = 1; // Add edge from v to w
    adjMatrix[w][v] = 1; // Add edge from w to v (since the graph is undirected)
}

void Graph::printGraph() {
    for (int i = 0; i < V; ++i) {
        cout << "Adjacency matrix row for vertex " << i << ": ";
        for (int j = 0; j < V; ++j) {
            cout << adjMatrix[i][j] << " ";
        }
        cout << endl;
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

    return 0;
}
```

## Explanation

### Includes and Namespace

```cpp
#include <iostream>
#include <vector>

using namespace std;
```

These lines include the necessary headers for input/output operations and using vectors. The `using namespace std` directive is used to avoid prefixing standard library names with `std::`.

### Class Definition

```cpp
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjMatrix; // Adjacency matrix

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
};
```

The `Graph` class is defined with private members `V` (number of vertices) and `adjMatrix` (adjacency matrix). Public members include the constructor, `addEdge` to add edges, and `printGraph` to print the graph.

### Constructor

```cpp
Graph::Graph(int V) {
    this->V = V;
    adjMatrix.resize(V, vector<int>(V, 0)); // Initialize matrix with zeros
}
```

The constructor initializes the number of vertices and resizes the adjacency matrix to accommodate these vertices, initializing all entries to zero.

### Adding Edges

```cpp
void Graph::addEdge(int v, int w) {
    adjMatrix[v][w] = 1; // Add edge from v to w
    adjMatrix[w][v] = 1; // Add edge from w to v (since the graph is undirected)
}
```

The `addEdge` method adds an edge between vertices `v` and `w` by setting the corresponding entries in the adjacency matrix to 1.

### Printing the Graph

```cpp
void Graph::printGraph() {
    for (int i = 0; i < V; ++i) {
        cout << "Adjacency matrix row for vertex " << i << ": ";
        for (int j = 0; j < V; ++j) {
            cout << adjMatrix[i][j] << " ";
        }
        cout << endl;
    }
}
```

The `printGraph` method prints the adjacency matrix, showing all connections between vertices.

### Main Function

```cpp
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

    return 0;
}
```

### Directed type

To get a directed graph We can modify the following lines,

```cpp
void Graph::addEdge(int v, int w) {
    adjMatrix[v][w] = 1; // Add edge from v to w
    adjMatrix[w][v] = 1; // Add edge from w to v (since the graph is undirected)
}
```
to this,

```cpp
void Graph::addEdge(int v, int w) {
    adjMatrix[v][w] = 1; // Add edge from v to w
}
```

### Weighted type

To get a directed graph We can modify the following lines,

```cpp
void Graph::addEdge(int v, int w) {
    adjMatrix[v][w] = 1; // Add edge from v to w
    adjMatrix[w][v] = 1; // Add edge from w to v (since the graph is undirected)
}
```
to this,

```cpp
void Graph::addEdge(int v, int w) {
    void Graph::addEdge(int v, int w) {
    adjMatrix[v][w] = 5; // Add edge from v to w
    adjMatrix[w][v] = 8; // Add edge from w to v (since the graph is undirected)
}
```

The `main` function demonstrates the usage of the `Graph` class by creating a graph with 5 vertices, adding edges between them, and printing the graph.
