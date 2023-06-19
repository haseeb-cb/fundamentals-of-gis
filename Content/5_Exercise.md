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

Questions:
- What do the hill shade parameters azimuth and altitude mean?
- What is the maximum slope of the study area based on the DEM10m_Muurla?
- How about the mean slope of the study area based on the DEM10m_Muurla?

### 1.2: Data type conversions - feature to raster
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
I6IjUifSwiaWpxdnQ5cEtYenR0S3o2VyI6eyJzdGFydCI6MzIy
OCwiZW5kIjozMjM4LCJ0ZXh0IjoiUXVlc3Rpb25zOiJ9LCJ3UH
ZBanpKTWt6aHc4OXRwIjp7InN0YXJ0IjozNzk5LCJlbmQiOjM4
MDAsInRleHQiOiI2In0sIlprVXZ3ODd3alI4RGNxQk8iOnsic3
RhcnQiOjQyMDQsImVuZCI6NDIxMCwidGV4dCI6IkZpZ3VyZSJ9
fSwiY29tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVCI6eyJkaX
NjdXNzaW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsImNyZWF0ZW
QiOjE2ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJVThhIjp7
ImRpc2N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm0iLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIs
ImNyZWF0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2pFTFRoN3
RpSzU1Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFKVXZZcjBG
d1ciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcm
VmZXJlbmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3NH0sIlA5
ZXhtWEtQazZJVE5pTHciOnsiZGlzY3Vzc2lvbklkIjoiUnRrMH
JOUUJCdUZod0I1RSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IldyaXRlIG91dCBpbnN0cnVjdGlvbnMiLCJjcmVhdGVkIj
oxNjg3MTcwOTUzNTQzfSwiUFR0WGJOaG83MFFEMng4eCI6eyJk
aXNjdXNzaW9uSWQiOiJaZTJRT2VZYmVncDNBdWp4Iiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJ
UyIsImNyZWF0ZWQiOjE2ODcxNzA5NzczMTl9LCJBN3MwUng3Sm
1XWXlrVzg2Ijp7ImRpc2N1c3Npb25JZCI6IkhocDBaeENrR255
NXlFdEEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3
JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MDk5NDg4
NX0sIkFLVXBxcHF1YWM0VmoxbnAiOnsiZGlzY3Vzc2lvbklkIj
oiWTdtMTlyZWt0enF4ZHVCZCIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdH
J1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMDcyNjU0fSwidDVq
OVNvTFhDVmRiMjdENSI6eyJkaXNjdXNzaW9uSWQiOiJXTlFRTT
FSTGdyZmtacTM5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZS
IsImNyZWF0ZWQiOjE2ODcxNzEwODEyOTZ9LCJ6elV5NUFqUnBW
R3NEZ0pZIjp7ImRpc2N1c3Npb25JZCI6ImlqcXZ0OXBLWHp0dE
t6NlciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaWd1
cmUgb3V0IHdoYXQgdG8gZG8gd2l0aCB0aGVzZSIsImNyZWF0ZW
QiOjE2ODcxNzExOTY4Mzh9LCJUdk5Oc0tmREtPM2ZrVHBlIjp7
ImRpc2N1c3Npb25JZCI6IndQdkFqekpNa3podzg5dHAiLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBR
R0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4Nz
E3MTI0NzAzMn0sIjBFd3BOam5nR1kwSTYyRUMiOnsiZGlzY3Vz
c2lvbklkIjoiWmtVdnc4N3dqUjhEY3FCTyIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRl
ZCI6MTY4NzE3MTI5ODM3NX19LCJoaXN0b3J5IjpbMTgzMTI5NT
kzMCwtODkxNTk5MjMzXX0=
-->