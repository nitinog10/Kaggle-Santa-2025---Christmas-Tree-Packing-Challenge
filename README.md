
# Christmas Tree Toy Packing Optimization

## Project Overview
This project addresses a 2D packing optimization problem: arranging a given number of Christmas tree-shaped toys into the smallest possible square parcel. The goal is to minimize the normalized area of the bounding box for shipments ranging from 1 to 200 trees, helping Santa Claus efficiently mail these stocking stuffers. Solutions are evaluated based on the score `s^2 / n`, where `s` is the side of the bounding box and `n` is the number of trees.

## Approach Taken

### 1. Tree Geometry Definition

A simplified 5-pointed star polygon was chosen as the geometric representation of a single Christmas tree toy. Its dimensions were set with an outer radius of 1.0 and an inner radius of 0.4, centered at the origin (0,0).

### 2. Bounding Box and Score Calculation

Two essential functions were developed:
*   `rotate_and_translate_polygon`: Transforms the vertices of a polygon based on given offsets and rotation degrees.
*   `calculate_bounding_box_side`: Determines the side `s` of the smallest square bounding box that encloses a set of transformed polygons.
*   `calculate_packing_score`: Computes the evaluation score `s^2 / n` for a given packing configuration.

### 3. Heuristic Packing Strategy

A heuristic optimization algorithm, `find_best_packing_heuristic`, was implemented to find packing solutions. This algorithm works as follows:
1.  **Initialization**: Generates an initial random configuration of `N` trees with random positions and rotations within a defined range.
2.  **Iterative Perturbation**: Over a set number of iterations, it randomly selects one tree and applies a small random perturbation to its position (x, y offsets) and rotation.
3.  **Evaluation**: Calculates the bounding box side and packing score for the perturbed configuration.
4.  **Acceptance**: If the new configuration yields a better (lower) packing score, it replaces the current best configuration.

### 4. Visualization of Packing Solutions

A `plot_packing_solution` function was created to visually represent the packed trees within their calculated minimal square bounding box. This aids in inspecting the effectiveness of the packing strategy.

### 5. Generating Results for N = 1 to 200

The heuristic strategy was applied iteratively for `N` ranging from 1 to 200 trees. The initial search range for tree placement was dynamically scaled by `2.0 * sqrt(N)` to accommodate the increasing number of trees. The best packing configuration, bounding box side, and score for each `N` were stored.

### 6. Submission File Generation

The collected packing data for `N=1` to `200` was formatted into a `submission main.csv` file. This file includes an `id` column (derived from the sample submission), `N`, `tree_index`, `x`, `y`, and `rotation` for each individual tree. Additionally, a `submission.json` file was created, representing the bounding box side (`s`) as "sX.Y" and tree configurations as "(X.Y,Z.W,A.B)" strings.

## Challenges and Next Steps

The implemented heuristic approach is effective in reducing the bounding box size but is susceptible to local optima. Finding a globally optimal solution for 2D packing problems, especially with rotated polygons, is a known NP-hard problem and computationally intensive.

**Potential next steps for improvement include:**
*   **Advanced Metaheuristics**: Exploring more sophisticated optimization algorithms such as Simulated Annealing, Genetic Algorithms, or Particle Swarm Optimization, which have mechanisms to escape local optima.
*   **Geometric Algorithms**: Investigating specialized geometric packing algorithms that might offer better theoretical guarantees or more efficient exploration of the solution space.
*   **Alternative Tree Shapes**: Evaluating the packing efficiency of different toy shapes (e.g., circles, rectangles, or other custom polygons) or even optimizing the toy's shape itself for better packing density."
