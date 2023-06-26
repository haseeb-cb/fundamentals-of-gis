### Fundamentals of Geographic Information Systems (GIS)

# Theory 6: Thiessen polygons and heatmapping (kernel density estimation)

## Heatmap analysis
Spatial phenomena tend to vary in intensity across a geographical area. When the occurrence of a certain phenomenon is significantly higher in one area than in the surrounding area, you could describe it as a “hotspot” for that phenomenon. For instance, cities are hotspots of buildings and human activity, forests are hotspots of trees etc. There are many ways to locate these hotspots: interpolation, cluster analysis, and heatmap analysis, to name a few. Today we’re taking a look at heatmaps and heatmap analysis. 

As the name would suggest, heatmaps describe the “heat,” or intensity, of the phenomenon in question. Heatmaps are generated with point feature data and form a raster layer. In its most rudimentary form, the pixel values of a heatmap depict proximity to other point features within a certain, user-specified, radius. A slightly more advanced form of heatmaps can be given a weight (from the point features’ attribute table) that will influence the pixel values.

For instance, two heatmaps are created out of the same point feature layer (bus stops). One heatmap wasn’t given a weight, so it only looks for other bus stops within a certain radius, e.g. 500 meters. The other was given a weight, e.g. daily passenger amount, from the attribute table of the bus stops layer. To generate this other heatmap, the GIS software not only looks for bus stops within a radius of 500 meters of each other, but also gives the bus stops with higher passenger amounts a higher weight. Thus, the bus stops with a high daily passenger amount will be “favored” in the resulting heatmap raster layer.

One step more advanced form of heatmap will also include modification of the kernel shape. Kernel is the statistical function used to give proximity and weight scores to the point features within the radius. Heatmaps are also known as kernel density analysis.

### What happens in Kernel Density Analysis?

To understand the basic idea of Kernel Density Analysis that we use to create a heatmap, you can watch this 9 minutes long video (Point Pattern Analysis Part 5: Kernel Density Estimation): https://www.youtube.com/watch?v=PBZVTjmhl74

When applying the kernel method, QGIS draws a circular neighborhood around each sample point (not each cell) and then applies a math function that goes from 1 at the location of the point to 0 at the neighborhood boundary. Think of a kernel as a smoothly curved surface that is fitted over each point.

![](http://www.geography.hunter.cuny.edu/~jochen/gtech361/lectures/lecture11/concepts/Kernel%20density%20calculations_files/image001.gif)
When a kernel function is applied to each data point, the effect is like that of an elevation surface, except that the density value for each cell is calculated by adding the values of all the kernel surfaces where they overlay the cell center.

![](http://www.geography.hunter.cuny.edu/~jochen/gtech361/lectures/lecture11/concepts/Kernel%20density%20calculations_files/image002.gif)
The kernel function generally creates a smoother-looking surface than one created with the simple method[^1].

If you still have difficulty understanding this concept, try out this video: https://www.youtube.com/watch?v=x5zLaWT5KPs
Otherwise, don't worry about it for now and move on! 

- Delimited Text Layer
- Voronoi/Thiessen polygons
- Heatmaps (kernel density estimation)
	- Radius
	- Pixel size
	- Kernel shape
	- Weight

[^1]: http://www.geography.hunter.cuny.edu/~jochen/gtech361/lectures/lecture11/concepts/Kernel%20density%20calculations.htm
<!--stackedit_data:
eyJoaXN0b3J5IjpbODMxNjgyOTg3LDExMjQ1MDg0ODgsLTY5MT
M3ODUwOV19
-->