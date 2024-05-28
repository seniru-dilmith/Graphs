
# Breadth-First Search (BFS) in C++

This document provides a simple implementation of the Breadth-First Search (BFS) algorithm in C++ using an adjacency list to represent the graph.

## BFS_For_Graphs.cpp

```cpp
#include <iostream>  // For input/output operations
#include <vector>    // For using the vector container
#include <queue>     // For using the queue container

using namespace std;

// Function to perform BFS on the graph
void BFS(int start, const vector<vector<int>>& adjList) {
    int n = adjList.size();            // Get the number of vertices
    vector<bool> visited(n, false);    // Create a visited vector to keep track of visited nodes
    queue<int> q;                      // Create a queue to explore nodes in FIFO order

    visited[start] = true;             // Mark the start node as visited
    q.push(start);                     // Push the start node into the queue

    while (!q.empty()) {               // Loop until the queue is empty
        int node = q.front();          // Get the front node from the queue
        q.pop();                       // Remove the front node from the queue
        cout << node << " ";           // Print the current node

        // Traverse all the neighbors of the current node
        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {  // If the neighbor has not been visited
                visited[neighbor] = true;  // Mark it as visited
                q.push(neighbor);          // Push it into the queue
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

    // Perform BFS starting from vertex 0
    BFS(0, adjList);

    return 0;
}
```

## Explanation

1. **Include necessary headers**: 
   - `#include <iostream>`: For input/output operations.
   - `#include <vector>`: For using the vector container to store the adjacency list.
   - `#include <queue>`: For using the queue container to implement the BFS algorithm.

2. **Define BFS function**:
   - `void BFS(int start, const vector<vector<int>>& adjList)`: This function takes the starting node and the adjacency list of the graph as parameters.
   - `int n = adjList.size()`: Get the number of vertices in the graph.
   - `vector<bool> visited(n, false)`: Create a visited vector to keep track of visited nodes, initialized to `false`.
   - `queue<int> q`: Create a queue to explore nodes in FIFO order.
   - `visited[start] = true`: Mark the start node as visited.
   - `q.push(start)`: Push the start node into the queue.

3. **BFS algorithm**:
   - `while (!q.empty())`: Loop until the queue is empty.
   - `int node = q.front()`: Get the front node from the queue.
   - `q.pop()`: Remove the front node from the queue.
   - `cout << node << " "`: Print the current node.
   - `for (int neighbor : adjList[node])`: Traverse all the neighbors of the current node.
   - `if (!visited[neighbor])`: If the neighbor has not been visited.
   - `visited[neighbor] = true`: Mark the neighbor as visited.
   - `q.push(neighbor)`: Push the neighbor into the queue.

4. **Main function**:
   - `int V = 5`: Define the number of vertices.
   - `vector<vector<int>> adjList(V)`: Create an adjacency list to represent the graph.
   - Add edges to the graph:
     - `adjList[0] = {1, 2}`: Node 0 is connected to nodes 1 and 2.
     - `adjList[1] = {0, 3, 4}`: Node 1 is connected to nodes 0, 3, and 4.
     - `adjList[2] = {0}`: Node 2 is connected to node 0.
     - `adjList[3] = {1}`: Node 3 is connected to node 1.
     - `adjList[4] = {1}`: Node 4 is connected to node 1.
   - `BFS(0, adjList)`: Perform BFS starting from vertex 0.

This code will output the order in which the nodes are visited starting from vertex 0. You can modify the graph structure or the starting node as needed.
