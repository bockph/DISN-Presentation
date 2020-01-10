

# A paper review on how to reconstruct high quality and detail-rich 3D shapes from 2D images
![enter image description here](https://github.com/bockph/DISN-Presentation/blob/master/title_1.png?raw=true)
<center><i>3D shape reconstruction from a 2D image using DISN [1]</i></center> 

While humans are quite good at recognizing objects and deriving their properties, for machines it is a rather complex task to recover a 3D shape from a single view. Since this capability is as a core technology necessary in a variety of fields, it is an important object of research in 3D computer vision.  Major progress has been achieved here, especially in the last few years through the introduction of deep learning. While most contemporary work already delivers quite decent results on recovering the overall shape, recovering fine-grained details was not a major focus in this field of research. In practice, this means small structures like holes have mostly been ignored in reconstruction processes.  To tackle this drawback Wang et al.  presented  "DISN: Deep Implicit Surface Network for High-quality single-view 3D Reconstruction" at the Conference on neural information processing systems (NeurIPS) 2019. In their publication, a Neural Network is presented capable of reconstructing both the overall shape as well as fine-grained details. While this post is about presenting their work more understandably, the original paper as well as the official code can be found here: https://github.com/laughtervv/DISN
## How does contemporary research solve the problem of single-view 3D reconstruction?
To get a clearer picture on how DISN compares to other approaches, we first must throw a look into what they do. Apart from the network architecture an important part of the reconstruction process is the representation of the 3D shape. 
In general, 3D representations can be divided into:

 - **explicit methods ---** which describe a 3D model solidly using e.g. point clouds, voxels or meshes. The main advantage of such a method is its intuitiveness which also makes them easy to encode e.g. in a Neural Network. But they suffer from limited resolution and fixed mesh topologies.
 - **implicit methods---** which in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds, then a point $P(X,Y,Z)$ is said to be on the surface.  Because of its continuity, the aforementioned drawbacks of explicit representations do not have to be considered here. Nonetheless, an implicit function probably has to be rendered on some point e.g. using the marching cubes algorithm -- adding additional calculation effort to an application.

Recent work that uses an explicit representation is e.g. *AtlasNet*, *Pixel2Mesh*, and *3DN*. 
While the former uses a set of parametric elements to generate 3D surfaces, the latter two reconstruct 3D shapes by deforming a given source mesh. Pixel2Mesh herefore uses a hardcoded Ellipsoidmesh while 3DN


AtlasNet to generate surfaces of 3D shapes using
a set of parametric surface elements. Wang et al. [12] introduce a graph-based network Pix2Mesh
to reconstruct 3D manifold shapes from input images whereas Wang et al. [13] present 3DN to
reconstruct a 3D shape by deforming a given source mesh A very common version of such an implicit function $F$ is the **Signed-Distance-Function (SDF)** which is also used by the here presented approach. An SDF maps the point $P$ to a real value $s  \in \mathbb{R}$ where the sign of $s$ tells whether $P$ is inside or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.







## A two-step approach

### Estimating the camera pose

### Prediction the Signed Distance Function

## Evaluating the Approach

## Some Discussion about this paper

### What the author thinks

### What I think

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3NTEwNTEyNiwtNzc1NzU2MTk0LDM2MT
k0NzMwMCwtMTEyODYxNDcyNyw5MDI2NDE3OTUsLTMyMDE1NjIs
LTIxMjE2OTM2MDIsNTU0MDY3ODA5LC0yMTQ2MjkzNjI0LDE1Mj
YxMjc0ODYsNTIzNzE3ODMzLC05ODMwNzM5OTQsLTE1NDI0NzU3
MjQsLTQyMjg1NTU0MiwyMTIzMjExNjk4LC0zNDk4OTEyODUsLT
E0NTM5NzcwNTksMjc2NzI3NTUsMTUyODcxMjM0NywtMjU1MDY5
NjcwXX0=
-->