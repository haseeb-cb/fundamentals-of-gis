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
widGV4dCI6IjEzIn19LCJjb21tZW50cyI6eyJHYkxvcFY0YjVQ
V3BET2lUIjp7ImRpc2N1c3Npb25JZCI6Ijc2WlUxS0JWRjUzQk
80M3QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJSZXdy
aXRlIiwiY3JlYXRlZCI6MTY4NzE3MDc4MTg0N30sIm12OWkyZk
hvTFdZYUlVOGEiOnsiZGlzY3Vzc2lvbklkIjoiSDZ6eTk2UUpY
eTZNTHBSbSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MDgzNTI3MH0s
InFVaXdTakVMVGg3dGlLNTUiOnsiZGlzY3Vzc2lvbklkIjoiMn
JKRlNBUUpVdllyMEZ3VyIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkZpeCByZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3MT
cwODg4Nzc0fSwiUDlleG1YS1BrNklUTmlMdyI6eyJkaXNjdXNz
aW9uSWQiOiJSdGswck5RQkJ1Rmh3QjVFIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiV3JpdGUgb3V0IGluc3RydWN0aW9u
cyIsImNyZWF0ZWQiOjE2ODcxNzA5NTM1NDN9LCJQVHRYYk5obz
cwUUQyeDh4Ijp7ImRpc2N1c3Npb25JZCI6IlplMlFPZVliZWdw
M0F1angiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3
JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MDk3NzMx
OX0sIkE3czBSeDdKbVdZeWtXODYiOnsiZGlzY3Vzc2lvbklkIj
oiSGhwMFp4Q2tHbnk1eUV0QSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIj
oxNjg3MTcwOTk0ODg1fSwiQUtVcHFwcXVhYzRWajFucCI6eyJk
aXNjdXNzaW9uSWQiOiJZN20xOXJla3R6cXhkdUJkIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJ
UyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNz
EwNzI2NTR9LCJ0NWo5U29MWENWZGIyN0Q1Ijp7ImRpc2N1c3Np
b25JZCI6IldOUVFNMVJMZ3Jma1pxMzkiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBm
aXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTA4MTI5Nn
0sInp6VXk1QWpScFZHc0RnSlkiOnsiZGlzY3Vzc2lvbklkIjoi
aWpxdnQ5cEtYenR0S3o2VyIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkZpZ3VyZSBvdXQgd2hhdCB0byBkbyB3aXRoIHRo
ZXNlIiwiY3JlYXRlZCI6MTY4NzE3MTE5NjgzOH0sIlR2Tk5zS2
ZES08zZmtUcGUiOnsiZGlzY3Vzc2lvbklkIjoid1B2QWp6Sk1r
emh3ODl0cCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
NvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJj
cmVhdGVkIjoxNjg3MTcxMjQ3MDMyfSwiMEV3cE5qbmdHWTBJNj
JFQyI6eyJkaXNjdXNzaW9uSWQiOiJaa1V2dzg3d2pSOERjcUJP
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3
R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMjk4Mzc1fSwiQUtFNFlF
N283T1lmNmRGMyI6eyJkaXNjdXNzaW9uSWQiOiJNZW96RFNxaz
k5TmJrSGFSIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
Rml4IGNvdXJzZSBzdHJ1Y3R1cmUgdG8iLCJjcmVhdGVkIjoxNj
g3MTcxNDI1MjU1fSwiQ0VxSzFUcDRKRVFhQVdPZCI6eyJkaXNj
dXNzaW9uSWQiOiJBdkY5anBxQzdTaVhIa0o4Iiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVh
dGVkIjoxNjg3MTcxNDUyNzI3fSwiNjlVRFgweVZXQUFJb21hNS
I6eyJkaXNjdXNzaW9uSWQiOiJqUHpwRlpVTkhxVlVPc3lyIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3
IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzE1MjA0NTZ9LCJtczdSY2QzU2xvZklRbGRjIjp7ImRpc2
N1c3Npb25JZCI6IkI1S2xaaG95M3hrZndxUEEiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODcxNzE1Mjk4NDd9LCJXbFpjcTY3bXZMNDJaSVNw
Ijp7ImRpc2N1c3Npb25JZCI6ImtRUnZRWjJmOWJ3WnFrMnYiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZv
ciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MTU1MjMwM30sImRad0
5acXpkbjVQUFZFR1oiOnsiZGlzY3Vzc2lvbklkIjoicjUwTGhP
Yk5XUEc2ZDZ1ZiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcx
NTc1NzA0fSwiZFI4R3hOMkVhWVo0cGJoTyI6eyJkaXNjdXNzaW
9uSWQiOiIwWWszQmhXM3d3YUhEYWllIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgd3
JpdGUgb3V0IGluIG1vcmUgZGV0YWlsIiwiY3JlYXRlZCI6MTY4
NzE3MTYxOTMyOH0sInV3ekdKSEt3YVZEQThDaDEiOnsiZGlzY3
Vzc2lvbklkIjoiMmpKOENXMDh5bDFDeTVYRSIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYX
RlZCI6MTY4NzE3MTYzODkyOH0sIlZ6MWZRYUtGc2FJdFdET2Mi
OnsiZGlzY3Vzc2lvbklkIjoiTUlGMTg2d1o1eG5kelg1NSIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9y
IFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNj
g3MTcxNjc3MDcxfSwiRnVJaWNaR3p2MXZaRnFqWCI6eyJkaXNj
dXNzaW9uSWQiOiJ1aGhUYkVMcXlSMHZzTTFPIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVh
dGVkIjoxNjg3MTcxNzA1MzYwfSwieWdUTjRzTTlubGc0eDdDei
I6eyJkaXNjdXNzaW9uSWQiOiJrMWpFWVExa1phNjViYk0wIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3
IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0
dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc0MTE1OX0sImhoa3hWQm
tob2lzMmYyMWQiOnsiZGlzY3Vzc2lvbklkIjoiMlpsOENxSkFF
d3FLeER2VCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc1NjU0NH0s
IlJFbW1CbnFTZFIxZ3JIb08iOnsiZGlzY3Vzc2lvbklkIjoiQW
plYkdkdjJEbVJyRTZFcCIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3
JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcx
NzE3OTUxMDR9fSwiaGlzdG9yeSI6Wy0xNzc3NTQ0Nzk1LC04OT
E1OTkyMzNdfQ==
-->