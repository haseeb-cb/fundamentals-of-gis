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

### GIS 

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


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJBekJ0bTlpSG5HS2pVUGVGIjp7In
N0YXJ0IjoyMTE5LCJlbmQiOjIxMjAsInRleHQiOiJYIn0sIno2
SmxoRFBWRnpxb3U4MnUiOnsic3RhcnQiOjM1MTYsImVuZCI6Mz
UyNiwidGV4dCI6IkNoYXQgbGluazoifSwiZTRrb1dqOU1SZXJy
VWdFdiI6eyJzdGFydCI6MzYyOCwiZW5kIjozNjMxLCJ0ZXh0Ij
oiKEApIn19LCJjb21tZW50cyI6eyJxWldYRmd0ZUxkZnZVc2Qy
Ijp7ImRpc2N1c3Npb25JZCI6IkF6QnRtOWlIbkdLalVQZUYiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgbnVtYmVy
IiwiY3JlYXRlZCI6MTY4NjEyMDU1MDI4MX0sIjFPY0F4NDFJaH
R0dmtNaFMiOnsiZGlzY3Vzc2lvbklkIjoiejZKbGhEUFZGenFv
dTgydSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BsaW5rIiwiY3JlYXRlZCI6MTY4NjEyMzU1NzM1MH0sIkxwVDNS
Q3Rzb1REWmhReGgiOnsiZGlzY3Vzc2lvbklkIjoiZTRrb1dqOU
1SZXJyVWdFdiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBuYW1lcyIsImNyZWF0ZWQiOjE2ODYxMjM2MTEwMDd9fS
wiaGlzdG9yeSI6WzE5NjgzNjU2OTAsMTY3ODg0NzE4MCwxMDE0
NjY3MDg5LDIwNjYyOTc3OTksLTEzNjgyOTMxMTMsLTE5Nzc3ND
Y0MzUsOTAwODkxODE2XX0=
-->