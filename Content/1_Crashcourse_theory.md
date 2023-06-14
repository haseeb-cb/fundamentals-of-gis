### Fundamentals of Geographic Information Systems (GIS)

# Introduction to Geographic Information System (GIS) and QGIS

## What is GIS and why do we use it?

GIS, which stands for Geographic Information System, is a technology that involves **capturing, storing, analyzing, and presenting geographically referenced data**. It integrates various types of information, such as maps, satellite imagery, and tabular data, into a digital framework that allows users to **view, understand, and analyze spatial patterns and relationships**.

GIS is used in a wide range of fields and industries, including:

1.  **Urban Planning**: GIS helps in analyzing land use patterns, transportation networks, and infrastructure planning. It enables urban planners to make informed decisions about zoning, growth management, and resource allocation.
2.  **Environmental Management**: GIS assists in monitoring and managing natural resources, such as forests, water bodies, and wildlife habitats. It aids in environmental impact assessments, conservation planning, and disaster management.
3.  **Public Health**: GIS is used to analyze disease outbreaks, track the spread of infectious diseases, and plan healthcare facilities and resources. It helps in understanding health disparities, identifying high-risk areas, and optimizing public health interventions.
4.  **Emergency Management**: GIS plays a crucial role in disaster preparedness, response, and recovery. It helps in identifying vulnerable areas, managing evacuation routes, and coordinating emergency services during natural disasters or other crises.
5.  **Transportation and Logistics**: GIS is utilized in optimizing transportation routes, analyzing traffic patterns, and planning efficient logistics networks. It assists in fleet management, supply chain optimization, and location-based services.
6.  **Natural Resource Management**: GIS is employed in assessing and managing natural resources like forests, water resources, minerals, and energy sources. It aids in land use planning, resource exploration, and environmental impact assessment.
7.  **Business and Marketing**: GIS helps businesses in market analysis, site selection, and customer profiling. It assists in identifying target markets, optimizing sales territories, and visualizing market trends.

These are just a few examples of the diverse applications of GIS. This course is not specifically tailored for a specific field, but it aims to give you a fundamental skillset in GIS that you can use to apply GIS in almost any field. 

### GIS workflow

PPDAC is a problem-solving framework commonly used in the field of data analysis and decision-making. It stands for Problem, Plan, Data, Analysis, and Conclusion. This framework provides a systematic approach to tackle complex problems and make informed decisions based on data-driven analysis. While PPDAC is not specifically tied to Geographic Information Systems (GIS), it can be applied within a GIS context to enhance the problem-solving process.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/GIS_PPDAC_v2.drawio.png)
By following the PPDAC framework, you can ensure a structured and systematic approach to problem-solving within the GIS domain. It helps in organizing your thoughts, guiding your analysis, and ensuring that your conclusions are based on robust data analysis.

For more information about the PPDAC Model: http://wiki.gis.com/wiki/index.php/PPDAC_Model

### Spatial data
Spatial data refers to **information that is associated with specific locations or geographic extents**. Vector and raster data are the two fundamental types of spatial data used in Geographic Information Systems (GIS) to represent and analyze spatial information.

![enter image description here](https://cdn.mindspritesolutions.com/onestopgis/GIS-Theory-and-Techniques/Raster-Data-Analysis/Comparison-of-Vector-and-Raster-based-Data-Analysis/posts/Comparison-of-Vector-and-Raster-Based-Data-Analysis/Figure-shows-comparison-of-Vector-and-Raster.webp)

1. **Vector data** provides a way to represent real world features within the GIS environment. A feature is anything you can see on the landscape. Imagine you are standing on the top of a hill. Looking down you can see houses, roads, trees, rivers, and so on. Each one of these things would be a **feature** when we represent them in a GIS Application. Vector features have **attributes**, which consist of text or numerical information that **describe** the features[^1].  Types of vector data include:
	-  Points: Represent specific locations in space, such as the coordinates of a city or a landmark.
	-  Lines: Represent linear features, such as roads, rivers, or boundaries. Lines are defined by a series of connected points.
	-  Polygons: Represent enclosed areas or regions, such as administrative boundaries, land parcels, or thematic zones. Polygons are defined by a series of connected lines forming a closed shape.

	Vector data provides precise and accurate representations of spatial features. 

- Real life example of vector data 

2. **Raster Data** represents spatial information by a continuous surface divided into a grid of cells or pixels. Each cell corresponds to a specific location and contains a value representing a particular attribute. Key characteristics of raster data include:
	-  Grid: The analyzed surface is divided into a regular grid of cells, where each cell represents a specific location or area.
	-  Resolution: Raster data has a spatial resolution that defines the size or extent of each cell. Higher resolution means smaller cell sizes, resulting in more detailed data representation.
	-  Attribute Value: Each cell contains a value that represents a specific attribute, such as elevation, temperature, land cover type, or satellite reflectance.
	
	Raster data is commonly used for continuous and regularly sampled data, such as satellite imagery, digital elevation models (DEMs), or climate data. It is suitable for analyzing continuous phenomena, interpolating values, and performing terrain analysis. Raster data is less suitable for representing discrete features or sharp boundaries.

- Real life example of vector data 

In GIS, both vector and raster data have their respective strengths and applications. Vector data is well-suited for representing discrete features and precise geometries, while raster data is ideal for representing continuous surfaces and performing spatial analysis based on cell values. GIS software allows for the integration, analysis, and visualization of both types of data, enabling users to explore and understand spatial information from different perspectives.

(Hungry for more? Further reading on vector and raster data in the QGIS documentation: https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/vector_data.html, https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/raster_data.html)

#### Spatial data sources
How and where to find spatial data is discussed in detail here: 

### Coordinate Reference Systems (CRS) and map projections
The basic idea of projection is to project the shape of the earth, or a specific area, onto a flat plane like a map. Due to the original shape of the earth, a rough sphere, we will always get some kind of distortion when we project it onto a flat plane. This is shown well here: https://unchartedterritories.tomaspueyo.com/p/maps-distort-how-we-see-the-world 

![enter image description here](https://upload.wikimedia.org/wikipedia/commons/e/ee/Worlds_animate.gif)

Coordinate Reference Systems (CRS) are frameworks that define how geographic locations are represented and referenced in a coordinate system. There are different CRS which use different Earth shape models and projection methods. The specific CRS used is often depending on the region where the data is located. When we are working with different kind of data, it is common that we have layers that are in different CRS. **Thus, it is important to check that the layers and the project are in the same CRS!** Most GIS data that we get comes with some CRS, if we decide to do something in some other projection, you can do reproject data into a different CRS. We will go into this 

![Map Projection Families](https://docs.qgis.org/3.4/en/_images/projection_families.png)

Some common CRS include:
- Finland: ETRS-TM35FIN (EPSG:3067) (Shown in the picture below)
- GPS: WGS 84 (EPSG:4326)

![ETRS=TM35FIN](https://upload.wikimedia.org/wikipedia/fi/1/15/ETRSTM35FIN.png)

(Hungry for more? Coordinate Reference Systems are described in more detail in the QGIS documentation: https://docs.qgis.org/3.4/en/docs/gentle_gis_introduction/coordinate_reference_systems.html

You can also search for Youtube videos on this topic:
- CRS in QGIS: https://www.youtube.com/watch?v=EKKXXAahu3w
- Why all world maps are wrong: https://www.youtube.com/watch?v=kIID5FDi2JQ
- How do Map Projections worl? https://www.youtube.com/watch?v=NAzy4S4EOwc )
 


### GIS analysis types
The most common GIS (Geographic Information System) analysis types can vary depending on the specific application and industry. However, some of the widely used and common GIS analysis types are:

1.  **Spatial Query and Selection**: This analysis involves selecting or querying spatial features based on their spatial relationship with other features. It helps answer questions like "Which points are within a certain distance of a line?" or "Which polygons intersect a specific area?"
2.  **Spatial Overlay and Intersection**: Overlay analysis combines multiple spatial datasets to create new datasets by intersecting, unioning, or differencing features. It helps identify areas of overlap, calculate areas, and analyze spatial relationships between different layers.
3.  **Buffer Analysis**: Buffer analysis creates a proximity zone around a specific feature or set of features. It helps assess the impact or accessibility of certain locations, such as finding all points within a certain distance of a river or road.
4.  **Network Analysis**: Network analysis focuses on analyzing and modeling networks, such as road networks or utility networks. It includes tasks like route optimization, shortest path analysis, service area analysis, and network connectivity analysis.
5.  **Spatial Interpolation**: Interpolation methods estimate attribute values at unsampled locations based on values observed at nearby sampled locations. It helps create continuous surfaces from point data, such as generating elevation models or estimating pollution levels.
6.  **Hotspot Analysis**: Hotspot analysis identifies statistically significant clusters or concentrations of spatial features. It helps identify areas of high or low values, such as identifying crime hotspots or disease clusters.
7.  **Density Analysis**: Density analysis calculates the density of spatial features within a specific area. It helps identify areas of high or low density, such as population density or density of specific events.
8.  **Geocoding and Geolocation**: Geocoding involves converting addresses or place names into spatial coordinates, while geolocation refers to determining the location of an entity based on its geographic features. These techniques are used for mapping, spatial referencing, and analysis.
9.  **Spatial Regression**: Spatial regression methods explore relationships between spatially referenced variables, considering spatial autocorrelation and spatial dependency. It helps understand how variables interact across space and can be used for predictive modeling or identifying spatial patterns in relationships.
10.  **Thematic Mapping and Cartography**: GIS analysis includes creating visually appealing and informative maps, charts, and graphs to visualize spatial patterns and analysis results effectively.

These are some of the most common GIS analysis types, but the field of GIS offers a vast range of analysis techniques and tools that can be tailored to specific needs and applications. 


## What is QGIS?
In short, QGIS is a GIS application that can be used for various GIS analyses. There are other GIS applications, the other most common of which is ArcGIS. We are using QGIS for this course since it is open-source and free, meaning it is accesible for all, in contrast to ArcGIS which is proprietary software. 

So, you're going to need QGIS for this course! Please take a moment now to ensure you have it installed: https://qgis.org/en/site/forusers/download.html#

You can find more information about the usage of QGIS here: https://docs.qgis.org/3.28/en/docs/index.html

## What is a good map?

A **good map** has: 
1. Clear and objective symbology that represents the data correctly
2. Is useful for the target audience
3. An adequate projection and scale(bar)
4. A north arrow
5. A legend with explanations of used symbology/colours etc.
6. Usually data sources and the used projection

Important to keep in mind is that: **maps are images that inherently selective and result from choices made by a cartographer**. There is no such thing as an "objective map". In reality, maps always emphasize some elements while ignoring others (or pushing them to the "background") and there's power involved. The fact that maps are images also means that a map is often accompanied by a caption that tells the reader what they are expected to see on the map. Making good captions is a skill in itself, as captions influence influence the way in which people interpret the maps (as well as the reality they are attempting to depict).  

Another important thing to keep in mind is to **make your maps accessible to all readers, including those who have some form of color blindness**. This is relatively simple, since QGIS already has a tool build-in to simulate a few color blind examples:

![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/1_CrashCourse_Theory/1_CrashCourse_theory_QGIS_color_blindness.png)

You can get color advice for your maps here: https://colorbrewer2.org/ 


# Time to get your hands dirty! Move on to the Crash Course exercise to get started with (Q)GIS  

[^1]: https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/vector_data.html
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJtWGprNzZRa291cmFwcVJuIjp7In
RleHQiOiItIFJlYWwgbGlmZSBleGFtcGxlIG9mIHZlY3RvciBk
YXRhIiwic3RhcnQiOjE0MDgsImVuZCI6MTQ0Mn0sIk9CUjhLdX
YxNHZDckFRTDQiOnsidGV4dCI6Ii0gUmVhbCBsaWZlIGV4YW1w
bGUgb2YgdmVjdG9yIGRhdGEiLCJzdGFydCI6MjUzMCwiZW5kIj
oyNTY0fSwiYnlNdnhqbzBmSXlyWTROSiI6eyJ0ZXh0IjoiIyMj
IEdJUyBhbmFseXNpcyB0eXBlcyIsInN0YXJ0Ijo1MzMzLCJlbm
QiOjUzNTV9LCJ6VDRWNUFGVjlnYVJTeENOIjp7InRleHQiOiJn
b29kIG1hcCIsInN0YXJ0Ijo5NzU2LCJlbmQiOjk3NjR9LCI4Sz
dTRlRUdTExVDlDQTlUIjp7InRleHQiOiIjIFRpbWUgdG8gZ2V0
IHlvdXIgaGFuZHMgZGlydHkhIE1vdmUgb24gdG8gdGhlIENyYX
NoIENvdXJzZSBleGVyY2lzZSB0byBnZXQgc3Rh4oCmIiwic3Rh
cnQiOjExMTg5LCJlbmQiOjExMjg0fSwiN2Ezak9RWElCbDM4U2
ZaYiI6eyJ0ZXh0Ijoic2F0ZWxsaXRlIiwic3RhcnQiOjM4Mywi
ZW5kIjozOTJ9LCJscWtuVGlzNEc2RGJpcWRYIjp7InRleHQiOi
Jwb2ludHMiLCJzdGFydCI6MTEyMSwiZW5kIjoxMTI3fSwibEVF
cVo4Qk4yTW1ZSWpJaCI6eyJ0ZXh0IjoibGluZXMiLCJzdGFydC
I6MTI5NCwiZW5kIjoxMjk5fSwiSm5CaTc2TnlrNEl4ako5SyI6
eyJ0ZXh0Ijoid29ybCIsInN0YXJ0Ijo4OTI1LCJlbmQiOjg5Mj
l9fSwiY29tbWVudHMiOnsiYk5PaVNVYTFocjFZQVpKYiI6eyJk
aXNjdXNzaW9uSWQiOiJtWGprNzZRa291cmFwcVJuIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJj
cmVhdGVkIjoxNjg2MTI3MDMyMDc4fSwiOTdNUldHTmFPUk03bE
xsUCI6eyJkaXNjdXNzaW9uSWQiOiJPQlI4S3V2MTR2Q3JBUUw0
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3
R1cmUiLCJjcmVhdGVkIjoxNjg2MTI3MDQ4OTY3fSwiUU5SdFJS
ckswTU9YeFdPQiI6eyJkaXNjdXNzaW9uSWQiOiJieU12eGpvMG
ZJeXJZNE5KIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
SW5jbHVkZSBleGFtcGxlIHBpY3R1cmVzIiwiY3JlYXRlZCI6MT
Y4NjEzNzg4NzE3MX0sInN0RmJhb1VZcHZSc1hrYW0iOnsiZGlz
Y3Vzc2lvbklkIjoielQ0VjVBRlY5Z2FSU3hDTiIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBleGFtcGxlIHdpdGgg
cG9pbnRlcnMiLCJjcmVhdGVkIjoxNjg2MTM4NDIyNTc4fSwiS0
xuOEZSdENjcWhWaU5QRyI6eyJkaXNjdXNzaW9uSWQiOiI4SzdT
RlRUdTExVDlDQTlUIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQWRkIGxpbmsgdG8gZXhlcmNpc2UiLCJjcmVhdGVkIjox
Njg2MTM4NTQ5MTM5fSwiN2VrRHh1bGE4WlJnM3pjQiI6eyJkaX
NjdXNzaW9uSWQiOiJieU12eGpvMGZJeXJZNE5KIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW5kIGxpbmtzIiwiY3JlYX
RlZCI6MTY4NjQ4MzEyOTQ1M30sIkdwMU5UN2Qwem95aWNselUi
OnsiZGlzY3Vzc2lvbklkIjoielQ0VjVBRlY5Z2FSU3hDTiIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IisgYmFkIGV4YW1w
bGUgYXMgd2VsbCIsImNyZWF0ZWQiOjE2ODY3MjE5NjQxMTd9LC
JGSGFwSms5c3Q5Y0t0MFVvIjp7ImRpc2N1c3Npb25JZCI6Ijdh
M2pPUVhJQmwzOFNmWmIiLCJzdWIiOiJnaDoyMjE2ODE1NyIsIn
RleHQiOiJhZXJpYWwgb3Igc2F0ZWxsaXRlPyIsImNyZWF0ZWQi
OjE2ODY3MjQ0Njg0NzJ9LCJPRHhhN012dURDNnVWOW1GIjp7Im
Rpc2N1c3Npb25JZCI6Imxxa25UaXM0RzZEYmlxZFgiLCJzdWIi
OiJnaDoyMjE2ODE1NyIsInRleHQiOiJub2Rlcz8iLCJjcmVhdG
VkIjoxNjg2NzI0NTMxNzEyfSwiSFBQUHdneDhJemFqT0NxcSI6
eyJkaXNjdXNzaW9uSWQiOiJsRUVxWjhCTjJNbVlJakloIiwic3
ViIjoiZ2g6MjIxNjgxNTciLCJ0ZXh0IjoiYWxzbyBub2Rlcz8i
LCJjcmVhdGVkIjoxNjg2NzI0NTU4NjM0fSwiU3V2NlBCYnJUdm
JSb0U3VyI6eyJkaXNjdXNzaW9uSWQiOiJKbkJpNzZOeWs0SXhq
SjlLIiwic3ViIjoiZ2g6MjIxNjgxNTciLCJ0ZXh0Ijoid29yaz
8iLCJjcmVhdGVkIjoxNjg2NzI0NzI5MjQyfX0sImhpc3Rvcnki
OlstMTg2ODI0OTI0NF19
-->