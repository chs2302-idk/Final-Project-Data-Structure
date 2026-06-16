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

### Soal 1: No Walls, No Weights
BFS is an unweighted graph traversal algorithm that explores nodes layer by layer uniformly outwards from the starting position, similar to a ripple expanding in water. It guarantees finding the shortest path on unweighted graphs because it evaluates all nodes at depth d before moving to depth 

It relies fundamentally on a Standard First-In First-Out (FIFO) Queue to manage the collection of frontier nodes to explore next, alongside a Hash Map or Balanced BST to keep track of discovered cells and prevent cycle evaluation.

### Soal 2: With Walls, No Weights


### Soal 3: With Walls & Weights


---

## Compilation & Execution

