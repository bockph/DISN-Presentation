

# A paper review on how to reconstruct high quality and detail-rich 3D shapes from 2D images
![enter image description here](https://github.com/bockph/DISN-Presentation/blob/master/title_1.png?raw=true)
<center><i>3D shape reconstruction from a 2D image using DISN [1]</i></center> 

While humans are quite good at recognizing objects and deriving their properties, for machines it is a rather complex task to recover a 3D shape from a single view. Since this capability is as a core technology necessary in a variety of fields, it is an important object of research in 3D computer vision.  Major progress has been achieved here, especially in the last few years through the introduction of deep learning. While most contemporary work already delivers quite decent results on recovering the overall shape, recovering fine-grained details was not a major focus in this field of research. In practice, this means small structures like holes have mostly been ignored in reconstruction processes.  To tackle this drawback Wang et al.  presented  "DISN: Deep Implicit Surface Network for High-quality single-view 3D Reconstruction" at the Conference on neural information processing systems (NeurIPS) 2019. In their publication, a Neural Network is presented capable of reconstructing both the overall shape as well as fine-grained details. While this post is about presenting their work more understandably, the original paper as well as the official code can be found here: https://github.com/laughtervv/DISN
## How does contemporary research solve the problem of single-view 3D reconstruction?
To get a clearer picture of what they are doing, we first have to understand what other trending work is out there and how they differ. Apart from the network architecture -- to the best of my knowledge all recent work uses deep learning -- an important part of the reconstruction process is the representation of the 3D shape. 
In general, 3D representations can be divided into:

 - **explicit methods ---** which describe a 3D model solidly using e.g. point clouds, voxels or meshes. The main advantage of such a method is its intuitiveness which also makes them easy to encode e.g. in a Neural Network. But they suffer from limited resolution and fixed mesh topologies.
 - **implicit methods---** which in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds, then a point $P(X,Y,Z)$ is said to be on the surface.  Because of its continuity, the aforementioned drawbacks of explicit representations do not have to be considered here. Nonetheless, an implicit function probably has to be rendered on some point e.g. using the marching cubes algorithm -- adding additional calculation effort to an application.Recent work that uses  an explicit representation is e.g. AtlasNet, Pixel2Mesh and 3DN. While the former uses a set of parametric elements to generate 3D surfaces, the latter two deform AtlasNet to generate surfaces of 3D shapes using
a set of parametric surface elements. Wang et al. [12] introduce a graph-based network Pix2Mesh
to reconstruct 3D manifold shapes from input images whereas Wang et al. [13] present 3DN to
reconstruct a 3D shape by deforming a given source meshA very common version of such an implicit function $F$ is the **Signed-Distance-Function (SDF)** which is also used by the here presented approach. An SDF maps the point $P$ to a real value $s  \in \mathbb{R}$ where the sign of $s$ tells whether $P$ is inside or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.







## A two-step approach

### Estimating the camera pose

### Prediction the Signed Distance Function

## Evaluating the Approach

## Some Discussion about this paper

### What the author thinks

### What I think

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzYxOTQ3MzAwLC0xMTI4NjE0NzI3LDkwMj
Y0MTc5NSwtMzIwMTU2MiwtMjEyMTY5MzYwMiw1NTQwNjc4MDks
LTIxNDYyOTM2MjQsMTUyNjEyNzQ4Niw1MjM3MTc4MzMsLTk4Mz
A3Mzk5NCwtMTU0MjQ3NTcyNCwtNDIyODU1NTQyLDIxMjMyMTE2
OTgsLTM0OTg5MTI4NSwtMTQ1Mzk3NzA1OSwyNzY3Mjc1NSwxNT
I4NzEyMzQ3LC0yNTUwNjk2NzAsLTg2MDMxNDIyMCwxMzM2NzYx
MTE2XX0=
-->