# PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation

## Purpose of Paper
 <p>Point cloud is a irregular 3d data format. Due to arising issues while transforming into 3D voxel grid or collections of image. The paper suggests PointNet to directly consumes point cloud data for application of Classification, Part Segmentation, Semantic Segmentation.</p>
 <p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124243029-58e5eb00-db58-11eb-9fca-f72088ba0bf6.png" width="50%"></p>
 
## Problems of Point Cloud data
(1) Unordered : n! permutation inputs should make same results  
(2) Interaction among points : local features should be extracted within adjacent points  
(3) Invariance under transformation : The rigid transformation(rotation, translation, reflection) of input data shouldn't affect the result

## Key Structures
- Max Pooling and mlp : Solution for Problem (1), (2)
<p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124255793-86856100-db65-11eb-841f-9a5b00cfd10c.png" width="50%"></p>
<p align = "center">h is mlp(feature extraction), g is maxpooling function(symmetric function : Regardless of input data order)</p>

- mini-pointnet : T-Net (Joint Alignment Network : Use the idea of 'Spatial Transformer network', NIPS, 2015) : Solution for Problem (3)
<p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124259732-cf3f1900-db69-11eb-898e-6990be130a0e.png" width="70%"></p>
<p>Input Transformation - Assume sampling grid : 3 x 3 Transformation matrix</p>
<p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124261171-71133580-db6b-11eb-880d-572768a6b995.png" width="20%"></p>
<p>Feature Transformation - Assume sampling grid with Loss function L(To make orthogonal matrix): 64 x 64 Transformation matrix</p>


## Network Architetcture
<p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124250189-94d07e80-db5f-11eb-9a9c-b4cf71684561.png"></p>

### Model for Classification Task (Blue box)
- Input n points are consist of (x, y, z) : n x 3
- Input Transfom for each points(T-Net)
- Feature extraction with (64,64) mlp on each points : n x 64
- Feature Transform for each points(T-Net)
- Feature extraction with (64,128,1024) mlp on each points : n x 1024
- Max Pooling to Extract Global Features : 1 x 1024
- Extract Output scores for k classes with (512,256,k) mlp : 1 x k

### Model for Segmentation Task (Yellow box)
- Same procedure with model for classification
- Concatenate local features with global features : [n x 64 : n x 1024] -> n x 1088
- Feature extration with (512,256,128) mlp on each points : n x 128
- Extract Output scores for m classes with (128,m) mlp : n x m
