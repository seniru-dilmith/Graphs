
# Depth-First Search (DFS) in C++

This document provides simple implementations of the Depth-First Search (DFS) algorithm in C++ using an adjacency list to represent the graph. Both iterative and recursive methods are covered.

## DFS_For_Graphs.cpp

### Recursive DFS

```cpp
#include <iostream>  // For input/output operations
#include <vector>    // For using the vector container

using namespace std;

// Function to perform DFS recursively on the graph
void DFS_Recursive(int node, const vector<vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;  // Mark the current node as visited
    cout << node << " ";   // Print the current node

    // Traverse all the neighbors of the current node
    for (int neighbor : adjList[node]) {
        if (!visited[neighbor]) {  // If the neighbor has not been visited
            DFS_Recursive(neighbor, adjList, visited);  // Recur for the neighbor
        }
    }
}

int main() {
    // Number of vertices
    int V = 5;

    // Adjacency list representation of the graph
    vector<vector<int>> adjList(V);

    // Adding edges
    adjList[0] = {1, 2};  // Node 0 is connected to nodes 1 and 2
    adjList[1] = {0, 3, 4};  // Node 1 is connected to nodes 0, 3, and 4
    adjList[2] = {0};  // Node 2 is connected to node 0
    adjList[3] = {1};  // Node 3 is connected to node 1
    adjList[4] = {1};  // Node 4 is connected to node 1

    vector<bool> visited(V, false);  // Create a visited vector to keep track of visited nodes

    // Perform DFS starting from vertex 0
    DFS_Recursive(0, adjList, visited);

    return 0;
}
```

### Iterative DFS

```cpp
#include <iostream>  // For input/output operations
#include <vector>    // For using the vector container
#include <stack>     // For using the stack container

using namespace std;

// Function to perform DFS iteratively on the graph
void DFS_Iterative(int start, const vector<vector<int>>& adjList) {
    int n = adjList.size();            // Get the number of vertices
    vector<bool> visited(n, false);    // Create a visited vector to keep track of visited nodes
    stack<int> s;                      // Create a stack to explore nodes in LIFO order

    s.push(start);                     // Push the start node into the stack

    while (!s.empty()) {               // Loop until the stack is empty
        int node = s.top();            // Get the top node from the stack
        s.pop();                       // Remove the top node from the stack

        if (!visited[node]) {          // If the node has not been visited
            visited[node] = true;      // Mark the node as visited
            cout << node << " ";       // Print the current node

            // Traverse all the neighbors of the current node
            for (int neighbor : adjList[node]) {
                if (!visited[neighbor]) {  // If the neighbor has not been visited
                    s.push(neighbor);      // Push the neighbor into the stack
                }
            }
        }
    }
}

int main() {
    // Number of vertices
    int V = 5;

    // Adjacency list representation of the graph
    vector<vector<int>> adjList(V);

    // Adding edges
    adjList[0] = {1, 2};  // Node 0 is connected to nodes 1 and 2
    adjList[1] = {0, 3, 4};  // Node 1 is connected to nodes 0, 3, and 4
    adjList[2] = {0};  // Node 2 is connected to node 0
    adjList[3] = {1};  // Node 3 is connected to node 1
    adjList[4] = {1};  // Node 4 is connected to node 1

    // Perform DFS starting from vertex 0
    DFS_Iterative(0, adjList);

    return 0;
}
```

## Explanation

### Recursive DFS

1. **Include necessary headers**: 
   - `#include <iostream>`: For input/output operations.
   - `#include <vector>`: For using the vector container to store the adjacency list.

2. **Define DFS function**:
   - `void DFS_Recursive(int node, const vector<vector<int>>& adjList, vector<bool>& visited)`: This function takes the current node, the adjacency list of the graph, and a visited vector as parameters.
   - `visited[node] = true`: Mark the current node as visited.
   - `cout << node << " "`: Print the current node.
   - `for (int neighbor : adjList[node])`: Traverse all the neighbors of the current node.
   - `if (!visited[neighbor])`: If the neighbor has not been visited.
   - `DFS_Recursive(neighbor, adjList, visited)`: Recur for the neighbor.

3. **Main function**:
   - `int V = 5`: Define the number of vertices.
   - `vector<vector<int>> adjList(V)`: Create an adjacency list to represent the graph.
   - Add edges to the graph:
     - `adjList[0] = {1, 2}`: Node 0 is connected to nodes 1 and 2.
     - `adjList[1] = {0, 3, 4}`: Node 1 is connected to nodes 0, 3, and 4.
     - `adjList[2] = {0}`: Node 2 is connected to node 0.
     - `adjList[3] = {1}`: Node 3 is connected to node 1.
     - `adjList[4] = {1}`: Node 4 is connected to node 1.
   - `vector<bool> visited(V, false)`: Create a visited vector to keep track of visited nodes.
   - `DFS_Recursive(0, adjList, visited)`: Perform DFS starting from vertex 0.

### Iterative DFS

1. **Include necessary headers**: 
   - `#include <iostream>`: For input/output operations.
   - `#include <vector>`: For using the vector container to store the adjacency list.
   - `#include <stack>`: For using the stack container to implement the iterative DFS algorithm.

2. **Define DFS function**:
   - `void DFS_Iterative(int start, const vector<vector<int>>& adjList)`: This function takes the starting node and the adjacency list of the graph as parameters.
   - `int n = adjList.size()`: Get the number of vertices in the graph.
   - `vector<bool> visited(n, false)`: Create a visited vector to keep track of visited nodes, initialized to `false`.
   - `stack<int> s`: Create a stack to explore nodes in LIFO order.
   - `s.push(start)`: Push the start node into the stack.

3. **DFS algorithm**:
   - `while (!s.empty())`: Loop until the stack is empty.
   - `int node = s.top()`: Get the top node from the stack.
   - `s.pop()`: Remove the top node from the stack.
   - `if (!visited[node])`: If the node has not been visited.
   - `visited[node] = true`: Mark the node as visited.
   - `cout << node << " "`: Print the current node.
   - `for (int neighbor : adjList[node])`: Traverse all the neighbors of the current node.
   - `if (!visited[neighbor])`: If the neighbor has not been visited.
   - `s.push(neighbor)`: Push the neighbor into the stack.

4. **Main function**:
   - `int V = 5`: Define the number of vertices.
   - `vector<vector<int>> adjList(V)`: Create an adjacency list to represent the graph.
   - Add edges to the graph:
     - `adjList[0] = {1, 2}`: Node 0 is connected to nodes 1 and 2.
     - `adjList[1] = {0, 3, 4}`: Node 1 is connected to nodes 0, 3, and 4.
     - `adjList[2] = {0}`: Node 2 is connected to node 0.
     - `adjList[3] = {1}`: Node 3 is connected to node 1.
     - `adjList[4] = {1}`: Node 4 is connected to node 1.
   - `DFS_Iterative(0, adjList)`: Perform DFS starting from vertex 0.

This code will output the order in which the nodes are visited starting from vertex 0. You can modify the graph structure or the starting node as needed.
