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

- Figure

#### 2.2: Defining the suitable areas

13. Now after you have identified the unsuitable areas, your next task it to rank the suitable ones. To make the “slope rank” go once again to Reclassify. Choose the original Slope_Muurla file as the input raster and open the classify window. Choose 4 classes and give the following break values 3, 7, 15, 54. Rank the classes as in the Figure 4 and name the file “slope_rank”.

Let’s move on to ranking the soil. You can see the explanation for the soil codes below.

- Figure

14. Open the Reclassify -tool and specify the values as in the Figure 5. The higher the value the better the soil fits for cultivation.

- Figure

***Note**: for simplicity, we did not identify an ‘unsuitable_soil’ layer but only the soil_rank, i.e. areas with soil type as rock will show a low suitability, but they will not be identified as completely unsuitable if they e.g. are located in a suitable slope pixel. This is ok for the purpose of the exercise, but it is good to keep it in mind. As an optional task, you can add them to unsuitable areas and make another analysis as well.*

#### 2.3: Identifying th


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
bmQiOjcxMDYsInRleHQiOiJGaWd1cmUifSwiazFqRVlRMWtaYT
Y1YmJNMCI6eyJzdGFydCI6NzEwOCwiZW5kIjo3MTEwLCJ0ZXh0
IjoiMTIifSwiMlpsOENxSkFFd3FLeER2VCI6eyJzdGFydCI6Nz
Q1NiwiZW5kIjo3NDYyLCJ0ZXh0IjoiRmlndXJlIn0sIkFqZWJH
ZHYyRG1SckU2RXAiOnsic3RhcnQiOjc1MDMsImVuZCI6NzUwNS
widGV4dCI6IjEzIn0sIk1LNDZ6RGZPVHY0b2VxNmIiOnsic3Rh
cnQiOjc5NzIsImVuZCI6Nzk4MCwidGV4dCI6Ii0gRmlndXJlIn
0sIlNDNXc5NmJYNmlTcnFGb0MiOnsic3RhcnQiOjc5ODIsImVu
ZCI6Nzk4NCwidGV4dCI6IjE0In0sInExaVY2YkdwNWY0cmZGd1
EiOnsic3RhcnQiOjgxMjEsImVuZCI6ODEyNywidGV4dCI6IkZp
Z3VyZSJ9fSwiY29tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVC
I6eyJkaXNjdXNzaW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsIm
NyZWF0ZWQiOjE2ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJ
VThhIjp7ImRpc2N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm
0iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2
pFTFRoN3RpSzU1Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFK
VXZZcjBGd1ciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JGaXggcmVmZXJlbmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3
NH0sIlA5ZXhtWEtQazZJVE5pTHciOnsiZGlzY3Vzc2lvbklkIj
oiUnRrMHJOUUJCdUZod0I1RSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IldyaXRlIG91dCBpbnN0cnVjdGlvbnMiLCJjcm
VhdGVkIjoxNjg3MTcwOTUzNTQzfSwiUFR0WGJOaG83MFFEMng4
eCI6eyJkaXNjdXNzaW9uSWQiOiJaZTJRT2VZYmVncDNBdWp4Ii
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzA5NzczMTl9LCJBN3
MwUng3Sm1XWXlrVzg2Ijp7ImRpc2N1c3Npb25JZCI6IkhocDBa
eENrR255NXlFdEEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3
MDk5NDg4NX0sIkFLVXBxcHF1YWM0VmoxbnAiOnsiZGlzY3Vzc2
lvbklkIjoiWTdtMTlyZWt0enF4ZHVCZCIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIG
ZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMDcyNjU0
fSwidDVqOVNvTFhDVmRiMjdENSI6eyJkaXNjdXNzaW9uSWQiOi
JXTlFRTTFSTGdyZmtacTM5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cn
VjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzEwODEyOTZ9LCJ6elV5
NUFqUnBWR3NEZ0pZIjp7ImRpc2N1c3Npb25JZCI6ImlqcXZ0OX
BLWHp0dEt6NlciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJGaWd1cmUgb3V0IHdoYXQgdG8gZG8gd2l0aCB0aGVzZSIsIm
NyZWF0ZWQiOjE2ODcxNzExOTY4Mzh9LCJUdk5Oc0tmREtPM2Zr
VHBlIjp7ImRpc2N1c3Npb25JZCI6IndQdkFqekpNa3podzg5dH
AiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0
IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZC
I6MTY4NzE3MTI0NzAzMn0sIjBFd3BOam5nR1kwSTYyRUMiOnsi
ZGlzY3Vzc2lvbklkIjoiWmtVdnc4N3dqUjhEY3FCTyIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzE3MTI5ODM3NX0sIkFLRTRZRTdvN09ZZj
ZkRjMiOnsiZGlzY3Vzc2lvbklkIjoiTWVvekRTcWs5OU5ia0hh
UiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBjb3
Vyc2Ugc3RydWN0dXJlIHRvIiwiY3JlYXRlZCI6MTY4NzE3MTQy
NTI1NX0sIkNFcUsxVHA0SkVRYUFXT2QiOnsiZGlzY3Vzc2lvbk
lkIjoiQXZGOWpwcUM3U2lYSGtKOCIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MT
Y4NzE3MTQ1MjcyN30sIjY5VURYMHlWV0FBSW9tYTUiOnsiZGlz
Y3Vzc2lvbklkIjoialB6cEZaVU5IcVZVT3N5ciIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMg
YW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNT
IwNDU2fSwibXM3UmNkM1Nsb2ZJUWxkYyI6eyJkaXNjdXNzaW9u
SWQiOiJCNUtsWmhveTN4a2Z3cVBBIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjox
Njg3MTcxNTI5ODQ3fSwiV2xaY3E2N212TDQyWklTcCI6eyJkaX
NjdXNzaW9uSWQiOiJrUVJ2UVoyZjlid1pxazJ2Iiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUy
IsImNyZWF0ZWQiOjE2ODcxNzE1NTIzMDN9LCJkWndOWnF6ZG41
UFBWRUdaIjp7ImRpc2N1c3Npb25JZCI6InI1MExoT2JOV1BHNm
Q2dWYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3Jy
ZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MTU3NTcwNH
0sImRSOEd4TjJFYVlaNHBiaE8iOnsiZGlzY3Vzc2lvbklkIjoi
MFlrM0JoVzN3d2FIRGFpZSIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIHdyaXRlIG91
dCBpbiBtb3JlIGRldGFpbCIsImNyZWF0ZWQiOjE2ODcxNzE2MT
kzMjh9LCJ1d3pHSkhLd2FWREE4Q2gxIjp7ImRpc2N1c3Npb25J
ZCI6IjJqSjhDVzA4eWwxQ3k1WEUiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzE2Mzg5Mjh9LCJWejFmUWFLRnNhSXRXRE9jIjp7ImRpc2
N1c3Npb25JZCI6Ik1JRjE4NndaNXhuZHpYNTUiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIG
FuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTY3
NzA3MX0sIkZ1SWljWkd6djF2WkZxalgiOnsiZGlzY3Vzc2lvbk
lkIjoidWhoVGJFTHF5UjB2c00xTyIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MT
Y4NzE3MTcwNTM2MH0sInlnVE40c005bmxnNHg3Q3oiOnsiZGlz
Y3Vzc2lvbklkIjoiazFqRVlRMWtaYTY1YmJNMCIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMs
IHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVyZSIsIm
NyZWF0ZWQiOjE2ODcxNzE3NDExNTl9LCJoaGt4VkJraG9pczJm
MjFkIjp7ImRpc2N1c3Npb25JZCI6IjJabDhDcUpBRXdxS3hEdl
QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3NTY1NDR9LCJSRW1tQm
5xU2RSMWdySG9PIjp7ImRpc2N1c3Npb25JZCI6IkFqZWJHZHYy
RG1SckU2RXAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JDb3JyZWN0IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5k
IGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNzk1MT
A0fSwiVDJTMGZZUk9MaVFBVWhjeSI6eyJkaXNjdXNzaW9uSWQi
OiJNSzQ2ekRmT1R2NG9lcTZiIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3
MTcxODMwMzU5fSwiNXJVTGtmY3FmcDAzSkhLUyI6eyJkaXNjdX
NzaW9uSWQiOiJTQzV3OTZiWDZpU3JxRm9DIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUywgd3
JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MTg1MzcxMn0sIklDUnFUanFzT3NTVXU5b0
8iOnsiZGlzY3Vzc2lvbklkIjoicTFpVjZiR3A1ZjRyZkZ3USIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dX
JlIiwiY3JlYXRlZCI6MTY4NzE3MTg2NjEyOH19LCJoaXN0b3J5
IjpbLTEwOTgxNTQ2NzAsLTg5MTU5OTIzM119
-->