

# A paper review on how to reconstruct high quality and detail-rich 3D shapes from 2D images
![enter image description here](https://github.com/bockph/DISN-Presentation/blob/master/title_1.png?raw=true)
<center><i>3D shape reconstruction from a 2D image using DISN [1]</i></center> 

While humans are quite good at recognizing objects and deriving their properties , for machines it is a rather complex task to recover a 3D shape from a single view. Since this capability is as a core technology necessary in a variety of fields it is an important object of research in 3D computer vision.  Major progress has been achieved here, especially in the last few years through the introduction of deep learning. While most contemporary work already delivers quite decent results on recovering the overall shape, recovering also fine graind details such as small holes was not a major focus in this field of research. Until 2019 when Wang et al. published "DISN: Deep Implicit Surface Network for High-quality Single-view 3D Reconstruction" a paper presenting a Neural Network capable of doing both. 

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
eyJoaXN0b3J5IjpbLTMyMDE1NjIsLTIxMjE2OTM2MDIsNTU0MD
Y3ODA5LC0yMTQ2MjkzNjI0LDE1MjYxMjc0ODYsNTIzNzE3ODMz
LC05ODMwNzM5OTQsLTE1NDI0NzU3MjQsLTQyMjg1NTU0MiwyMT
IzMjExNjk4LC0zNDk4OTEyODUsLTE0NTM5NzcwNTksMjc2NzI3
NTUsMTUyODcxMjM0NywtMjU1MDY5NjcwLC04NjAzMTQyMjAsMT
MzNjc2MTExNiwtMTA3MzU3NzQ1MiwyMDAwMjgwODAxLC02Njk1
NDQ4NTZdfQ==
-->