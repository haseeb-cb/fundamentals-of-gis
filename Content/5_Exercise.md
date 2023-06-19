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
7. One initial preparation to be done before starting is to set the environment settings which can be found under the Analysis tab → Environments. Apply the environment settings specified below. It is good to remember that the cell size is always determined by the layer with the lowest resolution. Close the Environment Settings by pressing OK.

- Figure

8. Start off with the water criteria. Go to Buffer -tool and make a 10-meter buffer for the Bodies_of_Water -layer without dissolving.

9. Next, you have to convert the newly created buffer zone -layer to raster format. As learned before in this practical, use the Feature to Raster -tool to make this rasterization. Choose “FID” as the field to assign the values to the output raster and check that the cell size matches DEM.

10.  Next navigate to Spatial Analyst Tools → Reclass → Reclassify. In order for the further calculations to succeed, you have to make the NoData acceptable because those areas are the ones without water. Make the changes as below and save the file as “reclass_water”.

- Figure

11. Let’s continue with defining the unsuitable areas by determining the “bad slopes”. Use the Reclassify -tool again, choose this time the slope raster as the input and press the classify button. In the new window choose reduce the number of classes to 2 and set the upper break values on the right manually as 15 and 54. Return to the first page by pressing OK and fill in the rest of the form using the image below as your support.

The “water buffer” and the “bad slopes” will be classified as “0” so that they can be removed from the calculations later on with multiplication.

- Figure

12. Now let’s combine the bad criteria layers with the Raster Calculator -tool which can be found under Map Algebra in Spatial Analyst Tools within Toolbox. Multiply the “Reclass_Water” with “BadSlope” layer in the calculator to create an “Unsuitable_areas”-layer. Always choose the layers and tools from the menus above to ensure correct form.


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
OiJGaWd1cmUifSwialB6cEZaVU5IcVZVT3N5ciI6eyJzdGFydC
I6NTQ1MCwiZW5kIjo1NDUxLCJ0ZXh0IjoiNyJ9LCJCNUtsWmhv
eTN4a2Z3cVBBIjp7InN0YXJ0Ijo1Nzk5LCJlbmQiOjU4MDUsIn
RleHQiOiJGaWd1cmUifSwia1FSdlFaMmY5YndacWsydiI6eyJz
dGFydCI6NTgwNywiZW5kIjo1ODA4LCJ0ZXh0IjoiOCJ9LCJyNT
BMaE9iTldQRzZkNnVmIjp7InN0YXJ0Ijo1OTQzLCJlbmQiOjU5
NDQsInRleHQiOiI5In0sIjBZazNCaFczd3dhSERhaWUiOnsic3
RhcnQiOjYyMzUsImVuZCI6NjIzNywidGV4dCI6IjEwIn0sIjJq
SjhDVzA4eWwxQ3k1WEUiOnsic3RhcnQiOjY1MDcsImVuZCI6Nj
UxMywidGV4dCI6IkZpZ3VyZSJ9LCJNSUYxODZ3WjV4bmR6WDU1
Ijp7InN0YXJ0Ijo2NTE1LCJlbmQiOjY1MTcsInRleHQiOiIxMS
J9LCJ1aGhUYkVMcXlSMHZzTTFPIjp7InN0YXJ0Ijo3MTAwLCJl
bmQiOjcxMDYsInRleHQiOiJGaWd1cmUifX0sImNvbW1lbnRzIj
p7IkdiTG9wVjRiNVBXcERPaVQiOnsiZGlzY3Vzc2lvbklkIjoi
NzZaVTFLQlZGNTNCTzQzdCIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IlJld3JpdGUiLCJjcmVhdGVkIjoxNjg3MTcwNzgx
ODQ3fSwibXY5aTJmSG9MV1lhSVU4YSI6eyJkaXNjdXNzaW9uSW
QiOiJINnp5OTZRSlh5Nk1McFJtIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNj
g3MTcwODM1MjcwfSwicVVpd1NqRUxUaDd0aUs1NSI6eyJkaXNj
dXNzaW9uSWQiOiIyckpGU0FRSlV2WXIwRndXIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IHJlZmVyZW5jZSIsImNy
ZWF0ZWQiOjE2ODcxNzA4ODg3NzR9LCJQOWV4bVhLUGs2SVROaU
x3Ijp7ImRpc2N1c3Npb25JZCI6IlJ0azByTlFCQnVGaHdCNUUi
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXcml0ZSBvdX
QgaW5zdHJ1Y3Rpb25zIiwiY3JlYXRlZCI6MTY4NzE3MDk1MzU0
M30sIlBUdFhiTmhvNzBRRDJ4OHgiOnsiZGlzY3Vzc2lvbklkIj
oiWmUyUU9lWWJlZ3AzQXVqeCIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIj
oxNjg3MTcwOTc3MzE5fSwiQTdzMFJ4N0ptV1l5a1c4NiI6eyJk
aXNjdXNzaW9uSWQiOiJIaHAwWnhDa0dueTV5RXRBIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJ
UyIsImNyZWF0ZWQiOjE2ODcxNzA5OTQ4ODV9LCJBS1VwcXBxdW
FjNFZqMW5wIjp7ImRpc2N1c3Npb25JZCI6Ilk3bTE5cmVrdHpx
eGR1QmQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3
JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MTA3MjY1NH0sInQ1ajlTb0xYQ1ZkYjI3RD
UiOnsiZGlzY3Vzc2lvbklkIjoiV05RUU0xUkxncmZrWnEzOSIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm
9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjox
Njg3MTcxMDgxMjk2fSwienpVeTVBalJwVkdzRGdKWSI6eyJkaX
NjdXNzaW9uSWQiOiJpanF2dDlwS1h6dHRLejZXIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRmlndXJlIG91dCB3aGF0IH
RvIGRvIHdpdGggdGhlc2UiLCJjcmVhdGVkIjoxNjg3MTcxMTk2
ODM4fSwiVHZOTnNLZkRLTzNma1RwZSI6eyJkaXNjdXNzaW9uSW
QiOiJ3UHZBanpKTWt6aHc4OXRwIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IH
N0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzEyNDcwMzJ9LCIw
RXdwTmpuZ0dZMEk2MkVDIjp7ImRpc2N1c3Npb25JZCI6IlprVX
Z3ODd3alI4RGNxQk8iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzEyOT
gzNzV9LCJBS0U0WUU3bzdPWWY2ZEYzIjp7ImRpc2N1c3Npb25J
ZCI6Ik1lb3pEU3FrOTlOYmtIYVIiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJGaXggY291cnNlIHN0cnVjdHVyZSB0byIs
ImNyZWF0ZWQiOjE2ODcxNzE0MjUyNTV9LCJDRXFLMVRwNEpFUW
FBV09kIjp7ImRpc2N1c3Npb25JZCI6IkF2RjlqcHFDN1NpWEhr
SjgiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcG
ljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE0NTI3Mjd9LCI2OVVE
WDB5VldBQUlvbWE1Ijp7ImRpc2N1c3Npb25JZCI6ImpQenBGWl
VOSHFWVU9zeXIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIi
wiY3JlYXRlZCI6MTY4NzE3MTUyMDQ1Nn0sIm1zN1JjZDNTbG9m
SVFsZGMiOnsiZGlzY3Vzc2lvbklkIjoiQjVLbFpob3kzeGtmd3
FQQSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBw
aWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTUyOTg0N30sIldsWm
NxNjdtdkw0MlpJU3AiOnsiZGlzY3Vzc2lvbklkIjoia1FSdlFa
MmY5YndacWsydiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcx
NTUyMzAzfSwiZFp3TlpxemRuNVBQVkVHWiI6eyJkaXNjdXNzaW
9uSWQiOiJyNTBMaE9iTldQRzZkNnVmIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZW
F0ZWQiOjE2ODcxNzE1NzU3MDR9LCJkUjhHeE4yRWFZWjRwYmhP
Ijp7ImRpc2N1c3Npb25JZCI6IjBZazNCaFczd3dhSERhaWUiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZv
ciBRR0lTIGFuZCB3cml0ZSBvdXQgaW4gbW9yZSBkZXRhaWwiLC
JjcmVhdGVkIjoxNjg3MTcxNjE5MzI4fSwidXd6R0pIS3dhVkRB
OENoMSI6eyJkaXNjdXNzaW9uSWQiOiIyako4Q1cwOHlsMUN5NV
hFIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBp
Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNjM4OTI4fSwiVnoxZl
FhS0ZzYUl0V0RPYyI6eyJkaXNjdXNzaW9uSWQiOiJNSUYxODZ3
WjV4bmR6WDU1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIs
ImNyZWF0ZWQiOjE2ODcxNzE2NzcwNzF9LCJGdUlpY1pHenYxdl
pGcWpYIjp7ImRpc2N1c3Npb25JZCI6InVoaFRiRUxxeVIwdnNN
MU8iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcG
ljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3MDUzNjB9fSwiaGlz
dG9yeSI6Wy02OTI1OTkzOSwtODkxNTk5MjMzXX0=
-->