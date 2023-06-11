### Fundamentals of Geographic Information Systems (GIS)

# Introduction to Geographic Information System (GIS) and QGIS

## Course introduction

### Learning outcomes
After completing the course you should be able to:
- Understand the fundamental principles of GIS, including rasters, vector, projections, geoprocessing and analysis
- Apply basic GIS skills to:
	- Map Design
	- Gathering GIS data from various sources
	- Use different types of spatial data
	- Analyse GIS data to address geosptial problems and/or research questions 
- Develop the aiblity to perform new anayses, troubleshoot, and find help from the GIS community to solve your problems

### Structure
The course consists of **9 exercises**, each accompanied by a piece of theory. The first exercise, which goes with this theory, is meant to give you the basic skills in GIS and the software we will be using, QGIS. From there on you will build on these basic skills using the other exercises, covering vairous analyses and methods, and develop a fundamental skillset in GIS and QGIS. 

| Exercise | Topic | Methods |
|--|--|--|
| Crash Course | Introduction | QGIS interface & Vector analysis |
| 1 | Vector analysis introduction | Digitizing, georeferencing, clipping |
| 2 | Socio-spatial differentiation | Raster analysis |
| 3 | Finding the optimal location for a new development | Buffer analysis, overlay analysis |
| 4 | Determining optimal land for cultivation | Digital Elevation Model (DEM), slope, hillshade, overlay analysis |
| 5 | Understnading disease transmission | Heatmap analysis (Kernel Density), Voronoi diagram, text processing |
| 6 | Air quality analysis | Spatial interpolation
| 7 | Calculating building efficiency | Expressions, creating grids |
| 8 | Wind power NIMBY (Not in my backyard) analysis | Public Participation GIS/SoftGIS, Directional Distribution |

### Evalution
To get the credits for this course, the following criteria have to be met:
 - [ ] Submitted original map output(s) for each exercise
	 - With your name on the output
 - [ ] Submitted original map reflection for each exercise
 - [ ] Completed the X Moodle exams  

To ensure that your submissions are original:
- Map output: Your name has to be mentioned on the map output and they are be compared with others
- Map reflection: Anti-plagiarism tool is used

### Troubleshooting
If you ever have a question or run in to an issue along this course, please follow the following troubleshooting process: 

![Troubleshooting process](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/GIS_troubleshooting_process.drawio.png)
1. Start by checking if the information in the **course materials** provide a solution, it might have been covered in the previous theory or exercises as well
	- If you come across missing information in the materials, please let us know so we can make sure others don't run into the same issue! 
2. Being a *Professional **Google** Searcher* will get you really far with (Q)GIS. Try searching your question or issue, below you can find some tips on how to improve your google searches
	- [Simple Google Search tips](https://www.youtube.com/watch?v=oIMTM168BK8)
	- [How to "Google It" like a Senior Software Engineer](https://www.youtube.com/watch?v=cEBkvm0-rg0)
	- [Refine web searches](https://support.google.com/websearch/answer/2466433?hl=en)
3. Ask your question in the **chat**, other students or professionals will be able to help you! Use the channel of the exercise you are working on. 
	- Chat link: 
5.  If at this point you still have not found a resolution, mention the **teachers** in the channel (@)



Following this process will help you **develop the independent troubleshooting skills** you will need when you use GIS on your own. 

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
We can apply the **PPDAC workflow** to GIS analysis:

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/GIS_PPDAC_v2.drawio.png)

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
The basic idea of a CRS is to project the shape of the earth, or the specific area of the CRS, onto a flat plane like a map. In other words, CRS are frameworks that define how geographic clocations are represented and referenced in a coordinate system. There are different CRS which use different Earth shape models as a reference and projection methods, the specific CRS used is often depending on the region where the data is located. When we are working with different kind of data, it is common that we have layers that are in different CRS. **Thus, it is important to check that the layers and the project are in the same CRS!**

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
3. An adequate projection and scale
4. A north arrow
5. A legend with explanations of used symbology/colours etc.
6. Usually data sources and the used projection

# Time to get your hands dirty! Move on to the Crash Course exercise to get started with (Q)GIS  

[^1]: https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/vector_data.html
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJBekJ0bTlpSG5HS2pVUGVGIjp7In
N0YXJ0IjoyMTIwLCJlbmQiOjIxMjEsInRleHQiOiJYIn0sIno2
SmxoRFBWRnpxb3U4MnUiOnsic3RhcnQiOjM1MTcsImVuZCI6Mz
UyNywidGV4dCI6IkNoYXQgbGluazoifSwiZTRrb1dqOU1SZXJy
VWdFdiI6eyJzdGFydCI6MzYyOSwiZW5kIjozNjMyLCJ0ZXh0Ij
oiKEApIn0sIm1Yams3NlFrb3VyYXBxUm4iOnsic3RhcnQiOjgw
NDUsImVuZCI6ODA3OSwidGV4dCI6Ii0gUmVhbCBsaWZlIGV4YW
1wbGUgb2YgdmVjdG9yIGRhdGEifSwiT0JSOEt1djE0dkNyQVFM
NCI6eyJzdGFydCI6OTE2NywiZW5kIjo5MjAxLCJ0ZXh0IjoiLS
BSZWFsIGxpZmUgZXhhbXBsZSBvZiB2ZWN0b3IgZGF0YSJ9LCI1
c082Y3c0dGFSa3kwSXY3Ijp7InN0YXJ0Ijo5OTQ1LCJlbmQiOj
EwMDA4LCJ0ZXh0IjoiSG93IGFuZCB3aGVyZSB0byBmaW5kIHNw
YXRpYWwgZGF0YSBpcyBkaXNjdXNzZWQgaW4gZGV0YWlsIGhlcm
U6In0sImJ5TXZ4am8wZkl5clk0TkoiOnsic3RhcnQiOjExMTg5
LCJlbmQiOjExMjExLCJ0ZXh0IjoiIyMjIEdJUyBhbmFseXNpcy
B0eXBlcyJ9LCJ6VDRWNUFGVjlnYVJTeENOIjp7InN0YXJ0Ijox
NDgyOSwiZW5kIjoxNDgzNywidGV4dCI6Imdvb2QgbWFwIn0sIj
hLN1NGVFR1MTFUOUNBOVQiOnsic3RhcnQiOjE1MTE0LCJlbmQi
OjE1MjA5LCJ0ZXh0IjoiIyBUaW1lIHRvIGdldCB5b3VyIGhhbm
RzIGRpcnR5ISBNb3ZlIG9uIHRvIHRoZSBDcmFzaCBDb3Vyc2Ug
ZXhlcmNpc2UgdG8gZ2V0IHN0YeKApiJ9fSwiY29tbWVudHMiOn
sicVpXWEZndGVMZGZ2VXNkMiI6eyJkaXNjdXNzaW9uSWQiOiJB
ekJ0bTlpSG5HS2pVUGVGIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQWRkIG51bWJlciIsImNyZWF0ZWQiOjE2ODYxMjA1
NTAyODF9LCIxT2NBeDQxSWh0dHZrTWhTIjp7ImRpc2N1c3Npb2
5JZCI6Ino2SmxoRFBWRnpxb3U4MnUiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJBZGQgbGluayIsImNyZWF0ZWQiOjE2OD
YxMjM1NTczNTB9LCJMcFQzUkN0c29URFpoUXhoIjp7ImRpc2N1
c3Npb25JZCI6ImU0a29XajlNUmVyclVnRXYiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgbmFtZXMiLCJjcmVhdGVk
IjoxNjg2MTIzNjExMDA3fSwiYk5PaVNVYTFocjFZQVpKYiI6ey
JkaXNjdXNzaW9uSWQiOiJtWGprNzZRa291cmFwcVJuIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLC
JjcmVhdGVkIjoxNjg2MTI3MDMyMDc4fSwiOTdNUldHTmFPUk03
bExsUCI6eyJkaXNjdXNzaW9uSWQiOiJPQlI4S3V2MTR2Q3JBUU
w0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBp
Y3R1cmUiLCJjcmVhdGVkIjoxNjg2MTI3MDQ4OTY3fSwiYmVqTV
A1VWpNRDBDMGIzRCI6eyJkaXNjdXNzaW9uSWQiOiI1c082Y3c0
dGFSa3kwSXY3Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiTGluayB0byBhcnRpY2xlIiwiY3JlYXRlZCI6MTY4NjEzNjcx
Nzg1MX0sIlFOUnRSUnJLME1PWHhXT0IiOnsiZGlzY3Vzc2lvbk
lkIjoiYnlNdnhqbzBmSXlyWTROSiIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkluY2x1ZGUgZXhhbXBsZSBwaWN0dXJlcy
IsImNyZWF0ZWQiOjE2ODYxMzc4ODcxNzF9LCJzdEZiYW9VWXB2
UnNYa2FtIjp7ImRpc2N1c3Npb25JZCI6InpUNFY1QUZWOWdhUl
N4Q04iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
ZXhhbXBsZSB3aXRoIHBvaW50ZXJzIiwiY3JlYXRlZCI6MTY4Nj
EzODQyMjU3OH0sIktMbjhGUnRDY3FoVmlOUEciOnsiZGlzY3Vz
c2lvbklkIjoiOEs3U0ZUVHUxMVQ5Q0E5VCIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBsaW5rIHRvIGV4ZXJjaXNl
IiwiY3JlYXRlZCI6MTY4NjEzODU0OTEzOX19LCJoaXN0b3J5Ij
pbLTM4NDY3MjQxNCwtNTExNzYwMjM1LC0yMDEwNTczMDI1LC0x
Mzc0NTQwMTEsLTI1NjAwNzI5NywxMzQzNTM3NTc3LC0xMDM1Nz
E4ODI1LDYwNzY3OTgsMTY3ODg0NzE4MCwxMDE0NjY3MDg5LDIw
NjYyOTc3OTksLTEzNjgyOTMxMTMsLTE5Nzc3NDY0MzUsOTAwOD
kxODE2XX0=
-->