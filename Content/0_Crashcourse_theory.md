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

	Vector data provides precise and accurate representations of spatial features . 

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
The basic idea of projection is to project the shape of the earth, or the specific area of the CRS, onto a flat plane like a map. In other words, CRS are frameworks that define how geographic locations are represented and referenced in a coordinate system. There are different CRS which use different Earth shape models as a reference and projection methods. The specific CRS used is often depending on the region where the data is located. When we are working with different kind of data, it is common that we have layers that are in different CRS. **Thus, it is important to check that the layers and the project are in the same CRS!**

The basic idea of a CRS is to project the shape of the earth, or the specific area of the CRS, onto a flat plane like a map. In other words, CRS are frameworks that define how geographic locations are represented and referenced in a coordinate system. There are different CRS which use different Earth shape models as a reference and projection methods. The specific CRS used is often depending on the region where the data is located. When we are working with different kind of data, it is common that we have layers that are in different CRS. **Thus, it is important to check that the layers and the project are in the same CRS!**

![Map Projection Families](https://docs.qgis.org/3.4/en/_images/projection_families.png)

Some common CRS include:
- Finland: ETRS-TM35FIN (EPSG:3067) (Shown in the picture below)
- GPS: WGS 84 (EPSG:4326)

![ETRS=TM35FIN](https://upload.wikimedia.org/wikipedia/fi/1/15/ETRSTM35FIN.png)
(Hungry for more? Coordinate Reference Systems are described in more detail in the QGIS documentation: https://docs.qgis.org/3.4/en/docs/gentle_gis_introduction/coordinate_reference_systems.html)

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
In short, QGIS is a GIS application that can be used for various GIS analyses. There are other GIS application, the other most common of which is ArcGIS. We are using QGIS for this course since it is open-source and free, meaning it is accesible for all, in contrast to ArcGIS which is proprietary software. 

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

# Time to get your hands dirty! Move on to the Crash Course exercise to get started with (Q)GIS  

[^1]: https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/vector_data.html
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJtWGprNzZRa291cmFwcVJuIjp7In
N0YXJ0Ijo1MDU2LCJlbmQiOjUwOTAsInRleHQiOiItIFJlYWwg
bGlmZSBleGFtcGxlIG9mIHZlY3RvciBkYXRhIn0sIk9CUjhLdX
YxNHZDckFRTDQiOnsic3RhcnQiOjYxNzgsImVuZCI6NjIxMiwi
dGV4dCI6Ii0gUmVhbCBsaWZlIGV4YW1wbGUgb2YgdmVjdG9yIG
RhdGEifSwiNXNPNmN3NHRhUmt5MEl2NyI6eyJzdGFydCI6Njk1
NiwiZW5kIjo3MDE5LCJ0ZXh0IjoiSG93IGFuZCB3aGVyZSB0by
BmaW5kIHNwYXRpYWwgZGF0YSBpcyBkaXNjdXNzZWQgaW4gZGV0
YWlsIGhlcmU6In0sImJ5TXZ4am8wZkl5clk0TkoiOnsic3Rhcn
QiOjg4MzgsImVuZCI6ODg2MCwidGV4dCI6IiMjIyBHSVMgYW5h
bHlzaXMgdHlwZXMifSwielQ0VjVBRlY5Z2FSU3hDTiI6eyJzdG
FydCI6MTI0NzgsImVuZCI6MTI0ODYsInRleHQiOiJnb29kIG1h
cCJ9LCI4SzdTRlRUdTExVDlDQTlUIjp7InN0YXJ0IjoxMzQwNi
wiZW5kIjoxMzUwMSwidGV4dCI6IiMgVGltZSB0byBnZXQgeW91
ciBoYW5kcyBkaXJ0eSEgTW92ZSBvbiB0byB0aGUgQ3Jhc2ggQ2
91cnNlIGV4ZXJjaXNlIHRvIGdldCBzdGHigKYifSwiazNMbExM
bUlWTG9jUmduQSI6eyJzdGFydCI6MTI0NTAsImVuZCI6MTI0Nz
IsInRleHQiOiIjIyBXaGF0IGlzIGEgZ29vZCBtYXA/In0sIjht
VDd3dXQyZzlaMzQxQUwiOnsic3RhcnQiOjcwMjIsImVuZCI6Nz
A4MCwidGV4dCI6IiMjIyBDb29yZGluYXRlIFJlZmVyZW5jZSBT
eXN0ZW1zIChDUlMpIGFuZCBtYXAgcHJvamVjdGlvbnMifSwiQ1
FBV29TeWtobXo3eGszTiI6eyJzdGFydCI6ODI2NSwiZW5kIjo4
MzUyLCJ0ZXh0IjoiKipUaHVzLCBpdCBpcyBpbXBvcnRhbnQgdG
8gY2hlY2sgdGhhdCB0aGUgbGF5ZXJzIGFuZCB0aGUgcHJvamVj
dCBhcmUgaW4gdGhlIHNhbeKApiJ9fSwiY29tbWVudHMiOnsiYk
5PaVNVYTFocjFZQVpKYiI6eyJkaXNjdXNzaW9uSWQiOiJtWGpr
NzZRa291cmFwcVJuIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2MTI3MDMy
MDc4fSwiOTdNUldHTmFPUk03bExsUCI6eyJkaXNjdXNzaW9uSW
QiOiJPQlI4S3V2MTR2Q3JBUUw0Iiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNj
g2MTI3MDQ4OTY3fSwiYmVqTVA1VWpNRDBDMGIzRCI6eyJkaXNj
dXNzaW9uSWQiOiI1c082Y3c0dGFSa3kwSXY3Iiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiTGluayB0byBhcnRpY2xlIiwi
Y3JlYXRlZCI6MTY4NjEzNjcxNzg1MX0sIlFOUnRSUnJLME1PWH
hXT0IiOnsiZGlzY3Vzc2lvbklkIjoiYnlNdnhqbzBmSXlyWTRO
SiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkluY2x1ZG
UgZXhhbXBsZSBwaWN0dXJlcyIsImNyZWF0ZWQiOjE2ODYxMzc4
ODcxNzF9LCJzdEZiYW9VWXB2UnNYa2FtIjp7ImRpc2N1c3Npb2
5JZCI6InpUNFY1QUZWOWdhUlN4Q04iLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJBZGQgZXhhbXBsZSB3aXRoIHBvaW50ZX
JzIiwiY3JlYXRlZCI6MTY4NjEzODQyMjU3OH0sIktMbjhGUnRD
Y3FoVmlOUEciOnsiZGlzY3Vzc2lvbklkIjoiOEs3U0ZUVHUxMV
Q5Q0E5VCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFk
ZCBsaW5rIHRvIGV4ZXJjaXNlIiwiY3JlYXRlZCI6MTY4NjEzOD
U0OTEzOX0sIjdla0R4dWxhOFpSZzN6Y0IiOnsiZGlzY3Vzc2lv
bklkIjoiYnlNdnhqbzBmSXlyWTROSiIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkFuZCBsaW5rcyIsImNyZWF0ZWQiOjE2
ODY0ODMxMjk0NTN9LCJLVjdZQjI0NHZSQXZmeTg2Ijp7ImRpc2
N1c3Npb25JZCI6ImszTGxMTG1JVkxvY1JnbkEiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJDb2xvciBicmV3ZXIsIG1ha2
UgYSBiYWQgbWFwLCBtYWtlIGEgZ29vZCBtYXAiLCJjcmVhdGVk
IjoxNjg2NjU5NDY4NDUwfSwiQmJCemZSZWZnUDB2ajgyQiI6ey
JkaXNjdXNzaW9uSWQiOiI4bVQ3d3V0Mmc5WjM0MUFMIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiWW91dHViZSB2aWRlby
IsImNyZWF0ZWQiOjE2ODY2NTk2Njc2ODl9LCJhT240elpiSUJM
bWxQeG1vIjp7ImRpc2N1c3Npb25JZCI6IjhtVDd3dXQyZzlaMz
QxQUwiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJTZXBl
cmF0ZSBwcm9qZWN0aW9ucyIsImNyZWF0ZWQiOjE2ODY2NTk2OD
UwOTd9LCJkbXVqQlFDY0JqM0c3V25hIjp7ImRpc2N1c3Npb25J
ZCI6IjhtVDd3dXQyZzlaMzQxQUwiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJHSVMgZGF0YSB0aGF0IHlvdSBnZXQgY29t
ZXMgd2l0aCBzb21lIENSUywgaWYgeW91IGRlY2lkZSB0byBkby
Bzb21ldGhpbmcgaW4gc29tZSBvdGhlciBwcm9qZWN0aW9uLCB5
b3UgY2FuIGRvIHNvbWUgdHJhbnNmb3JtYXRpb24sIGl0IHJlcH
JvamVjdHMgdGhlIGNvb3JkaW5hdGVzIiwiY3JlYXRlZCI6MTY4
NjY1OTg1NjY5NH0sInJVTEdVRUxLejkzeVozUnQiOnsiZGlzY3
Vzc2lvbklkIjoiQ1FBV29TeWtobXo3eGszTiIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBhIHNlY3Rpb24gYWJvdX
QgcmVwcm9qZWN0aW9uIiwiY3JlYXRlZCI6MTY4NjY1OTkwOTYz
NX19LCJoaXN0b3J5IjpbNTU1Mjg3NTkyLC0xOTA3NDY2NTY4LD
E4MDQ5NzAxMjAsMTEwNzA4MzMxMSwxMzAyNjU5Nzg3LDQ2OTQ4
MDAxNywtNTExNzYwMjM1LC0yMDEwNTczMDI1LC0xMzc0NTQwMT
EsLTI1NjAwNzI5NywxMzQzNTM3NTc3LC0xMDM1NzE4ODI1LDYw
NzY3OTgsMTY3ODg0NzE4MCwxMDE0NjY3MDg5LDIwNjYyOTc3OT
ksLTEzNjgyOTMxMTMsLTE5Nzc3NDY0MzUsOTAwODkxODE2XX0=

-->