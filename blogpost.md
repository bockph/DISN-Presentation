
  

  

  

  

# A paper review on how to reconstruct high quality and detail-rich 3D shapes from 2D images

![enter image description here](https://github.com/bockph/DISN-Presentation/blob/master/title_1.png?raw=true)

<center><i>3D shape reconstruction from a 2D image using DISN [1]</i></center>

  

While humans are quite good at recognizing objects and deriving their properties, for machines it is a rather complex task to recover a 3D shape from a single view. Since this capability is a core technology, necessary in a variety of fields, it is an important object of research in 3D computer vision. Major progress has been achieved here, especially in the last few years through the introduction of deep learning. While most contemporary work already delivers quite decent results on recovering the overall shape, recovering fine-grained details was not a major focus in this domain of research. In practice, this means small structures like holes have mostly been ignored in reconstruction processes. To tackle this drawback Wang et al. presented "DISN: Deep Implicit Surface Network for High-quality single-view 3D Reconstruction" at the Conference on neural information processing systems (NeurIPS) 2019.

In their publication, a Neural Network is presented capable of reconstructing both a high-quality overall shape as well as fine-grained details. While this post is about presenting their work more understandably, the original paper, as well as the official code, can be found here: https://github.com/laughtervv/DISN

  

## How does contemporary research solve the problem of single-view 3D reconstruction?

  

Modern research shows that as of now deep learning is the state of the art technique for single-view 3D reconstruction. However, apart from the Neural Network structures, the approaches differ in the way of how 3D shapes are represented in the networks. Therefore, we can cluster the related work in two distinct representation methods:

  

- **explicit methods ---** describe a 3D model solidly using e.g. point clouds, voxels or meshes. The main advantage of such a method is its intuitiveness which also makes them easy to encode e.g. in a Neural Network. But they suffer from limited resolution and fixed mesh topologies. Further, traditionally applied training losses like Earth-mover Distance (EMD) or Chamfer Distance (CD) only approximate the similarity of shape and are therefore not accurate metrics.

Examples that were compared to DISN are *AtlasNet*, *Pixel2Mesh*, and *3DN*. While the first uses a set of parametric elements to generate 3D surfaces, the latter two reconstruct 3D shapes by deforming a given source mesh. Pixel2Mesh herefore uses a hardcoded Ellipsoidmesh while 3DN expects the source Mesh as an input.

- **implicit methods ---** in contrast, define a surface by using a volumetric scalar function. If the equation $F(X,Y,Z) = 0$ holds, then a point $P(X,Y,Z)$ is said to be on the surface.

Recent works like *IMNet* or *OccNet* predict such functions and have shown to be capable of avoiding the aforementioned drawbacks of explicit methods. Nonetheless, none of those works has been capable of reconstructing fine-grained details.

  

## A two-step approach

To achieve the goal of reconstructing both overall shape as well as fine-grained details, Wang et al. represent a 3D object implicitly using a Signed-Distance-Function (SDF). An SDF maps a point $P$ to a real value $s \in \mathbb{R}$ where the sign of $s$ tells whether $P$ is inside or outside of the 3D shape and the absolute value gives the distance of $P$ to the isosurface. As this function is continuous, DISN reconstructs objects with arbitrary resolution.

To predict this SDF they developed a feed-forward neural network that takes a single 2D image and a point in world coordinates $P(X, Y, Z)$ and returns the corresponding SDF value. Internally, this is done by using two consecutive networks: The first estimates the camera pose to map an object in world space to the image plane. Having this mapping a local feature extraction module is employed in the second (SDF predicting) network additionally to the global feature encoder.

  

### How is the camera pose estimated

For camera pose estimation they use the general approach proposed by Insafutdinov and Dosovitskiy. By using a Convolutional Neural Network several pose candidates are combined. However, their approach suffers from a large number of network parameters and a complex training procedure.

To reduce those disadvantages, the authors of DISN make use of recent research results, that continuous representations are easier to regress for Neural Networks. Zhou et al. have shown that e.g. a 6D rotation representation $b=(b_x,b_y)$ where $b \in \mathbb{R}^6, b_x \in \mathbb{R}^3, b_y \in \mathbb{R}^3$ is continuous, while quaternions and Euler angles are not, and is, therefore, better suited for regression in neural networks. Once $b$ is predicted, one can then obtain the rotation matrix $R =(R_x, R_y, R_z)^T \in \mathbb{R}^{(3x3)}$ with the following formulas:

$$R_x = N(b_x),\space R_z = N(R_x \times b_y),\space and\space R_y = R_z \times R_x$$

  

with N(\point) being the normalization function and \times the cross product.**[?Zhou et al. ]**

Translation $t \in \mathbb{R}^3$ is predicted directly.

  

When training this module the authors use the ShapeNet Core dataset **[25]** , where all objects are within the same aligned model space, and the renderings provided by Choy et al **[28]**. The model space of the original dataset is then set as the world space where all camera parameters are with respect to. For regression, a given world space point cloud $PC_w$ is transformed to camera space using predicted parameters and then compared to the camera space ground truth point cloud $PC_{cam}$.

As a regression loss they use the Mean-squared-error (MSE) resulting in:

$$L_{cam} = \frac{\sum_{p \in PC_w}||p_G-(Rp_w +t)||^2_2}{\sum_{p \in PC_w} 1}$$

  

### How is the Signed Distance Function predicted

The SDF prediction network consists of three different parts.

1.  A simple VGG-16 Encoder that extracts global features from the 2D image.
2.  A local feature extraction module. It uses the estimated camera pose to project the point $P \in \mathbb{R}^3$ onto a 2D location $q \in \mathbb{R}^2$ on the image plane. Having $q$ in each feature map the corresponding part is extracted and concatenated. As not all feature maps equal the size of the input image, bilinear interpolation is used to resize the feature maps and extract the values.
3.  A multilayer perceptron which maps the given point to a higher dimensional feature space. This is then concatenated to both the global and local features.

Finally decoding the global and local features results in an SDF value for the overall shape for the former, and a *residual* SDF for the later. Combining them trough simple summation results in an SDF that in addition to an overall shape also recovers the in previous approaches missing details of an object. The following figure illustrates the concrete structure of the network.

  

\image

  

For the loss calculation of the network, two things have to be taken into consideration. First, in contrast to e.g., IMNet one wants to recover different iso-levels and second, the network should concentrate on details near and inside the iso-surface. This, in consequence, leads to a weighted loss function of SDF values being defined as:

$$ L_{SDF} =\sum_p m | f(I,p) - SDF^I(p)|

\\m =\begin{cases}

m_1, &SDF^I(p) >\delta \\

m_2, & \text{otherwise}

\end{cases}$$

  

## Evaluation of DISN

In order to evaluate whether the goal of reconstructing high-quality fine-grained 3D shapes has been achieved extensive evaluation and comparison against the previously mentioned methods (**[...]**) have to been done. Herefore qualitative (visual), as well as quantitative evaluation results on single-view 3D reconstruction, are provided . Additionally, the performance of the adapted camera pose estimation was examined against the original approach. In the last step Ablation studies have been conducted showing again qualitative as well as quantitative results.

### Experimental setup

This includes the Dataset as well as the preparation training and testing implementation.

#### Dataset

For the training of the test setup the ShapeNet Core **[...]** dataset has been used. According to the official website (**LINK**: [https://www.shapenet.org/](https://www.shapenet.org/)) It "is a subset of the full ShapeNet dataset with single clean 3D models and manually verified category and alignment annotations. It covers 55 common object categories with about 51,300 unique 3D models." However, to make the evaluation comparable, the official training/test split on 13 object categories is used. Furthermore, to obtain 2D images the renderings of Choy et al **[28]** are employed. This is quite good work as most of the aforementioned other approaches (**[Atlas, Pixel,3DN, OccNet]** ) did it the same way.

*As an additional contribution they rendered a new 2D dataset (**LINK:**:https: //github.com/Xharlie/ShapenetRender_more_variation w) that contains 5 degrees of freedom (DoF) at a Resolution of $224\times224$ -- pairing each image also "with a depth image, a normal map and an albedo image provided by blender". While this is an improvement over Choy et al. providing only 3 DoF and a resolution of $137\times137$, it is not used in the official evaluation"*

  

#### Data Preparation

In the data preparation step, two things have to be done: The first, ground truth data for camera pose estimation is needed. Herefore, the rendering of Choy et al. is used. The renderings provide different viewpoints of the objects in the main data set together with annotation of their transformation from world to camera space. Second, SDF ground truth data has to be generated. Following the approaches of **[29,30]** this is done by an SDF grid resolution of $256^3$. Nonetheless, as one is mostly interested in SDF values close to the iso-surface it is not necessary to train on all $256^3 = 16,777,216$ values. To reduce this number, Monte Carlo sampling under Gaussian distribution $\mathbb{N}(0,0.1) is used to choose 2048 grid points for training.

  

#### Training and Testing

In the training procedure, the two networks (camera pose estimation and SDF prediction) are trained individually, using for the latter ground truth camera parameters. As hyperparameters using Adam optimizer the following values are chosen:

$$m_1 = 4, \space m_2 =1, \space \delta = 0.001 \\ \alpha = 0.0001,\space \text{batch size} = 16$$

Convergence takes 50 epochs.

  

Afterward -- for testing -- the estimated camera parameters are used. However, as presented later they also show results with ground truth parameters.

  

### Quantitative Evaluation

The improvements of using not only an implicit method but also a local feature extraction module are measured by four commonly used metrics:

1.  **Earth Mover's Distance (EMD)** is the minimum amount work that has to be done to match two distribution x and y -- in this case prediction and ground truth. Normally, x and y have to be normalized, however, as we are comparing two distributions of equal weights this is no issue. The work itself is calculated using the L2-norm resulting in:$$ EMD(PC,PC_T) = min_{\phi: PC->PC_T} \sum_{p \in PC} ||p-\phi(p)||_2$$ EMD is better the smaller the value is.

2.  **Chamfer Distance (CD)** calculates the matching distance to the nearest feature in both ways, from $PC to PC_T$ as well as the other way round. Here the distance is calculated as the *squared* L2-Norm leading to the following equation:
$$ CD(PC,PC_T) = \sum_{p_1 \in PC} min_{p_2 \in PC_T} ||p_1-p_2||^2_2$$CD is better the smaller the value is.

3.  **Intersection over Union (IoU)** is a ratio, measuring how much overlap is present between two distributions. The general formula is given by $IoU = \frac{Intersection}{Union}$. Sadly the paper does not mention any word how they calculated Intersection and Union. Nonetheless, for evaluation, we can say the larger the value the better.
4.  **F-score** gives a percentage of how much area was reconstructed correctly. For its calculation, we need two measures: 
	- $Precision = \frac{|predicted poi}{}$Precision and Recall. 
The former describes a ratio between all predicted points with a distance to the closest ground truth point smaller than a threshold $t$ and all generated points, while the later similarly describes a ratio between all ground truth points with a distance to the closest predicted point smaller than a threshold $t$. Having precision and recall, the F-score is calculated by:

$$ \text{F-score} =2* \frac{Precision*Recall}{Precision+Recall}$$

Here counts the higher the better, while a small threshold describes the biggest similarity.

  

####Pose Estimation results

  

### Qualitative Evaluation

  

###Ablation studies

  

##Additional Work

  

## Conclusion

  

### What the author thinks

  

### What I think

  

##Sources
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4NTM1MDQxMSw5MTQ2NTUxMjQsLTExMz
A3NDcyNTgsLTE5MjMyNjA0NzIsMTQ3MjM1NzU0LDk1NTU0MjA2
MiwtMTY2Mzk3OTM5Myw1OTM5MjA5MzYsMTk4NjkwODMwNiwtMT
MyMjMwODg3MywyMDc1MTA1MTI2LC03NzU3NTYxOTQsMzYxOTQ3
MzAwLC0xMTI4NjE0NzI3LDkwMjY0MTc5NSwtMzIwMTU2MiwtMj
EyMTY5MzYwMiw1NTQwNjc4MDksLTIxNDYyOTM2MjQsMTUyNjEy
NzQ4Nl19
-->