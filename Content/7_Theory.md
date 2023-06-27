
### Fundamentals of Geographic Information Systems (GIS)

# Theory 7: Spatial Interpolation

Spatial interpolation is a technique used in GIS to estimate values at unsampled locations based on known measurements from surrounding locations. It is a method of creating continuous surfaces or maps of a particular phenomenon across a study area where data points are limited or unevenly distributed.

For example, in air pollution analysis, spatial interpolation allows for the estimation of pollutant concentrations at locations where direct measurements are not available or sparse. It helps fill in data gaps and provides a more comprehensive representation of pollutant levels across the study area. By utilizing mathematical models and statistical techniques, spatial interpolation generates a continuous surface that represents the varying concentration of pollutants, providing a smoother representation of the spatial patterns.

There are several spatial interpolation methods commonly used, each with its own strengths and limitations. The choice of interpolation method depends on the characteristics of the dataset, the spatial patterns of the phenomenon being analyzed, and the desired level of accuracy. It is important to assess the reliability and accuracy of the chosen interpolation technique by considering factors such as the data distribution, spatial dependence, and the underlying assumptions of the method.

### Inverse Distance Weighted (IDW)[^1]
One of the most common spatial interpolation methods is Inverse Distance Weighted (IDW). In the IDW interpolation method, the sample points are weighted during interpolation such that the influence of one point relative to another declines with distance from the unknown point you want to create.

![](https://docs.qgis.org/2.18/en/_images/idw_interpolation.png)[^1]

Weighting is assigned to sample points through the use of a weighting coefficient that controls how the weighting influence will drop off as the distance from new point increases. The greater the weighting coefficient, the less the effect points will have if they are far from the unknown point during the interpolation process. As the coefficient increases, the value of the unknown point approaches the value of the nearest observational point.

It is important to notice that the IDW interpolation method also has some disadvantages: the quality of the interpolation result can decrease, if the distribution of sample data points is uneven. Furthermore, maximum and minimum values in the interpolated surface can only occur at sample data points. This often results in small peaks and pits around the sample data points.

In GIS, interpolation results are usually shown as a 2 dimensional raster layer.



[^1]: https://docs.qgis.org/2.18/en/docs/gentle_gis_introduction/spatial_analysis_interpolation.html 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2MTkwOTU0NywtMTgyNjYxMzA0MF19
-->