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
BFS is an unweighted graph traversal algorithm that explores nodes layer by layer uniformly outwards from the starting position, similar to a ripple expanding in water. It guarantees finding the shortest path on unweighted graphs because it evaluates all nodes at depth d before moving to depth 
It relies fundamentally on a Standard First-In First-Out (FIFO) Queue to manage the collection of frontier nodes to explore next, alongside a Hash Map or Balanced BST to keep track of discovered cells and prevent cycle evaluation.

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
