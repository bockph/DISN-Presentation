




# A paper review on how to reconstruct high quality and detail-rich 3D shapes from 2D images
![enter image description here](https://github.com/bockph/DISN-Presentation/blob/master/title_1.png?raw=true)
<center><i>3D shape reconstruction from a 2D image using DISN [1]</i></center> 

While humans are quite good at recognizing objects and deriving their properties, for machines it is a rather complex task to recover a 3D shape from a single view. Since this capability is a core technology, necessary in a variety of fields, it is an important object of research in 3D computer vision. Major progress has been achieved here, especially in the last few years through the introduction of deep learning. While most contemporary work already delivers quite decent results on recovering the overall shape, recovering fine-grained details was not a major focus in this domain of research. In practice, this means small structures like holes have mostly been ignored in reconstruction processes. To tackle this drawback Wang et al. presented "DISN: Deep Implicit Surface Network for High-quality single-view 3D Reconstruction" at the Conference on neural information processing systems (NeurIPS) 2019. 
In their publication, a Neural Network is presented capable of reconstructing both a high-quality overall shape as well as fine-grained details. While this post is about presenting their work more understandably, the original paper, as well as the official code, can be found here: https://github.com/laughtervv/DISN

## How does contemporary research solve the problem of single-view 3D reconstruction?

Modern research shows that as of now deep learning is the state of the art technique for single-view 3D reconstruction. However, apart from the Neural Network structures, the approaches differ in the way of how 3D shapes are represented in the networks. Therefore, we can cluster the related work in two distinct representation methods:

 - **explicit methods ---** describe a 3D model solidly using e.g. point clouds, voxels or meshes. The main advantage of such a method is its intuitiveness which also makes them easy to encode e.g. in a Neural Network. But they suffer from limited resolution and fixed mesh topologies. Examples that were compared to DISN are *AtlasNet*, *Pixel2Mesh*, and *3DN*. 
While the first uses a set of parametric elements to generate 3D surfaces, the latter two reconstruct 3D shapes by deforming a given source mesh. Pixel2Mesh herefore uses a hardcoded Ellipsoidmesh while 3DN expects the source Mesh as an input. 
 - **implicit methods---** in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds, then a point $P(X,Y,Z)$ is said to be on the surface. Because of its continuity, the aforementioned drawbacks of explicit representations do not have to be considered here. Nonetheless, an implicit function probably has to be rendered on some point e.g. using the marching cubes algorithm -- adding additional calculation effort to an application. As an emerging area, implicit functions are predicted (amongst others) by 
*3D CNN* (as proposed by Dai et al.), *IMNet*, and *OccNet*.  While all achieve promising results recovering the overall shape they fail in recovering the fine-grained details.

A very common version of such an implicit function $F$ is the **Signed-Distance-Function (SDF)** which is also used by the here presented approach. An SDF maps the point $P$ to a real value $s  \in \mathbb{R}$ where the sign of $s$ tells whether $P$ is inside or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.







## A two-step approach

### Estimating the camera pose

### Prediction the Signed Distance Function

## Evaluating the Approach

## Some Discussion about this paper

### What the author thinks

### What I think

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMjIzMDg4NzMsMjA3NTEwNTEyNiwtNz
c1NzU2MTk0LDM2MTk0NzMwMCwtMTEyODYxNDcyNyw5MDI2NDE3
OTUsLTMyMDE1NjIsLTIxMjE2OTM2MDIsNTU0MDY3ODA5LC0yMT
Q2MjkzNjI0LDE1MjYxMjc0ODYsNTIzNzE3ODMzLC05ODMwNzM5
OTQsLTE1NDI0NzU3MjQsLTQyMjg1NTU0MiwyMTIzMjExNjk4LC
0zNDk4OTEyODUsLTE0NTM5NzcwNTksMjc2NzI3NTUsMTUyODcx
MjM0N119
-->