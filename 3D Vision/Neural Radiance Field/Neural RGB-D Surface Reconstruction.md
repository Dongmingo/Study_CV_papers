# Neural RGB-D Surface Reconstruction

## Purpose of Paper
1. Extend to use depth measurements with a commodity RGB-D sensor
2. Can reconstruct high qualiity with novel view synthesis with commercial cameras
3. Able to reconstruct geometry detail that is observed only in color, not visible in depth
 <p align ="center"><img src="https://user-images.githubusercontent.com/61967107/168423682-5965a85f-8d1b-468e-9a11-6ac795e0782f.png" width="100%"></p>

## Problems of Related Work
1. NeRF, marching cubes -> not exact point reconstruction -> limited at reproduction
2. Classic reconstructions (Differentiable Volumetric Rendering, KinectFusion)... -> uses depth camera, sensors which limits performance
3. BundleFusion uses colors to compute sparse SIFT, but uses depth to reconstruct scene -> so if there is missing depth -> holes
4. Neus tries to recon with RGB. but cant reconstruct featureless white wall

## Related Works
1. Classical fusion based 3D reconstructions (Not based on deep learning)
  - Stereo matching from two or multiple color views
    - [29]Multi-view stereo for community photo collections (ICCV 07')
    - [62]A taxonomy and evaluation of dense two-frame stereo correspondence algorithms (SMBV 01')
  - Structure-from-motion
    - [63]Structure-from-motion revisited (CVPR 16')
  - SLAM-based
    - [20]LSD-SLAM: Large-scale direct monocular SLAM (ECCV 14')
    - [21]Semi-dense visual odometry for monocular camera (ICCV 13')
    - [23]Svo: Fast semi-direct monocular visual odometry (ICRA 14')
  - Using disjoint representations
    - [25]Accurate, dense and robust multi-view stereopsis (IPAMI 10') : Oriented patches
    - [38]A theory of shape by space carving (00') : Volumes
    - [32]Towards high-resolution large-scale multi-view stereo (ICCV 09') : Meshes
=> based on [9]A volumetric method for building complex models from range images (SIGGRAPH 96') : multiple depth measurements are fused using SDF
  - [50]Kinectfusion: Real-time dense surface mapping and tracking (ISMAR 11') : combines representations into real-time tracking
  - [53]Real-time 3d reconstruction at scale using voxel hasing (TOG 13') : handle large scene propose a memory-efficient stroage of SDF
  - [14]BundleFusion: Real-time globally consistent 3d reconstruction using on-the-fly surface registration (TOG 17') : BA for loop closure
  - Handling outliers during reconstruction
    - [19]PSDF fusion: Probabilistic signed distance function for on-the-fly 3d data fusion and scene reconstruction (CoRR 18')
    - [61]A taxonomy and evaluation of dense two-frame stereo correspondence algorithms (SMBV 01')
    - [89]A globally optimal algorithm for robus tv-l range image integration (IEEE 07')
2. Deep Learning for 3D Reconstruction
  - Predict Depth from color images
    - [24]Deep ordinal regression network for monocular depth estimation (ICCV 18')
    - [28]Unsupervised monocular depth estimation with left-right consistency (ICCV 17')
    - [39]Deeper depth prediction with fully convolutional residual networks (3DV 16')
  - Learn multi-view stereo using 3D CNNs on voxel grids
    - [34]Learning a multi-view stereo machine (NeurIPS 17')
    - [68]Deep-voxels: Learning persistent 3d feature embeddings (CVPR 19')
    - [82]Mvsnes: Depth inference for unstructured multi-view stereo (ECCV 18')
  - Multi-plane images & learn image features for SLAM
    - [2]Codeslam --learning a compact, optimisable representation for dense visual slam (CVPR 18')
  - Reduce the influence of noisy depth values
    - [79]Routedfusion: Learning real-time depth map fusion (CVPR 20')
  - Complete incomplete scans
    - [13]Sg-nn: Sparse generative neural networks for self-supervised scene completion of rgb-d scans (CVPR 20')
    - [15]Spsg: Self-supervised photometric scene generation from rgb-d scans (CVPR 21')
  - Learn image features for SLAM
    - [10]Deepfactors: Real-time probabilistic dense monocular slam (IRAL 20')
    - [91]Scenecode: Monocular dense semantic reconstruction using learned encoded scene representations (CVPR 19')
  - Feature fusion
    - [4]Transformerfusion: Monocular rgb scene reconstruction using transformers (NeurIPS 21')
    - [71]Fourier features let networks learn high frequency functions in low dimensional domains (NeuraIPS 20')
    - [80]Neuralfusion: Online depth fusion in latent space (CVPR 21')
  - Predict normals
    - [90]Deep depth completion of a single rgb-d image (CVPR 18')
  - Predict objects or parts of a room from single images
    - [11]Panoptic 3D scene reconstruction from a single RGB image (NeurIPS 21')
    - [18]3d scene reconstruction from a single viewport (ECCV 20')
    - [27]Mesh R-CNN (CVPR 19')
    - [51]Total3DUnderstanding: Joint layout, object pose and mesh reconstruction for indoor scenes from a single image (CVPR 20')
    - [75]Pixel2mesh: Generating 3d mesh models from single rgb images (ECCV 18')
  - Coordinate-based model (MLP)
    - [74]Advances in neural rendering
    - [73]State of the art on neural rendering (Computer Graphics Forum 20')
  - MLP outputs occupancy
    - [7]Implicit functions in feature space for 3d shape reconstruction and completion (CVPR 20')
    - [47]Occupancy networks: Learning 3d reconstruction in function space (CVPR 19')
    - [52]Differentiable volumetric redering: Learning implicit 3d representations without 3d supervision (CVPR 20')
    - [55]Deepsdf: Learning continuous signed distance functions for shape representation (CVPR 19')
    - [58]Convolutional occupancy networks (ECCV 20')
    - [59]Pifu: Pixel-aligned implicit function for high-resolution clothed human digitzation (CVPR 19')
    - [60]Pifuhd: Multi-level pixel-aligned implicit function for high-resolution 3d human digitizing (20')
 3. NeRF
  - MLP outputs density, radiance
    - [48]NeRF: Representing scenes as neural radiance fields for view synthesis (ECCV 20')
  - MLP outputs color
    - [54]Unisurf: Unifying neural implicit surfaces and radiance fields for multi-view reconstruction (ICCV 21')
  - MLP outputs SDF
    - [56]Deepsdf: Learning continuous signed distance functions for shape representation (CVPR 19')
    - [83]Volume rendering of neural implicit surfaces (NeuraIPS 21')
    - [84]Multiview neural surface reconstruction by disentangling geometry and appearance (NeurIPS 20')
  - [69]Scene representation networks: Continuous 3d structure-aware neural scene representations : Combine such representation with learned renderer
  - Alternative positional encodings in NeRF (Sinusoidal)
    - [72]Fourier features let networks learn high freaquency functions in low dimentional domains (NeurIPS 20') : Fourier features
    - [67]Implicit neural representations with periodic activation functions (NeurIPS 20') : Sinusoidal activation layer
  - Wild data
    - [45]NeRF in the Wild: Neural Radiance Fields for Unconstrained Photo Collections (CVPR 21')
  - Dynamic scene
    - [40]Neural scene flow fields for space-time view synthesis of dynamic scene (CVPR 21')
    - [57]Deformable neural radiance fields (CVPR 21')
  - Avatars
    - [26]Dynamic neural radiance fields for monocular 4d facial avatar reconstruction (CVPR 21')
  - Adapting to generative modeling
    - [5]Matterport3d: Learning from rgb-d data in indoor environments (arXiv 20')
    - [66]Graf: Generative radiance fields for 3d-aware image synthesis (NeurIPS 20)
  - Image-based rendering
    - [77]Ibrnet: Learning multi-view image-based rendering (CVPR 21')
    - [87]pixelnerf: Neural radiance fields from one or few images (CVPR 21')
  - Resectioning a camera given a learned NeRF
    - [85]inerf: Inverting neural radiance fields for pose estimation  (IROS 21')
  - Optimizing the camera Poses
    - [41]Barf: Bundle-adjusting neural radiance fields (ICCV 21')
    - [78]NeRF-: Neural radiance fields without known camera parameters (arXiv 21')
4. Concurrent work
  - [76]Neus: Learning neural implicit surfaces by volume rendering for multi-view reconstruction (arXiv 21') : uses an implicit surface representation to improve novel view synthesis of NeRF
  - [81]Nerfingmvs: Guided optimization of neural radiance fields for indoor multi-voew stereo (CVPR 21') : propose a multi-view stereo approach to estimate dense depth maps which they use to constrain the sampling region when optimizing NeRF
  - [49]DONeRF: Towards Real-Time Rendering of Compact Neural Radiance Fields using Depth Oracle networks (Computer Graphics Forum 21') : restrict the volumetric rendering to near surface regions
  - [16]Depth-supervised nerf: Fewer views and faster training for free (arXiv 21') : additional constraints on the depth predictions of NeRF



=> Uses NeRF to learn a TSDF

 <p align ="center"><img src="https://user-images.githubusercontent.com/61967107/168461973-74d5962f-63ed-41b3-9eac-9e2aaf62f3df.png" width="100%"></p>


## Key Structures
- Direct SDF-based loss on input depth maps
- Structure 2
<p align ="center"><img src="example_image_2"></p>

## Network Architetcture and Visualization of model learning while training 
<p align ="center"><img src="example_image_3"></p>

## Limitations (problems in active object recognition)
(1) limitations 1

## Training Details
- Jointly optimize scene with camera poses (Initialize with BundleFusion)
- Scene is represented using MLPs, encoding distance value, view-point dependant $D_i$ & $c_i$ per point $p_i$

## Evaluation
- Evaluate both on Synthetic data and Real Dataset(ScanNet)
- use Marching Cubes to extract trianglue mesh from the optimized implicit scene representation
#### link, citations
 
