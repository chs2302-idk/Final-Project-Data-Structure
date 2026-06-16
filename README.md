# Final-Project-Data-Structure

## Final Comparison Metrics

| Problem Map | Algorithm Used | Cells Explored (Visited) | Path Length (Moves) | Total Path Cost |
| :--- | :--- | :---: | :---: | :---: |
| **Soal 1 (No Walls/Weights)** | Breadth-First Search (BFS) | **36** | **10** | **10** |
| **Soal 1 (No Walls/Weights)** | Greedy Best-First Search | **11** | **10** | **10** |
| **Soal 2 (Walls, No Weights)** | Breadth-First Search (BFS) | **35** | **14** | **14** |
| **Soal 2 (Walls, No Weights)** | Depth-First Search (DFS)| **30** | **14** | **14** |
| **Soal 3 (Walls & Weights)** | *[Friend's Task — Pending]* | *TBD* | *TBD* | *TBD* |

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



---

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
