
# Graph Implementation with adjacency list in C++

This document provides a simple implementation of a graph using an adjacency list in C++. It includes methods to add edges and print the graph, ensuring no duplicate edges are added. This graph uis undirected and equally(1) weighted.

## Code

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <algorithm>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<list<int>> adj; // Adjacency list

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    // Check if the edge already exists in both directions
    if (find(adj[v].begin(), adj[v].end(), w) == adj[v].end()) {
        adj[v].push_back(w); // Add w to v’s list
    }
    if (find(adj[w].begin(), adj[w].end(), v) == adj[w].end()) {
        adj[w].push_back(v); // Add v to w’s list (since the graph is undirected)
    }
}

void Graph::printGraph() {
    for (int v = 0; v < V; ++v) {
        cout << "Adjacency list of vertex " << v << "\nhead ";;
        for (auto x : adj[v])
            cout << "-> " << x;
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
    g.addEdge(3, 4); // Duplicate edge

    g.printGraph();

    return 0;
}
```

## Explanation

### Includes and Namespace

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <algorithm>

using namespace std;
```

These lines include the necessary headers for input/output operations, using vectors and lists, and the `find` algorithm. The `using namespace std` directive is used to avoid prefixing standard library names with `std::`.

### Class Definition

```cpp
class Graph {
private:
    int V; // Number of vertices
    vector<list<int>> adj; // Adjacency list

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
};
```

The `Graph` class is defined with private members `V` (number of vertices) and `adj` (adjacency list). Public members include the constructor, `addEdge` to add edges, and `printGraph` to print the graph.

### Constructor

```cpp
Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}
```

The constructor initializes the number of vertices and resizes the adjacency list to accommodate these vertices.

### Adding Edges

```cpp
void Graph::addEdge(int v, int w) {
    // Check if the edge already exists in both directions
    if (find(adj[v].begin(), adj[v].end(), w) == adj[v].end()) {
        adj[v].push_back(w); // Add w to v’s list
    }
    if (find(adj[w].begin(), adj[w].end(), v) == adj[w].end()) {
        adj[w].push_back(v); // Add v to w’s list (since the graph is undirected)
    }
}
```

The `addEdge` method adds an edge between vertices `v` and `w`. It first checks if the edge already exists in both directions using the `find` algorithm to avoid duplicates. If not found, it adds the edge to the adjacency lists of both vertices.

### Printing the Graph

```cpp
void Graph::printGraph() {
    for (int v = 0; v < V; ++v) {
        cout << "Adjacency list of vertex " << v << "\n head ";
        for (auto x : adj[v])
            cout << "-> " << x;
        cout << endl;
    }
}
```

The `printGraph` method prints the adjacency list of each vertex, showing all connected vertices.

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
    g.addEdge(3, 4); // Duplicate edge

    g.printGraph();

    return 0;
}
```

### To directed type

To get a directed graph We can modify the following lines,

```cpp
void Graph::addEdge(int v, int w) {
    // Check if the edge already exists in both directions
    if (find(adj[v].begin(), adj[v].end(), w) == adj[v].end()) {
        adj[v].push_back(w); // Add w to v’s list
    }
    if (find(adj[w].begin(), adj[w].end(), v) == adj[w].end()) {
        adj[w].push_back(v); // Add v to w’s list (since the graph is undirected)
    }
}
```
to this,

```cpp
void Graph::addEdge(int v, int w) {
    // Check if the edge already exists in both directions
    if (find(adj[v].begin(), adj[v].end(), w) == adj[v].end()) {
        adj[v].push_back(w); // Add w to v’s list
    }
}
```

The `main` function demonstrates the usage of the `Graph` class by creating a graph with 5 vertices, adding edges between them, and printing the graph. It also includes an example of attempting to add a duplicate edge to showcase the duplicate check.


Furthermore,
To get the weighted undirected graph, we have to modify the code to the following.

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <algorithm>
#include <utility> // for std::pair

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<list<pair<int, int>>> adj; // Adjacency list with weights

public:
    Graph(int V); // Constructor

    void addEdge(int v, int w, int weight); // Function to add an edge to graph
    void printGraph(); // Function to print the graph
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w, int weight) {
    // Check if the edge already exists in both directions
    bool exists = false;
    for (const auto& edge : adj[v]) {
        if (edge.first == w) {
            exists = true;
            break;
        }
    }
    if (!exists) {
        adj[v].push_back(make_pair(w, weight)); // Add w with weight to v’s list
    }
    
    exists = false;
    for (const auto& edge : adj[w]) {
        if (edge.first == v) {
            exists = true;
            break;
        }
    }
    if (!exists) {
        adj[w].push_back(make_pair(v, weight)); // Add v with weight to w’s list (since the graph is undirected)
    }
}

void Graph::printGraph() {
    for (int v = 0; v < V; ++v) {
        cout << "Adjacency list of vertex " << v << "\n head ";
        for (const auto& edge : adj[v])
            cout << "-> (" << edge.first << ", " << edge.second << ")";
        cout << endl;
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
    g.addEdge(4, 1, 10); // Duplicate edge
    g.addEdge(2, 3, 10); // Duplicate edge
    g.addEdge(3, 4, 10); // Duplicate edge

    g.printGraph();

    return 0;
}
```

Similarly we can do the directed graph.

### Directed Weighted Graph

Modify,
```cpp
void Graph::addEdge(int v, int w, int weight) {
    // Check if the edge already exists in both directions
    bool exists = false;
    for (const auto& edge : adj[v]) {
        if (edge.first == w) {
            exists = true;
            break;
        }
    }
    if (!exists) {
        adj[v].push_back(make_pair(w, weight)); // Add w with weight to v’s list
    }
    
    exists = false;
    for (const auto& edge : adj[w]) {
        if (edge.first == v) {
            exists = true;
            break;
        }
    }
    if (!exists) {
        adj[w].push_back(make_pair(v, weight)); // Add v with weight to w’s list (since the graph is undirected)
    }
}
```

to
```cpp
void Graph::addEdge(int v, int w, int weight) {
    // Check if the edge already exists in both directions
    bool exists = false;
    for (const auto& edge : adj[v]) {
        if (edge.first == w) {
            exists = true;
            break;
        }
    }
    if (!exists) {
        adj[v].push_back(make_pair(w, weight)); // Add w with weight to v’s list
    }
}
```

this.
