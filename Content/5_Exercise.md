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

### Part 1: Getting familiar with raster data
This exercise focuses mainly on raster data and raster analysis. You have already gotten used to working with vector data, but even though the world of raster might feel slightly complicated at first, it is just as simple as with vector when you get accustomed to it.

#### 1.1: Getting to know the digital elevation model

- Figure of DEM

1. Start the exercise by downloading the data “Exercise7.zip” from the course portal in Moodle and saving it in a folder for this exercise.

2. You have to download the Digital Elevation Model (DEM) from PaITuli. Select National Land Survey of Finland (NLS) Elevation Model as the data, 10m x 10m as the grid size (cell size), type L3343 to the search bar and download the given files.

3. Add the Digital Elevation Model you downloaded from PaITuli. The program will probably ask whether you want to add pyramids – in this case just press yes. The DEM is a large raster image file and thus rather heavy to process. To make the program run smoother, clip the DEM to a smaller extent. Study area for the practical is the same as Muurla_Frame -layer, use it for the clipping extent.

*Tip: there’s separate tools for vector and raster files. Clipping rasters happens with Clip Raster -tool. Don’t forget to name your output files! Great name for this file could be DEM10m_Muurla, for example.*

4. One of the important features of DEM is that it can be used to create a hillshade relief. Hillshade is mostly used in visualization to create an imposing 3D-effect of the surface. To create a hillshade, open Tools and navigate to Spatial Analyst Tools → Surface → Hillshade. Choose the clipped DEM as the input raster and set the output folder. Try first how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.

*Tip: Again, name the files! Good name for the first Hillshade could be for example “HillShade_Muurla_def” or “HS_Muurla_def” indicating that it’s a hillshade, study area and default settings – for the next one you could change the name to for example “HS_Muurla_Az180” and so on, based on the chosen settings.*

5. Another very useful feature of a DEM is the possibility to identify the gradient of the raster surface. This can be done with the Slope –tool, which can also be found under the Surface -tools. Again, use the clipped DEM as the input raster and perform the operation. You can use the default settings.

Questions:
- What do the hill shade parameters azimuth and altitude mean?
- What is the maximum slope of the study area based on the DEM10m_Muurla?
- How about the mean slope of the study area based on the DEM10m_Muurla?

#### 1.2: Data type conversions - feature to raster
It is quite common in GIS that data has to be converted from one type to another; some analyses for instance require a certain file type to work. In part two of this exercise you are going to need the shapefile “Muurla_Soil.shp” as a raster file to be able to perform the raster overlay analyses.

6. So, without further ado, navigate to Conversion Tools -> To Raster and select Feature to Raster, as you are rasterizing a shapefile. Raster can’t have multiple attributes like shapefiles do. Column “PINTA” has the information which we want to use for the analysis, so this is the column you should select for “Field” -parameter. Name the file and choose the same cell size as you chose for the DEM.

- Figure

---

### 2: Modelling optimal cultivation areas

Southwest Finland is sometimes called as the bread-basket of Finland that refers to its plentiful fields and agricultural productivity. In this exercise your task is to model optimal cultivation areas using raster data analyses in Muurla, which is a district of Salo, a city between Turku and Helsinki.

The aim is to classify the study area based on its suitability for cultivation. The criteria are the following:

- Good or moderate soil
- Slope < 15°
- Minimum distance of 10m from the bodies of water
- The soil factor is twice as important as the slope factor

In the earlier phase you already clipped the DEM, calculated the slope and made the feature to raster conversion for the soil so some phases are already done. The following flow chart shows the different stages of the optimal cultivation areas analysis.

- Figure

#### 2.1: Defining the unsuitable areas


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI3NlpVMUtCVkY1M0JPNDN0Ijp7In
N0YXJ0Ijo5OCwiZW5kIjoxMTEsInRleHQiOiIjIyBPQkpFQ1RJ
VkVTIn0sIkg2enk5NlFKWHk2TUxwUm0iOnsic3RhcnQiOjEzND
gsImVuZCI6MTM2MywidGV4dCI6Ii0gRmlndXJlIG9mIERFTSJ9
LCIyckpGU0FRSlV2WXIwRndXIjp7InN0YXJ0IjoxNDUzLCJlbm
QiOjE0NTksInRleHQiOiJNb29kbGUifSwiUnRrMHJOUUJCdUZo
d0I1RSI6eyJzdGFydCI6MTUwNiwiZW5kIjoxNTA3LCJ0ZXh0Ij
oiMiJ9LCJaZTJRT2VZYmVncDNBdWp4Ijp7InN0YXJ0IjoxNzUy
LCJlbmQiOjE3NTMsInRleHQiOiIzIn0sIkhocDBaeENrR255NX
lFdEEiOnsic3RhcnQiOjIxNDgsImVuZCI6MjE1MSwidGV4dCI6
IlRpcCJ9LCJZN20xOXJla3R6cXhkdUJkIjp7InN0YXJ0IjoyMz
U4LCJlbmQiOjIzNTksInRleHQiOiI0In0sIldOUVFNMVJMZ3Jm
a1pxMzkiOnsic3RhcnQiOjMyMzksImVuZCI6MzI0MCwidGV4dC
I6IjUifSwiaWpxdnQ5cEtYenR0S3o2VyI6eyJzdGFydCI6MzU0
NCwiZW5kIjozNTU0LCJ0ZXh0IjoiUXVlc3Rpb25zOiJ9LCJ3UH
ZBanpKTWt6aHc4OXRwIjp7InN0YXJ0Ijo0MTE2LCJlbmQiOjQx
MTcsInRleHQiOiI2In0sIlprVXZ3ODd3alI4RGNxQk8iOnsic3
RhcnQiOjQ1MjEsImVuZCI6NDUyNywidGV4dCI6IkZpZ3VyZSJ9
LCJNZW96RFNxazk5TmJrSGFSIjp7InN0YXJ0Ijo5NzgsImVuZC
I6MTAyMywidGV4dCI6IiMjIyBQYXJ0IDE6IEdldHRpbmcgZmFt
aWxpYXIgd2l0aCByYXN0ZXIgZGF0YSJ9LCJBdkY5anBxQzdTaV
hIa0o4Ijp7InN0YXJ0Ijo1NDAyLCJlbmQiOjU0MDgsInRleHQi
OiJGaWd1cmUifX0sImNvbW1lbnRzIjp7IkdiTG9wVjRiNVBXcE
RPaVQiOnsiZGlzY3Vzc2lvbklkIjoiNzZaVTFLQlZGNTNCTzQz
dCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlJld3JpdG
UiLCJjcmVhdGVkIjoxNjg3MTcwNzgxODQ3fSwibXY5aTJmSG9M
V1lhSVU4YSI6eyJkaXNjdXNzaW9uSWQiOiJINnp5OTZRSlh5Nk
1McFJtIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRk
IHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcwODM1MjcwfSwicV
Vpd1NqRUxUaDd0aUs1NSI6eyJkaXNjdXNzaW9uSWQiOiIyckpG
U0FRSlV2WXIwRndXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiRml4IHJlZmVyZW5jZSIsImNyZWF0ZWQiOjE2ODcxNzA4
ODg3NzR9LCJQOWV4bVhLUGs2SVROaUx3Ijp7ImRpc2N1c3Npb2
5JZCI6IlJ0azByTlFCQnVGaHdCNUUiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJXcml0ZSBvdXQgaW5zdHJ1Y3Rpb25zIi
wiY3JlYXRlZCI6MTY4NzE3MDk1MzU0M30sIlBUdFhiTmhvNzBR
RDJ4OHgiOnsiZGlzY3Vzc2lvbklkIjoiWmUyUU9lWWJlZ3AzQX
VqeCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJl
Y3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcwOTc3MzE5fS
wiQTdzMFJ4N0ptV1l5a1c4NiI6eyJkaXNjdXNzaW9uSWQiOiJI
aHAwWnhDa0dueTV5RXRBIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2
ODcxNzA5OTQ4ODV9LCJBS1VwcXBxdWFjNFZqMW5wIjp7ImRpc2
N1c3Npb25JZCI6Ilk3bTE5cmVrdHpxeGR1QmQiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIG
FuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTA3
MjY1NH0sInQ1ajlTb0xYQ1ZkYjI3RDUiOnsiZGlzY3Vzc2lvbk
lkIjoiV05RUU0xUkxncmZrWnEzOSIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeC
BzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMDgxMjk2fSwi
enpVeTVBalJwVkdzRGdKWSI6eyJkaXNjdXNzaW9uSWQiOiJpan
F2dDlwS1h6dHRLejZXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiRmlndXJlIG91dCB3aGF0IHRvIGRvIHdpdGggdGhlc2
UiLCJjcmVhdGVkIjoxNjg3MTcxMTk2ODM4fSwiVHZOTnNLZkRL
TzNma1RwZSI6eyJkaXNjdXNzaW9uSWQiOiJ3UHZBanpKTWt6aH
c4OXRwIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29y
cmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZW
F0ZWQiOjE2ODcxNzEyNDcwMzJ9LCIwRXdwTmpuZ0dZMEk2MkVD
Ijp7ImRpc2N1c3Npb25JZCI6IlprVXZ3ODd3alI4RGNxQk8iLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVy
ZSIsImNyZWF0ZWQiOjE2ODcxNzEyOTgzNzV9LCJBS0U0WUU3bz
dPWWY2ZEYzIjp7ImRpc2N1c3Npb25JZCI6Ik1lb3pEU3FrOTlO
YmtIYVIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaX
ggY291cnNlIHN0cnVjdHVyZSB0byIsImNyZWF0ZWQiOjE2ODcx
NzE0MjUyNTV9LCJDRXFLMVRwNEpFUWFBV09kIjp7ImRpc2N1c3
Npb25JZCI6IkF2RjlqcHFDN1NpWEhrSjgiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZW
QiOjE2ODcxNzE0NTI3Mjd9fSwiaGlzdG9yeSI6WzQwNjAzMjky
LC04OTE1OTkyMzNdfQ==
-->