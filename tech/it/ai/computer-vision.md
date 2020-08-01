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

### Surveying

- Looking at ee16a final summary in Notability
- Triangulation is the process of determining the location of a point by
  measuring only angles to it from known points at two ends of a fixed
  baseline, rather than measuring distances to the point directly as in
  trilateration.

### Geometry

A subdivision of a planar object into triangles, and by extension the
subdivision of higher-dimension geometric objects into simplices (a
simplex is a generalization of the notion of a triangle or tetrahedron
to arbitrary dimensions)

### Computer Vision

Triangulation is the process of determining a point in 3D space given
its projections onto two, or more, images.
- Sometimes, triangulation is referred to as *reconstruction*.
- The process needs the parameters of the camera projection function,
  and it usually is represented by camera matrices.
- Looking at ee127 hw4 question 1

# Epipolar geometry

- Essential matrix (E): is a metric object pertaining to **calibrated** camera.
- Fundamental matrix (F): more general and fundamental terms of projective geometry
- Relationship between E and F: E = (K')^TFK
    + K' and K are intrinsic calibration matrices of the two images involved.


# Depth

- Disparity/relative depth to absolute depth
    + abs_depth (mm) = [focal_length (pixels) * baseline (mm)] / disparity (pixels)
