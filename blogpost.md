![3D shape reconstruction from a 2D image using DISN](tmp)
# A paper review on how to recover high quality and detail-rich 3D shapes from 2D images
Recovering a 3D shape from a single view is an ongoing research field which experienced quite some progress in the last few years driven by DeepLearning approaches. While humans can solve this quite easily using our intuition, for machines this is a rather complex but necessary task as  Until Single-view 3D reconstruction has been a

## How can a 3D shape be represented and what other approaches exist so far.
Using 2D images for a 3D shape reconstruction is a trending topic in the Research of the last years. However, while there are already several promising approaches out there, scientists where not able to decide on a gold standard concerning the representation of the 3D shape yet. TODO insert Neural Networks as recent main approach

In general, 3D representations can be divided into:

 - **explicit methods ---** describe a 3D model solidly using e.g. pointclouds, voxels or meshes. The main advantage of such method is its intuitivity which also makes them easy to encode e.g. in a Neural Network. But they suffer from limited resolution and fixed mesh topologies.
 - **implicit methods---** in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds, then a point $P(X,Y,Z)$ is said to be on the surface.  Because of its continuity the aformentioned drawbacks of explicit representations do not have to be considered here. Nonetheless, an implicit function probably has to be rendered on some point e.g. using the marching cubes algorithm adding additional calculation effort to an application.


Recent work that uses  an explicit representation is e.g. AtlasNet, Pixel2Mesh
### What 
Famous work
A very common version of such an implicit function $F$ is the **Signed-Distance-Function (SDF)** which is also used by the here presented approach. A SDF maps the point $P$ to a real value $s  \in \mathbb{R}$ where the sign of $s$ tells wether $P$ is insider or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.

As explicit representations are often quite intuitiv in their usage and therefore easy to encode. But, if such a representation is choosen a limited resolution and fixed mesh topology has to be assumed -- limiting the flexibility of an approach. These drawbacks, however, can be overcome by using an implicit function which are neither limited in resolution, because of their continuity,  nor suffer from fixed topology. 





## A two step approach

### Estimating the camera pose

### Prediction the Signed Distance Function

## Evaluating the Approach

## Some Discussion about this paper

### What the author thinks

### What I think

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2ODYxNDc0NCwyMTIzMjExNjk4LC0zND
k4OTEyODUsLTE0NTM5NzcwNTksMjc2NzI3NTUsMTUyODcxMjM0
NywtMjU1MDY5NjcwLC04NjAzMTQyMjAsMTMzNjc2MTExNiwtMT
A3MzU3NzQ1MiwyMDAwMjgwODAxLC02Njk1NDQ4NTYsMjMzMTky
OTddfQ==
-->