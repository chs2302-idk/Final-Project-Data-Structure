# Final-Project-Data-Structure

## Final Comparison Metrics

| Problem Map | Algorithm Used | Cells Explored (Visited) | Path Length (Moves) | Total Path Cost |
| :--- | :--- | :---: | :---: | :---: |
| **Soal 1 (No Walls/Weights)** | Breadth-First Search (BFS) | **36** | **10** | **10** |
| **Soal 1 (No Walls/Weights)** | Greedy Best-First Search | **11** | **10** | **10** |
| **Soal 2 (Walls, No Weights)** | Breadth-First Search (BFS) | **35** | **14** | **14** |
| **Soal 2 (Walls, No Weights)** | Depth-First Search (DFS)| **30** | **14** | **14** |
| **Soal 3 (Walls & Weights)** | Dijkstra | **278** | **47** | **67** |
| **Soal 3 (Walls & Weights)** | Breadth-First Search (BFS) | **278** | **47** | **57** |
---

## Analysis Per Problem

### Soal 1: No Walls, No Weights
BFS is an unweighted graph traversal algorithm that explores nodes layer by layer uniformly outwards from the starting position, similar to a ripple expanding in water. It guarantees finding the shortest path on unweighted graphs because it evaluates all nodes at depth d before moving to depth 

It relies fundamentally on a Standard First-In First-Out (FIFO) Queue to manage the collection of frontier nodes to explore next, alongside a Hash Map or Balanced BST to keep track of discovered cells and prevent cycle evaluation.

### Soal 2: With Walls, No Weights
Breadth First Search / BFS
BFS is an unweighted graph traversal algorithm that explores nodes in layers, evenly outwards from the start point, like an expanding ripple. It guarantees shortest path, since it visits every node at depth $d$ before it visits nodes at depth $d+1$.

It is based on a standard FIFO Queue for the management of the frontier nodes and on a Hash Map or a Balanced BST to store the cells already discovered and to avoid cycles.

Depth First Search / DFS
DFS is a graph traversal algorithm . It starts in the initial node , and goes branch by branch , deep inwards . Like a root growing into the soil . It does not guarantee the shortest path, because it does not evaluate level by level, but jumps to maximum depth before backtracking.

It employs a Standard LIFO Stack for maintaining frontier nodes and Hash Map or Balanced BST to record discovered cells and avoid loops.



### Soal 3: With Walls & Weights
For Soal3, Dijkstra's Algorithm was chosen because the map contains both walls and weighted cells with traversal costs ranging from 1 to 9. In this situation, finding the shortest path in terms of steps is not enough, since a shorter route may have a higher total cost than a longer route with cheaper cells.
Dijkstra's algorithm evaluates the cumulative cost of each path and always expands the node with the lowest known cost using a priority queue. This allows the algorithm to efficiently avoid expensive cells and identify the minimum-cost route to the goal.
Compared to BFS, Dijkstra requires additional processing and memory because it must maintain distance values and manage a priority queue. However, this trade-off is worthwhile because it guarantees the optimal solution for weighted maps, making it the most suitable algorithm for Soal3.


## Compilation & Execution

### Soal 1: No Walls, No Weights

#### BFS
```
#include "harness.h"
#include <queue>
#include <map>
#include <vector>

vector<Cell> solve(vector<vector<char>>& grid, Cell start, Cell goal){
  vector<Cell> visited;
  
  std::queue<Cell> q;
  q.push(start);

  std::map<Cell, bool> discovered;
  discovered[start] = true;

  int dr[] = {-1, 1, 0, 0};
  int dc[] = { Rp01, 1};

  while(!q.empty()){
    Cell current = q.front();
    q.pop();

    visited.push_back(current);

    if(current.first == goal.first && current.second == goal.second){
      break;
    }

    for(int k = 0; k < 4; ++k){
      int nr = current.first + dr[k];
      int nc = current.second + dc[k];
      Cell neighbor = {nr, nc};

      if(inBounds(nr, nc) && !isWall(grid[nr][nc]) && !discovered[neighbor]){
        discovered[neighbor] = true;
        came_from[neighbor] = current; 
        q.push(neighbor);
      }
    }
  }

  return visited;
}
```

#### Greedy BFS
```
#include "harness.h"
#include <queue>
#include <map>
#include <vector>
#include <cmath>


int getDistance(Cell a, Cell b) {
    return std::abs(a.first - b.first) + std::abs(a.second - b.second);
}

vector<Cell> solve(vector<vector<char>>& grid, Cell start, Cell goal){
  vector<Cell> visited;

  std::priority_queue<std::pair<int, Cell>, 
                      std::vector<std::pair<int, Cell>>, 
                      std::greater<std::pair<int, Cell>>> pq;
  
  pq.push({getDistance(start, goal), start});

  std::map<Cell, bool> discovered;
  discovered[start] = true;

  int dr[] = {-1, 1, 0, 0};
  int dc[] = { Rp01, 1};

  while(!pq.empty()){
    Cell current = pq.top().second;
    pq.pop();

    visited.push_back(current);

    if(current.first == goal.first && current.second == goal.second){
      break;
    }

    for(int k = 0; k < 4; ++k){
      int nr = current.first + dr[k];
      int nc = current.second + dc[k];
      Cell neighbor = {nr, nc};

      if(inBounds(nr, nc) && !isWall(grid[nr][nc]) && !discovered[neighbor]){
        discovered[neighbor] = true;
        came_from[neighbor] = current;
        pq.push({getDistance(neighbor, goal), neighbor});
      }
    }
  }

  return visited;
}
```

### Soal 2: With Walls, No Weights

#### BFS
```
#include "harness.h"
#include <queue>
#include <set>

using namespace std;

vector<Cell> solve(vector<vector<char>>& grid, Cell start, Cell goal){
    vector<Cell> visited;

    queue<Cell> q;
    set<Cell> seen;

    q.push(start);
    seen.insert(start);

    int dr[] = {-1, 1, 0, 0};
    int dc[] = {0, 0, -1, 1};

    while(!q.empty()){
        Cell cur = q.front();
        q.pop();

        visited.push_back(cur);

        if(cur == goal) break;

        for(int k = 0; k < 4; k++){
            int nr = cur.first + dr[k];
            int nc = cur.second + dc[k];

            if(!inBounds(nr, nc)) continue;
            if(isWall(grid[nr][nc])) continue;

            Cell nxt = {nr, nc};

            if(seen.count(nxt)) continue;

            seen.insert(nxt);

            came_from[nxt] = cur;

            q.push(nxt);
        }
    }

    return visited;
}
```

#### DFS
```
#include "harness.h"
#include <stack>
#include <set>

vector<Cell> solve(vector<vector<char>>& grid, Cell start, Cell goal){

    vector<Cell> visited;

    stack<Cell> st;
    set<Cell> seen;

    st.push(start);
    seen.insert(start);

    int dr[] = {-1, 1, 0, 0};
    int dc[] = {0, 0, -1, 1};

    while(!st.empty()){

        Cell current = st.top();
        st.pop();

        visited.push_back(current);

        if(current == goal)
            break;

        int r = current.first;
        int c = current.second;

        for(int k = 0; k < 4; k++){

            int nr = r + dr[k];
            int nc = c + dc[k];

            if(!inBounds(nr, nc))
                continue;

            if(isWall(grid[nr][nc]))
                continue;

            Cell neighbor = {nr, nc};

            if(seen.count(neighbor))
                continue;

            seen.insert(neighbor);
            came_from[neighbor] = current;
            st.push(neighbor);
        }
    }

    return visited;
}

```

### Soal 3: With Walls and Weights

#### Dijkstra
```
#include "harness.h"
#include <queue>
#include <vector>

using namespace std;

vector<Cell> solve(vector<vector<char>>& grid, Cell start, Cell goal){
    vector<Cell> visited;
    const int INF = 1e9;

    vector<vector<int>> dist(rows_g, vector<int>(cols_g, INF));

    priority_queue<
        pair<int, Cell>,
        vector<pair<int, Cell>>,
        greater<pair<int, Cell>>
    > pq;

    dist[start.first][start.second] = 0;
    pq.push({0, start});

    int dr[4] = {-1, 1, 0, 0};
    int dc[4] = {0, 0, -1, 1};

    while(!pq.empty()){
        auto [cost, current] = pq.top();
        pq.pop();

        int r = current.first;
        int c = current.second;

        if(cost > dist[r][c])
            continue;

        visited.push_back(current);

        if(current == goal)
            break;

        for(int k = 0; k < 4; k++){
            int nr = r + dr[k];
            int nc = c + dc[k];

            if(nr < 0 || nr >= rows_g || nc < 0 || nc >= cols_g)
                continue;

            if(grid[nr][nc] == '#')
                continue;

            int weight = 1;

            if(grid[nr][nc] >= '1' && grid[nr][nc] <= '9')
                weight = grid[nr][nc] - '0';

            int newCost = cost + weight;

            if(newCost < dist[nr][nc]){
                dist[nr][nc] = newCost;

                came_from[{nr, nc}] = current;

                pq.push({newCost, {nr, nc}});
            }
        }
    }

    return visited;
}

```

#### BFS
```
#include "harness.h"
#include <queue>
#include <vector>

using namespace std;

vector<Cell> solve(vector<vector<char>>& grid, Cell start, Cell goal){
    vector<Cell> visited;

    queue<Cell> q;
    map<Cell,bool> seen;

    q.push(start);
    seen[start] = true;

    int dr[4] = {-1,1,0,0};
    int dc[4] = {0,0,-1,1};

    while(!q.empty()){
        Cell cur = q.front();
        q.pop();

        visited.push_back(cur);

        if(cur == goal)
            break;

        for(int k=0;k<4;k++){
            int nr = cur.first + dr[k];
            int nc = cur.second + dc[k];

            if(nr < 0 || nr >= rows_g || nc < 0 || nc >= cols_g)
                continue;

            if(grid[nr][nc] == '#')
                continue;

            Cell nxt = {nr,nc};

            if(!seen[nxt]){
                seen[nxt] = true;
                came_from[nxt] = cur;
                q.push(nxt);
            }
        }
    }

    return visited;
}
