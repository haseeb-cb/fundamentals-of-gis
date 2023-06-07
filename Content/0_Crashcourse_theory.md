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
| 8 | Wind power NIMBY (Not in my backyard) analysis | Public Paticipation GIS/SoftGIS, Directional Distribution |

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
- Diagram 

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

### Coordinate systems and projection


---
- Definition
	- Geoinformatics vs GIS
	- Uses
- Spatial data
	- Definition
	- Types (vector vs raster)
	- Objects
	- Attributes
	- Sources
- Coordinate systems and projection
	- GCS
	- CRS
	- PCS
	- Earth shape
	- Map projection
- Spatial data analysis methods
	- Which exist 
	- Which are covered in this course
	- Examples (in research and society)
- GIS workflow

## What is QGIS?

- Data files
	- Vector and raster

## What is a good map?

[^1]: https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/vector_data.html
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJBekJ0bTlpSG5HS2pVUGVGIjp7In
N0YXJ0IjoyMTE5LCJlbmQiOjIxMjAsInRleHQiOiJYIn0sIno2
SmxoRFBWRnpxb3U4MnUiOnsic3RhcnQiOjM1MTYsImVuZCI6Mz
UyNiwidGV4dCI6IkNoYXQgbGluazoifSwiZTRrb1dqOU1SZXJy
VWdFdiI6eyJzdGFydCI6MzYyOCwiZW5kIjozNjMxLCJ0ZXh0Ij
oiKEApIn0sIkZhcFdOajhLeWJqOFR4SkkiOnsic3RhcnQiOjYy
MTMsImVuZCI6NjIyMCwidGV4dCI6IkRpYWdyYW0ifSwibVhqaz
c2UWtvdXJhcHFSbiI6eyJzdGFydCI6NzgwNCwiZW5kIjo3ODM4
LCJ0ZXh0IjoiLSBSZWFsIGxpZmUgZXhhbXBsZSBvZiB2ZWN0b3
IgZGF0YSJ9LCJPQlI4S3V2MTR2Q3JBUUw0Ijp7InN0YXJ0Ijo4
OTI2LCJlbmQiOjg5NjAsInRleHQiOiItIFJlYWwgbGlmZSBleG
FtcGxlIG9mIHZlY3RvciBkYXRhIn0sIjVzTzZjdzR0YVJreTBJ
djciOnsic3RhcnQiOjk3MDUsImVuZCI6OTc2OCwidGV4dCI6Ik
hvdyBhbmQgd2hlcmUgdG8gZmluZCBzcGF0aWFsIGRhdGEgaXMg
ZGlzY3Vzc2VkIGluIGRldGFpbCBoZXJlOiJ9fSwiY29tbWVudH
MiOnsicVpXWEZndGVMZGZ2VXNkMiI6eyJkaXNjdXNzaW9uSWQi
OiJBekJ0bTlpSG5HS2pVUGVGIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIG51bWJlciIsImNyZWF0ZWQiOjE2ODYx
MjA1NTAyODF9LCIxT2NBeDQxSWh0dHZrTWhTIjp7ImRpc2N1c3
Npb25JZCI6Ino2SmxoRFBWRnpxb3U4MnUiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgbGluayIsImNyZWF0ZWQiOj
E2ODYxMjM1NTczNTB9LCJMcFQzUkN0c29URFpoUXhoIjp7ImRp
c2N1c3Npb25JZCI6ImU0a29XajlNUmVyclVnRXYiLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgbmFtZXMiLCJjcmVh
dGVkIjoxNjg2MTIzNjExMDA3fSwibUJpZ0VyNmNHbFpIOGxCMS
I6eyJkaXNjdXNzaW9uSWQiOiJGYXBXTmo4S3liajhUeEpJIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGRpYWdyYW
0iLCJjcmVhdGVkIjoxNjg2MTI2MTkyMjE0fSwiYk5PaVNVYTFo
cjFZQVpKYiI6eyJkaXNjdXNzaW9uSWQiOiJtWGprNzZRa291cm
FwcVJuIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRk
IHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2MTI3MDMyMDc4fSwiOT
dNUldHTmFPUk03bExsUCI6eyJkaXNjdXNzaW9uSWQiOiJPQlI4
S3V2MTR2Q3JBUUw0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2MTI3MDQ4
OTY3fSwiYmVqTVA1VWpNRDBDMGIzRCI6eyJkaXNjdXNzaW9uSW
QiOiI1c082Y3c0dGFSa3kwSXY3Iiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiTGluayB0byBhcnRpY2xlIiwiY3JlYXRlZC
I6MTY4NjEzNjcxNzg1MX19LCJoaXN0b3J5IjpbLTg5ODUwODcz
MiwxMzQzNTM3NTc3LC0xMDM1NzE4ODI1LDYwNzY3OTgsMTY3OD
g0NzE4MCwxMDE0NjY3MDg5LDIwNjYyOTc3OTksLTEzNjgyOTMx
MTMsLTE5Nzc3NDY0MzUsOTAwODkxODE2XX0=
-->