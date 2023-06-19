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

11. 
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
UxMywidGV4dCI6IkZpZ3VyZSJ9fSwiY29tbWVudHMiOnsiR2JM
b3BWNGI1UFdwRE9pVCI6eyJkaXNjdXNzaW9uSWQiOiI3NlpVMU
tCVkY1M0JPNDN0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiUmV3cml0ZSIsImNyZWF0ZWQiOjE2ODcxNzA3ODE4NDd9LC
JtdjlpMmZIb0xXWWFJVThhIjp7ImRpc2N1c3Npb25JZCI6Ikg2
enk5NlFKWHk2TUxwUm0iLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzA4
MzUyNzB9LCJxVWl3U2pFTFRoN3RpSzU1Ijp7ImRpc2N1c3Npb2
5JZCI6IjJySkZTQVFKVXZZcjBGd1ciLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJGaXggcmVmZXJlbmNlIiwiY3JlYXRlZC
I6MTY4NzE3MDg4ODc3NH0sIlA5ZXhtWEtQazZJVE5pTHciOnsi
ZGlzY3Vzc2lvbklkIjoiUnRrMHJOUUJCdUZod0I1RSIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IldyaXRlIG91dCBpbnN0
cnVjdGlvbnMiLCJjcmVhdGVkIjoxNjg3MTcwOTUzNTQzfSwiUF
R0WGJOaG83MFFEMng4eCI6eyJkaXNjdXNzaW9uSWQiOiJaZTJR
T2VZYmVncDNBdWp4Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcx
NzA5NzczMTl9LCJBN3MwUng3Sm1XWXlrVzg2Ijp7ImRpc2N1c3
Npb25JZCI6IkhocDBaeENrR255NXlFdEEiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3
JlYXRlZCI6MTY4NzE3MDk5NDg4NX0sIkFLVXBxcHF1YWM0Vmox
bnAiOnsiZGlzY3Vzc2lvbklkIjoiWTdtMTlyZWt0enF4ZHVCZC
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3Qg
Zm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIj
oxNjg3MTcxMDcyNjU0fSwidDVqOVNvTFhDVmRiMjdENSI6eyJk
aXNjdXNzaW9uSWQiOiJXTlFRTTFSTGdyZmtacTM5Iiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJ
UyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNz
EwODEyOTZ9LCJ6elV5NUFqUnBWR3NEZ0pZIjp7ImRpc2N1c3Np
b25JZCI6ImlqcXZ0OXBLWHp0dEt6NlciLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJGaWd1cmUgb3V0IHdoYXQgdG8gZG8g
d2l0aCB0aGVzZSIsImNyZWF0ZWQiOjE2ODcxNzExOTY4Mzh9LC
JUdk5Oc0tmREtPM2ZrVHBlIjp7ImRpc2N1c3Npb25JZCI6IndQ
dkFqekpNa3podzg5dHAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0
dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI0NzAzMn0sIjBFd3BOam
5nR1kwSTYyRUMiOnsiZGlzY3Vzc2lvbklkIjoiWmtVdnc4N3dq
UjhEY3FCTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI5ODM3NX0s
IkFLRTRZRTdvN09ZZjZkRjMiOnsiZGlzY3Vzc2lvbklkIjoiTW
VvekRTcWs5OU5ia0hhUiIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkZpeCBjb3Vyc2Ugc3RydWN0dXJlIHRvIiwiY3JlYX
RlZCI6MTY4NzE3MTQyNTI1NX0sIkNFcUsxVHA0SkVRYUFXT2Qi
OnsiZGlzY3Vzc2lvbklkIjoiQXZGOWpwcUM3U2lYSGtKOCIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJl
IiwiY3JlYXRlZCI6MTY4NzE3MTQ1MjcyN30sIjY5VURYMHlWV0
FBSW9tYTUiOnsiZGlzY3Vzc2lvbklkIjoialB6cEZaVU5IcVZV
T3N5ciIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcn
JlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVh
dGVkIjoxNjg3MTcxNTIwNDU2fSwibXM3UmNkM1Nsb2ZJUWxkYy
I6eyJkaXNjdXNzaW9uSWQiOiJCNUtsWmhveTN4a2Z3cVBBIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cm
UiLCJjcmVhdGVkIjoxNjg3MTcxNTI5ODQ3fSwiV2xaY3E2N212
TDQyWklTcCI6eyJkaXNjdXNzaW9uSWQiOiJrUVJ2UVoyZjlid1
pxazJ2Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29y
cmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzE1NTIzMD
N9LCJkWndOWnF6ZG41UFBWRUdaIjp7ImRpc2N1c3Npb25JZCI6
InI1MExoT2JOV1BHNmQ2dWYiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6
MTY4NzE3MTU3NTcwNH0sImRSOEd4TjJFYVlaNHBiaE8iOnsiZG
lzY3Vzc2lvbklkIjoiMFlrM0JoVzN3d2FIRGFpZSIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSV
MgYW5kIHdyaXRlIG91dCBpbiBtb3JlIGRldGFpbCIsImNyZWF0
ZWQiOjE2ODcxNzE2MTkzMjh9LCJ1d3pHSkhLd2FWREE4Q2gxIj
p7ImRpc2N1c3Npb25JZCI6IjJqSjhDVzA4eWwxQ3k1WEUiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZS
IsImNyZWF0ZWQiOjE2ODcxNzE2Mzg5Mjh9fSwiaGlzdG9yeSI6
Wy0xMTgxNTY5OTAsLTg5MTU5OTIzM119
-->