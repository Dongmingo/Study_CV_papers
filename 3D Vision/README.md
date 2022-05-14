# Datatypes of 3D datasets

## 1. Ordered dataset(Euclidian)
- Primitives: Datasets based on mathematical basis, is composed of common shapes like cube, plane, shphere, polygon, donut, cone... and control points that transforms the data.
 <p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124564295-e3418e00-de7b-11eb-92dc-4dddff2c551a.png", width = "50%"></p>

- Projection : Mapping into shperical coordinate, or cylinderical coordinate<br>
- RGB-D : Express the data seperating color data(RGB) and depth. Can only shows the data in a specific field of view
<p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124566116-b7270c80-de7d-11eb-9b28-650e8529f87f.png", width = "50%"></p>

- Voxel grid : Volume + pixel, Represents a value on a regular grid in 3D space. Infer the position of a boxel based upon its position relative to other voxels. Seems like minecraft dataset
<p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124566894-6bc12e00-de7e-11eb-8076-df460076f7a5.png", width = "50%"></p>

- Multi vision : Project the 3d data into colored 2d datas in several points of views 
<p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124569584-0b7fbb80-de81-11eb-9fac-4cf809d9e068.png", width = "50%"></p>

## 2. Unordered Dataset(Nun Euclidian)

- Point cloud : Consists of points including the informations of location and color, typical output of 3d scanner
<p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124571457-c197d500-de82-11eb-948d-376b72064bfc.png", width = "50%"></p>

- Graph : Datatype similar to mesh, Vertex <-> Node, Edge <-> Connecting information
<p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124571057-6a920000-de82-11eb-9d81-53d910737e2b.png", width = "30%"></p>

- Mesh : Consists of Vertex(point), Edge, Polygon(Usually triangle, quadrangle)
<p align = "center"><img src = "https://user-images.githubusercontent.com/61967107/124571314-a3ca7000-de82-11eb-9167-1b9b0db11c1c.png", width = "50%"></p>

