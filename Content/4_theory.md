
### Fundamentals of Geographic Information Systems (GIS)

# Theory 4: Buffer and overlay analysis

## Buffer analysis
GIS buffer analysis is a spatial analysis technique used to create proximity zones or buffers around spatial features. A buffer is a defined area around a geographic object, such as a point, line, or polygon, that represents a specific distance or range. The buffer can be created by measuring a fixed distance from the object or by using other criteria, such as travel time or risk factors.

Buffer analysis is commonly used in GIS to answer questions about spatial relationships and proximity. By creating buffers around specific features, analysts can determine which other features fall within or intersect those buffers. This can be helpful in various applications, including urban planning, environmental impact assessment, transportation analysis, and emergency response planning.

The process of buffer analysis involves the following steps:

1.  Define the input feature: Identify the geographic object for which you want to create a buffer. This could be a point, line, or polygon representing a specific feature like a building, road, or water body.
    
2.  Specify buffer distance: Determine the distance or range that defines the buffer zone around the feature. It can be a fixed distance (e.g., 100 meters) or vary based on specific criteria.
    
3.  Create buffers: Apply the buffer distance to the input feature to generate the buffer zones. This involves calculating the geometric shape (e.g., circle, polygon) that represents the buffer for each feature.
    
4.  Analyze buffer intersections: Assess the spatial relationships between the buffer zones and other features in the GIS dataset. This can involve identifying features that intersect, touch, or fall completely within the buffer zones.
    
5.  Derive insights: Interpret the results of the buffer analysis to gain insights about the proximity and relationships between different geographic features. This information can be used for decision-making, planning, and resource allocation.
    
Buffer analysis can be performed using GIS software, which provides tools and functions for creating buffers and analyzing the spatial relationships. The specific capabilities and options for buffer analysis may vary depending on the GIS software being used.

## Overlay analysis
GIS overlay analysis, also known as spatial overlay analysis, is a technique used in Geographic Information Systems (GIS) to combine multiple spatial datasets to derive new information and gain insights about their spatial relationships. Overlay analysis involves overlaying multiple layers or maps to create a composite map that integrates the attributes and geometry of the input datasets.



The overlay analysis process involves the following steps:

1.  Select input datasets: Identify the layers or maps that you want to overlay. Each layer represents a different geographic feature or theme, such as land use, population density, transportation networks, or environmental factors.
    
2.  Define overlay operation: Determine the specific type of overlay operation to be performed. There are several common types of overlay operations, including:
        
3.  Perform the overlay: Apply the selected overlay operation to the input datasets. This involves comparing the spatial positions and attributes of the features in each layer and creating the output layer based on the overlay rules.
    
4.  Analyze the results: Interpret the output layer to gain insights and extract useful information. The overlay analysis can reveal patterns, relationships, and spatial dependencies between different geographic features.
    
Overlay analysis is a powerful tool in GIS because it allows the combination and integration of multiple datasets to generate new information and support decision-making processes. It is commonly used in various applications, such as land-use planning, environmental analysis, market research, demographic analysis, and infrastructure development. GIS software provides tools and functions to perform overlay analysis, and the specific capabilities may vary depending on the software used.

## Overlay operations 

![](https://saylordotorg.github.io/text_essentials-of-geographic-information-systems/section_11/a33268f6ff028c24152080d0aa3f2aad.jpg)[^1]
- (a) Union: The union operation combines all the input datasets to create a single output layer that includes the combined geometry and attributes of all features from the input layers.

- (b) Intersection: This operation identifies the spatial extent where the input datasets overlap or intersect. The resulting output will include only the areas that are common to all input datasets.

- (c) Symmetrical Difference: This operation identifies the areas that are unique to each input dataset, including the overlapping portions.

- (d) **Identify**: Creates an output layer with the spatial extent of the input layer but includes attribute information from the overlay.

In addition to the aforementioned vector overlay methods, **other common multiple layer geoprocessing options** are available to the user. These included the clip, erase, and split tools.

- (e) **Clip**: Used to extract those features from an input point, line, or polygon layer that falls within the spatial extent of the clip layer.

- (f) **Erase**: Whereas the clip tool preserves areas within an input layer, the erase tool preserves only those areas outside the extent of the erase layer.

- (g) **Split**: Used to divide an input layer into two or more layers based on a split layer.

(Hungry for more? Check out this in-detail description of Multiple Layer Analysis: https://saylordotorg.github.io/text_essentials-of-geographic-information-systems/s11-02-multiple-layer-analysis.html)

### Geometric predicates
Geometric predicates are functions used to determine the spatial relation a feature has with another by comparing whether and how their geometries share a portion of space. They are often part of the options when doing overlay analysis, come back to this section when you run into them. 

![](https://docs.qgis.org/3.28/en/_images/selectbylocation.png)
Using the figure above, we are looking for the green circles by spatially comparing them to the orange rectangle feature. Available geometric predicates are[^2]:

- **Intersect**: Tests whether a geometry intersects another. Returns 1 (true) if the geometries spatially intersect (share any portion of space - overlap or touch) and 0 if they don’t. In the picture above, this will return circles 1, 2 and 3.

- **Contain**: Returns 1 (true) if and only if no points of b lie in the exterior of a, and at least one point of the interior of b lies in the interior of a. In the picture, no circle is returned, but the rectangle would be if you would look for it the other way around, as it contains circle 1 completely. This is the opposite of _are within_.

- **Disjoint**: Returns 1 (true) if the geometries do not share any portion of space (no overlap, not touching). Only circle 4 is returned.

- **Equal**: Returns 1 (true) if and only if geometries are exactly the same. No circles will be returned.

- **Touch**: Tests whether a geometry touches another. Returns 1 (true) if the geometries have at least one point in common, but their interiors do not intersect. Only circle 3 is returned.

- **Overlap**: Tests whether a geometry overlaps another. Returns 1 (true) if the geometries share space, are of the same dimension, but are not completely contained by each other. Only circle 2 is returned.

- **Are within**: Tests whether a geometry is within another. Returns 1 (true) if geometry a is completely inside geometry b. Only circle 1 is returned.

- **Cross**: Returns 1 (true) if the supplied geometries have some, but not all, interior points in common and the actual crossing is of a lower dimension than the highest supplied geometry. For example, a line crossing a polygon will cross as a line (true). Two lines crossing will cross as a point (true). Two polygons cross as a polygon (false). In the picture, no circles will be returned.

[^1]: https://saylordotorg.github.io/text_essentials-of-geographic-information-systems/s11-02-multiple-layer-analysis.html
[^2]: https://docs.qgis.org/3.28/en/docs/user_manual/processing_algs/algs_include.html
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJNMFhjUWUwT0thTTR3UjM1Ijp7In
N0YXJ0Ijo5NzAsImVuZCI6MjA4NCwidGV4dCI6IjEuICBEZWZp
bmUgdGhlIGlucHV0IGZlYXR1cmU6IElkZW50aWZ5IHRoZSBnZW
9ncmFwaGljIG9iamVjdCBmb3Igd2hpY2ggeW91IHdhbnTigKYi
fSwib3lrR3UwZkFzZ0NPM0RvYyI6eyJzdGFydCI6MTE5LCJlbm
QiOjkwNiwidGV4dCI6IkdJUyBidWZmZXIgYW5hbHlzaXMgaXMg
YSBzcGF0aWFsIGFuYWx5c2lzIHRlY2huaXF1ZSB1c2VkIHRvIG
NyZWF0ZSBwcm94aW1pdHkgem/igKYifSwiR1RIdWI2a3N2MTF1
akF0OSI6eyJzdGFydCI6MjgyNSwiZW5kIjozNjkzLCJ0ZXh0Ij
oiMS4gIFNlbGVjdCBpbnB1dCBkYXRhc2V0czogSWRlbnRpZnkg
dGhlIGxheWVycyBvciBtYXBzIHRoYXQgeW91IHdhbnQgdG8gb3
ZlcmxheeKApiJ9fSwiY29tbWVudHMiOnsiRTFGeUxHNzBTTEp0
M0VzaiI6eyJkaXNjdXNzaW9uSWQiOiJNMFhjUWUwT0thTTR3Uj
M1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRGlhZ3Jh
bSIsImNyZWF0ZWQiOjE2ODcxNTkxNDEwNjZ9LCJHb3BjQXQySj
lBUGlWdVR5Ijp7ImRpc2N1c3Npb25JZCI6Im95a0d1MGZBc2dD
TzNEb2MiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJFeG
FtcGxlIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTU5MTUzNzYy
fSwiQ21QTmtlMDZOeVFmRXRmSSI6eyJkaXNjdXNzaW9uSWQiOi
JHVEh1YjZrc3YxMXVqQXQ5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiRGlhZ3JhbSIsImNyZWF0ZWQiOjE2ODcxNTk0OD
UwMDJ9fSwiaGlzdG9yeSI6WzE1ODAzNjI1MTAsMTYzNjU5Mjcx
NywxNjI5Nzk1NDkzLDEyMjc2MzA3NzQsNzMwOTk4MTE2XX0=
-->