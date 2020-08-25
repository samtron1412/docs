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
- Depth
    + lighter is further away, and white (0) is the closest;
    + darker is closer, and black (255) is furthest
- Disparity: inverse of depth, so lighter is closer and darker is
  further

## Introduction

- Depth perception is the visual ability to perceive the world in 3D and
  the distance of an object.
- Depth perception arises from a variety of depth cues.
    + Binocular cues that are based on the receipt of sensory
      information in 3D from both eyes
        * *Retinal disparity*, which exploits parallax and vergence
        * Parallax: a displacement or difference in the apparent
          position (position as seen by an observer) of an object viewed
          along two different lines of sight, and is measured by the
          *angle* or *semi-angle* between those two lines.
        * Vergence: the simultaneous movement of both eyes in opposite
          direction to obtain or maintain single binocular vision.
            - Looking at closer objects: the eyes rotate towards each
              other (convergence)
            - Looking at farther away objects, they rotate away from
              each other (divergence)
    + Monocular cues that can be represented in just 2D and observed
      with just one eye.
        * Relative size (distant objects subtend smaller visual angles
          than near objects), texture gradient, occlusion, linear
          perspective, contrast differences, and motion parallax.

## Monocular Cues

### Motion parallax

- When an observer moves, the apparent relative motion of several
  stationary objects against a background gives hints about their
  relative distance.
- If information about the direction and velocity of movement is known,
  motion parallax can provide absolute depth information.
- This effect can be seen clearly when driving in a car: nearby things
  pass quickly, while far off objects appear stationary.

### Depth from Motion

- When an object moves towards an observer, the projection of the object
  is larger, so the changing in size serves as a distance cue.
    + The visual system's capacity to calculate time-to-contact (TTC) of
      an approaching object from the rate of optical expansion (driving
      a car or playing a ball game)

### Perspective

Something

### Relative size

Something

### Absolute size

Something

### Lighting and shading

Something

## Binocular Cues

### Stereopsis, or retinal (binocular) disparity, or binocular parallax

Disparity

### Convergence

Vergence

### Shadow Stereopsis

Something
