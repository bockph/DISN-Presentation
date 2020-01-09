![3D shape reconstruction from a 2D image using DISN](tmp)
# A paper review on how to recover high quality and detail-rich 3D shapes from 2D images
some apetizing here
## What is 3D shape reconstruction about
Using 2D images for a 3D shape reconstruction is a trending topic in the Research of the last  years. However, while there are already several promising approaches out there, scientists where not able to decide on a gold standard concerning the representation of the 3D shape yet.

In general, 3D representations can be divided into:

 - **explicit representations ---** are
 - **implicit representations ---** define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds then a point $P(X,Y,Z)$ is said to be on the surface. The advantage of such an representations is that a volumetric model which is continous itself is also described by a continous functionA very common version of such an implicit function $F$ is the **Signed-Distance-Function (SDF)** which is also used by the here presented approach. A SDF maps the point $P$ to a real value $s  \in \mathbb{R}$ where the sign of $s$ tells wether $P$ is insider or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.

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
eyJoaXN0b3J5IjpbLTIwMjk2MzA0OTUsLTE0NTM5NzcwNTksMj
c2NzI3NTUsMTUyODcxMjM0NywtMjU1MDY5NjcwLC04NjAzMTQy
MjAsMTMzNjc2MTExNiwtMTA3MzU3NzQ1MiwyMDAwMjgwODAxLC
02Njk1NDQ4NTYsMjMzMTkyOTddfQ==
-->