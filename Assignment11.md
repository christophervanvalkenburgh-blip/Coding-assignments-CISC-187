# Assignment 11
## Part 1
### Explain with the help of an example "Why Dijkstra's algorithm fails on negative weights".
First, I'll explain how the Dijkstra's algorithm works, and then I'll explain why it fails with negative weights. 
Dijkstra's algorithm finds the shortest path from a starting vertex to all other vertices in the graph. It chooses the vertex with the current known lowest total weight (distance, price, etc) from the start and then finalizes that as the shortest path to that vertex.  Then it keeps repeating this process, finding the shortest distances to each neighbor, and adding it to the original shortest distance, until we have all of the shortest paths from the starting vertex to all other vertices. 
This process doesn't always work with negative weights. If the negative weight does not create a shorter path to a vertex that was already finalized, the algorithm might work fine. But if we discover a path later that has a lower weight from that vertex to one that has already had its weight finalized, it will not replace that finalized distance. So it will fail to factor in the better path. The reason it sometimes works is because this error can be non-existent depending on where the shortest path ends up. In the perfect order, it could work. But since it doesn't always work for every scenario, it cannot be used with negative weights. 
This is a small example of how it doesn't work, no code specified required so I'm going to use something simple:

Home -> Store = 4 <br>
Home -> School = 7 <br>
School -> Store = -6

Dijkstra's algorithm attempts to find the shortest path from the starting vertex to each of the others. First, it checks the edges between home and each of the vertices school and store. Home to store has a weight of 4, home to school has weight of 7. The shortest path from home to store is now finalized with a distance of 4. However, when it starts checking the edges of school, it finds that school to store has an edge weight of -6. This means that the shortest path is now: 

Home -> (7) School -> (-6) Store 

which would result in a net distance of 1. But since it was already decided that the shortest path to the store from home was a distance of 4, this is the finalized distance and the shortcut gets ignored. 

