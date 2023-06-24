
### Fundamentals of Geographic Information Systems (GIS)

# Theory 4: Digital Elevation Model, Hillshade, and raster overlay analysis

## Digital Elevation Model (DEM)
A digital elevation model (DEM) is a three-dimensional representation of the Earth's surface that is created using elevation data. It is a digital representation of the topography of a particular area, typically displayed as a grid of elevation values.

- Example picture of DEM

DEM data is collected using various methods, including remote sensing techniques such as LiDAR (Light Detection and Ranging), radar, or photogrammetry. These methods involve sending out signals or capturing images from different perspectives to measure the height of the Earth's surface at specific points.

- Example picture of capturing technique

The resulting elevation data is then processed and interpolated to create a continuous representation of the terrain. The grid of elevation values in a DEM is often represented as a raster dataset, where each cell or pixel contains the elevation information for that location.

DEM data has numerous applications in various fields, including geography, geology, environmental science, urban planning, and engineering. It is used for visualizing and analyzing terrain characteristics, mapping landforms, identifying slopes and aspect, hydrological modeling, determining visibility and line of sight, and more. DEMs are essential in creating accurate maps, conducting terrain analysis, and supporting decision-making processes in numerous industries and research domains.

### Filling sinks in a DEM
Filling sinks in a DEM is an important preprocessing step that addresses a common issue in elevation data. A sink refers to a depression or low-lying area in the terrain where water can accumulate, such as a small basin or a closed contour. When sinks are present in a DEM, they can introduce inaccuracies and create problems in subsequent analyses or applications. 

The process of filling sinks typically involves identifying the depressions or sinks in the DEM and modifying the elevation values within those areas to ensure a continuous and realistic representation of the terrain. This can be done using various algorithms or techniques, such as the breaching or filling algorithms, which raise the elevation of the sinks until they reach the surrounding terrain level. By filling sinks, the DEM becomes more suitable for accurate and reliable analysis and visualization of the terrain.

(Want to learn more about why and when filling sinks in necessary? Check videos such as: https://www.youtube.com/watch?v=6rcx4OwnryI)

### Hillshade
The hillshade technique is a method used to create a shaded relief representation of a DEM or terrain surface. It simulates the effects of lighting on the terrain to enhance the visual perception of the three-dimensional characteristics of the landscape. The resulting hillshade image provides a sense of depth and helps to emphasize the topographic features of the terrain.

- Example picture of hillshade

The hillshade technique calculates the illumination and shadows on the terrain surface based on the direction of the light source, the elevation values of the DEM, and the slope and aspect of each pixel. 

The hillshade technique is widely used in cartography, geospatial analysis, and visualization applications. It helps in understanding the topography of an area, identifying landforms, visualizing slopes and ridges, and enhancing the aesthetics of terrain maps.

### Slope
A DEM provides the necessary data to perform slope analysis. With a DEM, you can calculate and analyze the slope of the terrain at various locations. Slope analysis allows you to understand the steepness of the landscape, identify areas of high or low slope, and assess the terrain characteristics for various applications.

- Slope picture

Slope analysis using a DEM is valuable in a range of applications, including terrain characterization, land management, environmental assessment, and infrastructure planning. It provides insights into the topographic features of the landscape, supporting decision-making processes and aiding in understanding the terrain's behavior and suitability for various purposes.

## Raster overlay analysis
- Data reclassification
- Raster calculator
- Raster overlay analysis (calculations)


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJZOTg1QlJqQ284RDI1UWFyIjp7In
N0YXJ0Ijo0MjMsImVuZCI6NDQ3LCJ0ZXh0IjoiLSBFeGFtcGxl
IHBpY3R1cmUgb2YgREVNIn0sIjhTa2RvdUQ4NmFSMUxkUlEiOn
sic3RhcnQiOjc1NywiZW5kIjo3OTcsInRleHQiOiItIEV4YW1w
bGUgcGljdHVyZSBvZiBjYXB0dXJpbmcgdGVjaG5pcXVlIn0sIn
JTbUZjZjRmalFXNWh5MEYiOnsic3RhcnQiOjMwMTUsImVuZCI6
MzA0NSwidGV4dCI6Ii0gRXhhbXBsZSBwaWN0dXJlIG9mIGhpbG
xzaGFkZSJ9LCJGYkFjVkZlZEZVOHdTOWJjIjp7InN0YXJ0Ijoz
ODUwLCJlbmQiOjM4NjUsInRleHQiOiItIFNsb3BlIHBpY3R1cm
UifX0sImNvbW1lbnRzIjp7InR1eGhlaHlzeTRqRWxTVUQiOnsi
ZGlzY3Vzc2lvbklkIjoiWTk4NUJSakNvOEQyNVFhciIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzU4MjYwMTA3NH0sIjFIN2dnYjVpeE8ycV
BEc1AiOnsiZGlzY3Vzc2lvbklkIjoiOFNrZG91RDg2YVIxTGRS
USIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaW
N0dXJlIiwiY3JlYXRlZCI6MTY4NzU4MjYzNTE3MH0sIkhZbENS
NzJFUEgyanZxOXUiOnsiZGlzY3Vzc2lvbklkIjoiclNtRmNmNG
ZqUVc1aHkwRiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzU4Mjg0MzM3OX
0sIlZHeHUyNG5IRWRrYmVuSUgiOnsiZGlzY3Vzc2lvbklkIjoi
RmJBY1ZGZWRGVTh3UzliYyIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzU4
Mjk4MzAxOH19LCJoaXN0b3J5IjpbLTE3ODI0NjgwNDgsOTk0Nz
IwMTkzLC0zNTEwNzY1ODAsLTEzOTAzMzIwNTFdfQ==
-->