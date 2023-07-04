![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/logo-en-purple-small.png)
### Fundamentals of Geographic Information Systems (GIS)
 
# Course introduction

**Welcome to the *Fundamentals of Geographic Information Systems (GIS)* course!** This is an open course developed by Tampere University meant to get you started with GIS and give you the ability to work with GIS independently. 

This course can be completed independently, or as a student at the Tampere University. Everyone is able to access the course materials and support, with the exception that students have to complete a number of criteria and if they do so, they are eligible for ECTS credits. 

## Learning outcomes
After completing the course you should be able to:
- Understand the fundamental principles of GIS, including rasters, vector, projections, geoprocessing and analysis
- Apply basic GIS skills to:
	- Map Design
	- Gathering GIS data from various sources
	- Use different types of spatial data
	- Analyse GIS data to address geosptial problems and/or research questions 
- Develop the aiblity to perform new anayses, troubleshoot, and find help from the GIS community to solve your problems

## Structure
The course consists of **9 exercises**, each accompanied by a piece of theory. It's recommended to go through the theory before attempting the exercise. The first exercise is meant to give you the basic skills in GIS and the software we will be using, QGIS. From there on you will build on these basic skills using the other exercises, covering various analyses and methods, and develop a fundamental skillset in GIS and QGIS. 

| Exercise | Topic | Methods |
|--|--|--|
| [1](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/1_Crashcourse_theory.md) | Crash Course| QGIS interface & Vector analysis |
| [2](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/2_Theory.md) | Vector analysis introduction | Digitizing, georeferencing, clipping |
| [3](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/3_Theory.md) | Socio-spatial differentiation | Raster analysis |
| [4](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/4_theory.md) | Finding the optimal location for a new development | Buffer analysis, overlay analysis |
| [5](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/5_Theory.md) | Determining optimal land for cultivation | Digital Elevation Model (DEM), slope, hillshade, overlay analysis |
| [6](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/6_Theory.md) | Understanding disease transmission | Heatmap analysis (Kernel Density), Voronoi diagram, text processing |
| [7](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/7_Theory.md) | Air quality analysis | Spatial interpolation
| [8](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/8_Theory.md) | Calculating building efficiency | Expressions, creating grids |
| [9](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/9_Theory.md) | Wind power NIMBY (Not in my backyard) analysis | Public Participation GIS/SoftGIS, Directional Distribution |

## Evaluation
To get the credits for this course, the following criteria have to be met:
 - [ ] Submitted original map output(s) for each exercise
	 - With your name on the output
 - [ ] Submitted original map reflection for each exercise
 - [ ] Completed the Moodle exams  

To ensure that your submissions are original:
- Map output: Your name has to be mentioned on the map output and they will be compared with others
- Map reflection: Anti-plagiarism tool is used

## Troubleshooting
If you ever have a question or run in to an issue along this course, please follow the following troubleshooting process: 

![Troubleshooting process](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/0_Course_introduction/GIS_troubleshooting_process.drawio.png)
1. Start by checking if the information in the **course materials** provide a solution, it might have been covered in the previous theory or exercises as well
	- If you come across missing information in the materials, please let us know so we can make sure others don't run into the same issue! 
2. Being a *Professional **Google** Searcher* will get you really far with (Q)GIS. Try searching your question or issue, below you can find some tips on how to improve your google searches
	- [Simple Google Search tips](https://www.youtube.com/watch?v=oIMTM168BK8)
	- [How to "Google It" like a Senior Software Engineer](https://www.youtube.com/watch?v=cEBkvm0-rg0)
	- [Refine web searches](https://support.google.com/websearch/answer/2466433?hl=en)
3. Ask your question in the **chat**, other students or professionals will be able to help you! Use the channel of the exercise you are working on. 
	- [Chat invite link (Microsoft Teams)](https://teams.microsoft.com/l/team/19:HduKwpmM4c7LyKk3vcQFZnV_uIFMB63WvG-e_p6P1wM1@thread.tacv2/conversations?groupId=713525aa-e19b-4ba5-9491-cba5bcfc17be&tenantId=fa6944af-cc7c-4cd8-9154-c01132798910)
5.  If at this point you still have not found a resolution, you can ping the **teachers** in the channel with @teachers

Following this process will help you **develop the independent troubleshooting skills** you will need when you use GIS on your own. 

## Tools
- Github (where to download data)
- Chat
- Moodle
- QGIS 

## Feedback

## Credits

# Let's get started with the [first theory section](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Content/1_Crashcourse_theory.md)!
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI0b3M2a2lvb2g0a3lDZFdiIjp7In
N0YXJ0Ijo1MzU5LCJlbmQiOjU0MjQsInRleHQiOiIjIyBUb29s
c1xuLSBHaXRodWIgKHdoZXJlIHRvIGRvd25sb2FkIGRhdGEpXG
4tIENoYXRcbi0gTW9vZGxlXG4tIFFHSVMifSwiSzVkcE9KaUx3
RnI1eTk0diI6eyJzdGFydCI6NTQyNywiZW5kIjo1NDM4LCJ0ZX
h0IjoiIyMgRmVlZGJhY2sifSwibGswYVZNeXJIVFNEc3lvaSI6
eyJzdGFydCI6NTQ0MCwiZW5kIjo1NDUwLCJ0ZXh0IjoiIyMgQ3
JlZGl0cyJ9fSwiY29tbWVudHMiOnsiNkdIUzJLNE1GTmdPZE5P
QyI6eyJkaXNjdXNzaW9uSWQiOiI0b3M2a2lvb2g0a3lDZFdiIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHNlY3Rp
b24iLCJjcmVhdGVkIjoxNjg3MDY0ODgwMzgxfSwiU2lkd1JkWF
lPT2U2MU4xOCI6eyJkaXNjdXNzaW9uSWQiOiJLNWRwT0ppTHdG
cjV5OTR2Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIGZlZWRiYWNrIHNlY3Rpb24iLCJjcmVhdGVkIjoxNjg4NDU1
NDU2MzE0fSwiUUtieml0aUEwc0l0MVRkaiI6eyJkaXNjdXNzaW
9uSWQiOiJsazBhVk15ckhUU0RzeW9pIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQWRkIGNyZWRpdHMgc2VjdGlvbiIsIm
NyZWF0ZWQiOjE2ODg0NTU0NzIzMjl9fSwiaGlzdG9yeSI6WzU5
Mzk4ODY4MSwtODkxNzEzMTQ1LDQyMDUwMjk2NSwtMTExNzMwMj
k0NSwtMTY1MjU1MzY1Miw3MzM3MDI2NDMsMTU2MjE5MTI4LDg4
NTQxNzgyNCwtMTkyOTgwMjIyOSwxMTgzNTcyNjI4XX0=
-->