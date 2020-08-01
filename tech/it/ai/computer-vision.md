# Overview

# Geometry

## Trilateration

In 2D, using distances from 3 different known points to allocate an
unknown point.
- Let the distances be d1, d2, d3
- Draw 3 circles with the centers at the three known points, and the
  radii are d1, d2, d3 appropriately.
- These three circle will meet at the unknown point.

## Triangulation

In 2D, using 2 known angles and a known baseline to calculate the
distance to an unknown point.
- Looking at ee16a final summary in Notability
- Looking at ee127 hw4 question 1

# Epipolar geometry

- Essential matrix (E): is a metric object pertaining to **calibrated** camera.
- Fundamental matrix (F): more general and fundamental terms of projective geometry
- Relationship between E and F: E = (K')^TFK
    + K' and K are intrinsic calibration matrices of the two images involved.
