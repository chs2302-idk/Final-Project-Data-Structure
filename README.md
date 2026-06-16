# Final-Project-Data-Structure

[cite_start]Final project repository for the Data Structures course (IUP)[cite: 1]. [cite_start]This repository contains a C++ implementation of multiple pathfinding algorithms evaluated across three distinct map environments[cite: 2, 7]. [cite_start]Performance metrics are simulated and measured using a local web visualizer engine[cite: 2, 6].

---

## Final Comparison Metrics

| Problem Map | Algorithm Used | Cells Explored (Visited) | Path Length (Moves) | Total Path Cost |
| :--- | :--- | :---: | :---: | :---: |
| **Soal 1 (No Walls/Weights)** | Breadth-First Search (BFS) | **36** | **10** | **10** |
| **Soal 1 (No Walls/Weights)** | Greedy Best-First Search | **11** | **10** | **10** |
| **Soal 2 (Walls, No Weights)** | *[Friend's Task — Pending]* | *TBD* | *TBD* | *TBD* |
| **Soal 3 (Walls & Weights)** | *[Friend's Task — Pending]* | *TBD* | *TBD* | *TBD* |

---

## Analysis Per Problem

### Soal 1: Open Grid Layout (No Walls, No Weights)
For the baseline map, we implemented and contrasted two different approaches to showcase algorithmic efficiency:

1. **Breadth-First Search (BFS):** * **Behavior:** BFS expands blindly and uniformly in a circular pattern across the grid. It processed **36 cells** before validating the path to the goal position.
   * **Trade-off:** It guarantees the shortest path, but has high computational overhead (large exploration footprint).
2. **Greedy Best-First Search:**
   * **Behavior:** Utilizing a Manhattan Distance heuristic ($|x_1 - x_2| + |y_1 - y_2|$), the priority queue pushes the exploration directly toward the target coordinates in a straight diagonal path. It processed only **11 cells**.
   * **Trade-off:** Drastically reduces the `Cells Explored` metric while maintaining path optimality on completely open terrain.

### Soal 2: Maze Layout (With Walls, No Weights)
* **Assigned To:** [Friend's Name 1]
* **Algorithm Draft:** *[e.g., Breadth-First Search (BFS) / Depth-First Search]*
* *[Slot for Friend 1 to write their short explanation of how the algorithm navigates around the wall `#` elements here]*

### Soal 3: Complex Terrain Layout (With Walls & Weights)
* **Assigned To:** [Friend's Name 2]
* **Algorithm Draft:** *[e.g., Dijkstra's Algorithm / A\* Search]*
* *[Slot for Friend 2 to write their short explanation of how a priority queue handles grid cell costs ranging from `1` to `9` here]*

---

## Compilation & Execution

[cite_start]To compile and execute the pathfinding binaries locally, navigate to the `submission/` directory and use a C++17 compatible compiler[cite: 6, 8]:

### 1. Build and Run BFS Version:
```bash
g++ -O2 -std=c++17 solution_bfs.cpp -o solution_bfs
./solution_bfs ../maps/soal1.txt output_bfs.txt
