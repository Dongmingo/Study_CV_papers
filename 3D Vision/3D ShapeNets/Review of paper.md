# 3D ShapeNets : A Deep Representation for Volumetric Shapes

## Purpose of Paper
 <p> Building first 3D deep learning model. Propose a convolutional deep belief network to represent a geometric 3D shape as a probability distribution of binary variables on a 3D voxel grid. Train with 3D CAD dataset(ModelNet),
   Then model can jointly recognize and reconstruct objects from a single-view 2.5D depth map (e.g. RGB-D)</p>
 <p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124710983-7cce7580-df38-11eb-94dc-4f52a2f39ca4.png" width="50%"></p>
 
## Problems of Related Work
(1) Traditional methods dealing 3d dataset are limited in several problems : a specific class of shapes with small variations with surface correspondence,
can only tackle small holes or deficiencies, quality of abailable templates and often do not provide different semantic interpretations of reconstrutions  
(2) There is some models using depth maps, but not model in full 3D

## Key Structures
- View-based Sampling (reconstruction)
- Next-Best-View Algorithm (recognition)
<p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124711487-18f87c80-df39-11eb-9f5e-6f96ec43587a.png"></p>

## Network Architetcture and Visualization of model learning while training 
<p align ="center"><img src="https://user-images.githubusercontent.com/61967107/124711269-d5057780-df38-11eb-84b7-9b3641b63c97.png"></p>

## Limitations (problems in active object recognition)
 Unlike static object recognition, the seonsor in active object recognition should move to next view point to gather more information
