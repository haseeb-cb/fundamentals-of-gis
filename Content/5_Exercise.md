### Fundamentals of Geographic Information Systems (GIS)

# Exercise 5: 

## OVERVIEW & PURPOSE


## OBJECTIVES
The aim of this practical is to learn the basics of Raster GIS and to perform cartographic modeling that is based on map algebra. The subject is introduced through an exercise where the goal is to locate the optimal cultivation areas.

The student will also learn how to utilize a Digital Elevation Model (DEM) and make data type conversions from vector to raster. To strengthen the assimilation, a short reflection will be written on what was done and why.

## DATA USED

## Completion

Work in pairs or individually. Complete the exercise and submit a short report containing at least the following:

1. Maps of the outcome of the exercise

	- Remember: all maps should have a legend, a scale bar and a north arrow

	- Use the tips from the Crash Course to improve your map

2. A short reflection (200-300 words) on this exercise and your map

## EXERCISE PHASES

### 1.1: Getting to know the digital elevation model

- Figure of DEM

1. Start the exercise by downloading the data “Exercise7.zip” from the course portal in Moodle and saving it in a folder for this exercise.

2. You have to download the Digital Elevation Model (DEM) from PaITuli. Select National Land Survey of Finland (NLS) Elevation Model as the data, 10m x 10m as the grid size (cell size), type L3343 to the search bar and download the given files.

3. Add the Digital Elevation Model you downloaded from PaITuli. The program will probably ask whether you want to add pyramids – in this case just press yes. The DEM is a large raster image file and thus rather heavy to process. To make the program run smoother, clip the DEM to a smaller extent. Study area for the practical is the same as Muurla_Frame -layer, use it for the clipping extent.

*Tip: there’s separate tools for vector and raster files. Clipping rasters happens with Clip Raster -tool. Don’t forget to name your output files! Great name for this file could be DEM10m_Muurla, for example.*

4. One of the important features of DEM is that it can be used to create a hillshade relief. Hillshade is mostly used in visualization to create an imposing 3D-effect of the surface. To create a hillshade, open Tools and navigate to Spatial Analyst Tools → Surface → Hillshade. Choose the clipped DEM as the input raster and set the output folder. Try first how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.

*Tip: Again, name the files! Good name for the first Hillshade could be for example “HillShade_Muurla_def” or “HS_Muurla_def” indicating that it’s a hillshade, study area and default settings – for the next one you could change the name to for example “HS_Muurla_Az180” and so on, based on the chosen settings.*

5. Another very useful feature of a DEM is the possibility to identify the gradient of the raster surface. This can be done with the Slope –tool, which can also be found under the Surface -tools. Again, use the clipped DEM as the input raster and perform the operation. You can use the default settings.
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI3NlpVMUtCVkY1M0JPNDN0Ijp7In
N0YXJ0Ijo5OCwiZW5kIjoxMTEsInRleHQiOiIjIyBPQkpFQ1RJ
VkVTIn0sIkg2enk5NlFKWHk2TUxwUm0iOnsic3RhcnQiOjEwMz
IsImVuZCI6MTA0NywidGV4dCI6Ii0gRmlndXJlIG9mIERFTSJ9
LCIyckpGU0FRSlV2WXIwRndXIjp7InN0YXJ0IjoxMTM3LCJlbm
QiOjExNDMsInRleHQiOiJNb29kbGUifSwiUnRrMHJOUUJCdUZo
d0I1RSI6eyJzdGFydCI6MTE5MCwiZW5kIjoxMTkxLCJ0ZXh0Ij
oiMiJ9LCJaZTJRT2VZYmVncDNBdWp4Ijp7InN0YXJ0IjoxNDM2
LCJlbmQiOjE0MzcsInRleHQiOiIzIn0sIkhocDBaeENrR255NX
lFdEEiOnsic3RhcnQiOjE4MzIsImVuZCI6MTgzNSwidGV4dCI6
IlRpcCJ9LCJZN20xOXJla3R6cXhkdUJkIjp7InN0YXJ0IjoyMD
QyLCJlbmQiOjIwNDMsInRleHQiOiI0In0sIldOUVFNMVJMZ3Jm
a1pxMzkiOnsic3RhcnQiOjI5MjMsImVuZCI6MjkyNCwidGV4dC
I6IjUifX0sImNvbW1lbnRzIjp7IkdiTG9wVjRiNVBXcERPaVQi
OnsiZGlzY3Vzc2lvbklkIjoiNzZaVTFLQlZGNTNCTzQzdCIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlJld3JpdGUiLCJj
cmVhdGVkIjoxNjg3MTcwNzgxODQ3fSwibXY5aTJmSG9MV1lhSV
U4YSI6eyJkaXNjdXNzaW9uSWQiOiJINnp5OTZRSlh5Nk1McFJt
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3
R1cmUiLCJjcmVhdGVkIjoxNjg3MTcwODM1MjcwfSwicVVpd1Nq
RUxUaDd0aUs1NSI6eyJkaXNjdXNzaW9uSWQiOiIyckpGU0FRSl
V2WXIwRndXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
Rml4IHJlZmVyZW5jZSIsImNyZWF0ZWQiOjE2ODcxNzA4ODg3Nz
R9LCJQOWV4bVhLUGs2SVROaUx3Ijp7ImRpc2N1c3Npb25JZCI6
IlJ0azByTlFCQnVGaHdCNUUiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJXcml0ZSBvdXQgaW5zdHJ1Y3Rpb25zIiwiY3Jl
YXRlZCI6MTY4NzE3MDk1MzU0M30sIlBUdFhiTmhvNzBRRDJ4OH
giOnsiZGlzY3Vzc2lvbklkIjoiWmUyUU9lWWJlZ3AzQXVqeCIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm
9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcwOTc3MzE5fSwiQTdz
MFJ4N0ptV1l5a1c4NiI6eyJkaXNjdXNzaW9uSWQiOiJIaHAwWn
hDa0dueTV5RXRBIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNz
A5OTQ4ODV9LCJBS1VwcXBxdWFjNFZqMW5wIjp7ImRpc2N1c3Np
b25JZCI6Ilk3bTE5cmVrdHpxeGR1QmQiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBm
aXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTA3MjY1NH
0sInQ1ajlTb0xYQ1ZkYjI3RDUiOnsiZGlzY3Vzc2lvbklkIjoi
V05RUU0xUkxncmZrWnEzOSIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1
Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMDgxMjk2fX0sImhpc3
RvcnkiOlsyMDc4NDMyODk2LC04OTE1OTkyMzNdfQ==
-->