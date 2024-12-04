# RitzSolver: Thin Plate Vibration Solver

[中文版博客](https://fengyukongzhou.github.io/2024/12/04/ritz-method-in-wl/)

## Overview

`RitzSolver` is a Wolfram Language package to approximate solutions for thin plate vibration problems using the Ritz method. It supports arbitrary geometries and boundary conditions.

---

## Installation

1. Download `RitzSolver.wl` and save it to your working directory or a directory in `$Path`.
2. Load the package:

   ```wolfram
   << RitzSolver.wl
   ```

---

## Usage

### 1. General Solver
Solve PDEs with arbitrary boundary conditions and geometries.

```wolfram
RitzSolver[{n, m}, {bf, bc, region, pr}, {x, y}]
```

- `n`: Number of basis functions in x-direction.
- `m`: Number of modes to compute.
- `bf`: Boundary function (e.g., `(x^2 + y^2 - 1)^i` for a circle).
- `bc`: Boundary condition (0: free, 1: simply supported, 2: clamped).
- `region`: Geometry (e.g., `Disk[]`, `Rectangle[]`, or custom polygons).
- `pr`: Poisson's ratio.

#### Example:
Solve for the first 3 modes of a clamped circular plate:
```wolfram
RitzSolver[{5, 3}, {(1 - x^2 - y^2)^2, 2, Disk[], 0.3}, {x, y}]
```

---

### 2. Predefined Geometries
Retrieve cached modal solutions for common shapes.

```wolfram
RitzSolver["geometry", {x, y}]
```

- `"Disk"`: Circular plate.  
- `"Square"`: Square plate.  
- `"Hexagon"`: Hexagonal plate.

#### Example:
Retrieve the first mode of a square plate:
```wolfram
RitzSolver["Square", {x, y}]
```
---

## Examples

1. **Clamped Circular Plate**:
   ```wolfram
   region = Disk[];
   boundary = (1 - x^2 - y^2)^2;
   RitzSolver[{5, 3}, {boundary, 2, region, 0.3}, {x, y}]
   ```

2. **Simply Supported Square Plate**:
   ```wolfram
   region = Rectangle[{-1, -1}, {1, 1}];
   boundary = (1 - x^2) (1 - y^2);
   RitzSolver[{4, 2}, {boundary, 1, region, 0.3}, {x, y}]
   ```

3. **Clamped Hexagonal Plate**:
   ```wolfram
   region = RegularPolygon[6];
   boundary = polygonBorder[CirclePoints[6], {x, y}];
   RitzSolver[{4, 4}, {boundary, 2, region, 1}, {x, y}]
   ```
