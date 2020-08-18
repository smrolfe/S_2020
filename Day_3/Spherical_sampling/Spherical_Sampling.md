## Spherical Sampling

This method uses a sampled template to place semi-landmark points on the surface of a mesh. The landmark placement is constrained to the external surface of the mesh. Points sampled on the template are projected to the mesh surface along the surface normals of the template. Once the initial intersections are found with the base mesh, a second projection is done along the surface normals of the base mesh to locate the most external mesh intersections. The projected points are then filtered to remove those witin the sample spacing distance, improving regularity of sampling. This module can be used to generate a large number of points on a mesh with no manual landmarks. These landmarks can then be transferred to individual specimens using the 'ALPACA' module.

### Sphere template
1. Download the Gorilla Skull Reference Model from the 'Sample Data' (will be in your Cache folder). Load the mesh (PLY) into Slicer.

2. Navigate to the 'Spherical Sampling' module, located in the SlicerMorph Labs folder. Select the loaded gorilla skull as the base mesh. The spacing tolerence will set the spacing of the sampled points as a factor of the diagonal length of the selected image. For this example, select a spacing tolerance of 3%. 

The template geometry will determine the shape of the estimted sampling template. For this example, choose the 'Sphere' option. With the parameters of the template set, you can check the initial number of sampled points on the template that will be projected to the base mesh. This number will be greater than or equal to the final number of sampled points since the final spatial filtering step will remove some points. Select the 'Get subsample number' button to display the number of points on the sampling sphere in the 'Sampling Information' window. You should have a spherical template with 934 points. This step can be repeated with a different spacing tolerance if the number of points displayed is to high or low.

<img src="./Picture1.png">

3. Click the 'Generate template' button to display the sphere template. The template is centered at the arithmatic center of the loaded mesh and has radius defined by the image diagonal. This default radius can be adjusted using the 'Template scale factor' slider. For this example, you can use the default scale factor, 110%.

<img src="./Picture2.png">

4. Click the 'Project points to surface' button to project the points from the sphere to the base mesh. The first step in this process inflates or deflates the point position along the normal vector of the sphere at that point until the most external intersection with the mesh is found. The second step takes this initial point placement on the base mesh and again inflates and deflates the point position, this time along the normal vector of the base mesh to find the most external point. The projected points are displayed on the base mesh.

<img src="./Picture3.png">

5. Select the 'Enforce spatial sampling rate' button to remove samples with a point-to-point distance lower than the spatial sampling rate. This improves the regularity of the sampling over the mesh surface. This step may take a couple minutes. The wait time will increase with the size of the sampled point set. The final number of points after filtering will be diplayed in the 'Sampling Information' window. There should be 795 points remaining.  The final sampled point set will be displayed on the base mesh. The points have been placed over the external surface area of the mesh, but some areas of the skull with high curvature have a low sample density.

<img src="./Picture4.png">

### Template estimated from the specimen geometry
To address the low sampling rate in areas of high curvature, the sampling rate could be increased, but this will significantly increase processing time. One solution is to use a template with geometry closer to that of the specimen. 

1. As in the previous example, select the loaded gorilla skull as the base mesh and set the spacing tolerance to 3%. Select the 'Original Geometry' option for the template geometry, and check the number of sampled points by clicking the 'Get subsample number' button. You should see 1052 sampled points.

<img src="./Picture5.png">

2. Click the 'Generate template' button. This time, you will see a template mesh that is an approximation of the gorilla skull.

<img src="./Picture5_5.png">

3. Select the 'Project points' button, followed by the 'Enforce spatial sampling rate' button. The spatial filtering may take a few minutes. When complete, the final spherically sampled point set will be displayed on the base mesh. This point set provides more regular coverage of the mesh surface and performs better in areas of high curvature. 

<img src="./Picture6.png">

4. The output points can be saved from the 'Data' module by right clicking the node named 'sphericalSampledLandmarks', selecting 'Export as' and choosing the export file type as .CSV.

<img src="./Picture7.png">