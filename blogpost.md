


# A paper review on how to reconstruct high quality and detail-rich 3D shapes from 2D images
![enter image description here](https://github.com/bockph/DISN-Presentation/blob/master/title_1.png?raw=true)
<center><i>3D shape reconstruction from a 2D image using DISN [1]</i></center> 

While humans are quite good at recognizing objects and deriving their properties, for machines it is a rather complex task to recover a 3D shape from a single view. Since this capability is a core technology, necessary in a variety of fields, it is an important object of research in 3D computer vision. Major progress has been achieved here, especially in the last few years through the introduction of deep learning. While most contemporary work already delivers quite decent results on recovering the overall shape, recovering fine-grained details was not a major focus in this domain of research. In practice, this means small structures like holes have mostly been ignored in reconstruction processes. To tackle this drawback Wang et al. presented "DISN: Deep Implicit Surface Network for High-quality single-view 3D Reconstruction" at the Conference on neural information processing systems (NeurIPS) 2019. 
In their publication, a Neural Network is presented capable of reconstructing both a high-quality overall shape as well as fine-grained details. While this post is about presenting their work more understandably, the original paper, as well as the official code, can be found here: https://github.com/laughtervv/DISN

## How does contemporary research solve the problem of single-view 3D reconstruction?

Modern research shows that as of now deep learning is the state of the art technique for single-view 3D reconstruction. However, apart from the Neural Network structures, the approaches differ in the way of how 3D shapes are represented in the networks. Therefore, we can cluster the related work in two distinct representation methods:

 - **explicit methods ---** describe a 3D model solidly using e.g. point clouds, voxels or meshes. The main advantage of such a method is its intuitiveness which also makes them easy to encode e.g. in a Neural Network. But they suffer from limited resolution and fixed mesh topologies. Further, traditionally applied training losses like Earth-mover Distance (EMD) or Chamfer Distance (CD) only approximate the similarity of shape and are therefore not accurate metrics.
Examples that were compared to DISN are *AtlasNet*, *Pixel2Mesh*, and *3DN*.  While the first uses a set of parametric elements to generate 3D surfaces, the latter two reconstruct 3D shapes by deforming a given source mesh. Pixel2Mesh herefore uses a hardcoded Ellipsoidmesh while 3DN expects the source Mesh as an input. 
 - **implicit methods ---** in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds, then a point $P(X,Y,Z)$ is said to be on the surface. 
Recent works like  *IMNet* or *OccNet*  predict such functions and have shown to be capable of avoiding the aforementioned drawbacks of explicit methods. Nonetheless, none of those works has been capable of reconstructing fine-grained details.

## A two-step approach
To achieve the goal of reconstructing both overall shape as well as fine-grained details, Wang et al. represent a 3D object implicitly using a Signed-Distance-Function (SDF). An SDF maps a point $P$ to a real value $s \in \mathbb{R}$ where the sign of $s$ tells whether $P$ is inside or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface.  As this function is continuous, DISN provides arbitrary resolution and therefore, avoids the drawback of the other explicit methods.
To predict this SDF they developed a feed-forward neural network that takes a single 2D image and a point in world coordinates $P(X, Y, Z)$ and returns the corresponding SDF value. Internally, this is done by using two consecutive networks: one for camera pose estimation and the other for concrete SDF prediction.

### How is the camera pose estimated 
For camera pose estimation they use the general approach proposed by Insafutdinov and Dosovitskiy **[???]** . By using a Convolutional Neural Network several pose candidates are combined. However, their approach suffers from a large number of network parameters and a complex training procedure. 
To reduce those disadvantages, the authors of DISN make use of recent research results, that continuous representations are easier to regress for Neural Networks. Zhou et al. have shown that e.g. a 6D rotation representation $b=(b_x,b_y)$ where $b \in \mathbb{R}^6, b_x \in \mathbb{R}^3, b_y \in \mathbb{R}^3$  is continuous, while quaternions and Euler angles are not, and is, therefore, better suited for regression in neural networks. Once $b$ is predicted, one can then obtain the rotation matrix R =(R_x, R_y, R_z)^T \in \matbb{R}^(3x3) with the following formulas:
$R_x = N(b_x), R_z = N(R_x \times b_y) , R_y = R_z \times R_x$

with N(\point) being the normalization function and \times the cross product.**[?Zhou et al. ]**
Translation $t \in \matbb{R}^3$ is predicted directly.




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMzA0OTgsLTEzMjIzMDg4NzMsMjA3NT
EwNTEyNiwtNzc1NzU2MTk0LDM2MTk0NzMwMCwtMTEyODYxNDcy
Nyw5MDI2NDE3OTUsLTMyMDE1NjIsLTIxMjE2OTM2MDIsNTU0MD
Y3ODA5LC0yMTQ2MjkzNjI0LDE1MjYxMjc0ODYsNTIzNzE3ODMz
LC05ODMwNzM5OTQsLTE1NDI0NzU3MjQsLTQyMjg1NTU0MiwyMT
IzMjExNjk4LC0zNDk4OTEyODUsLTE0NTM5NzcwNTksMjc2NzI3
NTVdfQ==
-->