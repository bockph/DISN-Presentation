![3D shape reconstruction from a 2D image using DISN](tmp)
# A paper review on how to recover high quality and detail-rich 3D shapes from 2D images
some apetizing here
## What is 3D shape reconstruction about
Using 2D images for a 3D shape reconstruction is a trending topic in the Research of the last  years. However, while there are already several promising approaches out there, scientists where not able to decide on a gold standard concerning the representation of the 3D shape yet.

In general, 3D representations can be divided into:

 - **explicit methods ---** describe a 3D model solidly using e.g. pointclouds, voxels or meshes. As these methods are quite intuitiv in their usage they are very easy to encode. However, if such a representation is choosen a limited resolution and fixed mesh topology has to be assumed -- limiting the flexibility of an approach.
 - **implicit representations ---** in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds then a point $P(X,Y,Z)$ is said to be on the surface. The advantage of such an representations is that a volumetric model which is continous itself is also described by a continous function. This lead to more A very common version of such an implicit function $F$ is the **Signed-Distance-Function (SDF)** which is also used by the here presented approach. A SDF maps the point $P$ to a real value $s  \in \mathbb{R}$ where the sign of $s$ tells wether $P$ is insider or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.

explizit or implizit.
## Knowledge needed for the paper
## A two step approach

### Estimating the camera pose

### Prediction the Signed Distance Function

## Evaluating the Approach

## Some Discussion about this paper

### What the author thinks

### What I think

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1ODM2NDU2MSwtMTQ1Mzk3NzA1OSwyNz
Y3Mjc1NSwxNTI4NzEyMzQ3LC0yNTUwNjk2NzAsLTg2MDMxNDIy
MCwxMzM2NzYxMTE2LC0xMDczNTc3NDUyLDIwMDAyODA4MDEsLT
Y2OTU0NDg1NiwyMzMxOTI5N119
-->