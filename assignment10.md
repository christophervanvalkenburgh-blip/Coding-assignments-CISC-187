# Assignment 10
## Part 1
### Create a theoretical graph using a pen and paper OR electronically. (How about an electronic pen and paper!)
[Graph](https://github.com/christophervanvalkenburgh-blip/Coding-assignments-CISC-187/blob/main/graph.pdf)
## Part 2
### Implement the graph created in step 1 and apply breadth and depth-first search algorithms using C++.
```
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

//create Graph class for depth first and breadth first search algos
class Graph {
private:
    int size;
    vector<vector<int>> adj; //vector of vertex positions. outer: all, inner: neighbors

    // helper function for depth first search
    void dfsPrint(int v, vector<bool>& visited) {
        visited[v] = true; //mark current vertex v as visited to not revisit
        cout << airportName(v) << " "; //print airpot name for v

        //loop through each neighbor connected to v. If neighbor has not been visited, call dfsPrint on it
        for (int neighbor : adj[v]) {
            if (!visited[neighbor]) {
                dfsPrint(neighbor, visited);
            }
        }
    }

public:
    // constructor to create graph object of size s inner vectors
    Graph(int s) {
        size = s;
        adj.resize(s);
    }

    // function to add edges between neighbors, both ways since undirected
    void addEdge(int a, int b) {
        adj[a].push_back(b);
        adj[b].push_back(a);
    }

    // function to return airport code from vertex number
    string airportName(int n) {
        if (n == 0) return "SEA";
        if (n == 1) return "SFO";
        if (n == 2) return "LAX";
        if (n == 3) return "DEN";
        if (n == 4) return "LAS";
        if (n == 5) return "PHX";
        if (n == 6) return "DFW";
        return "";
    }

    // breadth first search function
    void bfs(int start) {
        vector<bool> visited(size, false); //create a visited list of same size as graph
        queue<int> q; //create queue q for search to use

        visited[start] = true; //starting vertex marked as visited
        q.push(start); //put starting vertex into queue

        //while loop, continues while queue is not empty
        while (!q.empty()) {
            int current = q.front(); //assign front queue item to current
            q.pop(); //remove the item from queue

            cout << airportName(current) << " ";

            //loop through neighbors of current
            for (int neighbor : adj[current]) {
                if (!visited[neighbor]) { //check if not visited already
                    visited[neighbor] = true; //mark as visited so vertex isn't added to queue more than once
                    q.push(neighbor); //add unvisited neighbor to queue
                }
            }
        }
    }

    // depth first search function
    void dfs(int start) {
        vector<bool> visited(size, false); //create visited vector
        dfsPrint(start, visited); //call dfsPrint function
    }
};

int main() {

    Graph g(7); // create Graph object g with 7 vertices

    // add each edge to graph
    g.addEdge(0, 1); // SEA - SFO
    g.addEdge(1, 2); // SFO - LAX
    g.addEdge(1, 3); // SFO - DEN
    g.addEdge(2, 4); // LAX - LAS
    g.addEdge(4, 3); // LAS - DEN
    g.addEdge(4, 5); // LAS - PHX
    g.addEdge(3, 5); // DEN - PHX
    g.addEdge(3, 6); // DEN - DFW

    //output type of search followed by calling that search
    cout << "Breadth first search starting from the SEA vertex: ";
    g.bfs(0);
    cout << endl;
    //repeat for second type
    cout << "Depth first search starting from the SEA vertex: ";
    g.dfs(0);
    cout << endl;

    return 0;
}
```
## Part 3
### Compare both search algorithms in the context of Big O notations.
DFS and BFS actually have the same time complexity in big O of O(V + E) while using an adjacency list, which is what I used in my assignment. If they were to use a matrix instead, the time complexity would be O(V^2). V being the number of verticies and E being the number of edges. Both searches have to go through the graph by visiting each vertex and checking each edge with the adjacency list. This results in the time complexity of O(V + E). However, the difference between the two isn't in their Big O notation, it's the way they move through the graph. BFS searches each level by level using a queue. DFS goes as deep as possible before backtracking. So while they do have the same search complexity, they do have different use cases. For example, if you wanted to see the fewest flights from SEA to DFW on my graph, BFS is better. If you wanted to fully explore everywhere, DFS is better. 

