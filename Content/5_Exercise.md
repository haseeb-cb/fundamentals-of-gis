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

#### 2.3: Identifying the final suitability ranking

15. In the last part we will use all the components created to get the suitability map. Use the raster calculator following the formula as shown in the Figure 6.

- Figure

16. Open once more Reclassify and select the suitable areas layer as the input. Reclassify the layer so to have 4 classes so that one represents unsuitable values (0) and others have interval of 1 (with rank values 0, 1, 2, 3, see Figure 7) and name the output as “Final_Rank”.

- Figure

17. 

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
Z3VyZSJ9LCI3cG1NR05Tb29QejNKZ3dEIjp7InN0YXJ0Ijo4Nj
I2LCJlbmQiOjg2MjgsInRleHQiOiIxNSJ9LCJ6Qk1ZMGtwRmlz
MG5aNmphIjp7InN0YXJ0Ijo4Nzk5LCJlbmQiOjg4MDAsInRleH
QiOiIxNiJ9LCJjZ1d0QVV0d3BYQjlVTVZmIjp7InN0YXJ0Ijo4
NzkxLCJlbmQiOjg3OTcsInRleHQiOiJGaWd1cmUifSwiMzRlcX
NyT3JoampPTTdPQyI6eyJzdGFydCI6OTA3OCwiZW5kIjo5MDg2
LCJ0ZXh0IjoiLSBGaWd1cmUifX0sImNvbW1lbnRzIjp7IkdiTG
9wVjRiNVBXcERPaVQiOnsiZGlzY3Vzc2lvbklkIjoiNzZaVTFL
QlZGNTNCTzQzdCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IlJld3JpdGUiLCJjcmVhdGVkIjoxNjg3MTcwNzgxODQ3fSwi
bXY5aTJmSG9MV1lhSVU4YSI6eyJkaXNjdXNzaW9uSWQiOiJINn
p5OTZRSlh5Nk1McFJtIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcwOD
M1MjcwfSwicVVpd1NqRUxUaDd0aUs1NSI6eyJkaXNjdXNzaW9u
SWQiOiIyckpGU0FRSlV2WXIwRndXIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiRml4IHJlZmVyZW5jZSIsImNyZWF0ZWQi
OjE2ODcxNzA4ODg3NzR9LCJQOWV4bVhLUGs2SVROaUx3Ijp7Im
Rpc2N1c3Npb25JZCI6IlJ0azByTlFCQnVGaHdCNUUiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJXcml0ZSBvdXQgaW5zdH
J1Y3Rpb25zIiwiY3JlYXRlZCI6MTY4NzE3MDk1MzU0M30sIlBU
dFhiTmhvNzBRRDJ4OHgiOnsiZGlzY3Vzc2lvbklkIjoiWmUyUU
9lWWJlZ3AzQXVqeCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MT
cwOTc3MzE5fSwiQTdzMFJ4N0ptV1l5a1c4NiI6eyJkaXNjdXNz
aW9uSWQiOiJIaHAwWnhDa0dueTV5RXRBIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNy
ZWF0ZWQiOjE2ODcxNzA5OTQ4ODV9LCJBS1VwcXBxdWFjNFZqMW
5wIjp7ImRpc2N1c3Npb25JZCI6Ilk3bTE5cmVrdHpxeGR1QmQi
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IG
ZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6
MTY4NzE3MTA3MjY1NH0sInQ1ajlTb0xYQ1ZkYjI3RDUiOnsiZG
lzY3Vzc2lvbklkIjoiV05RUU0xUkxncmZrWnEzOSIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSV
MgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcx
MDgxMjk2fSwienpVeTVBalJwVkdzRGdKWSI6eyJkaXNjdXNzaW
9uSWQiOiJpanF2dDlwS1h6dHRLejZXIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiRmlndXJlIG91dCB3aGF0IHRvIGRvIH
dpdGggdGhlc2UiLCJjcmVhdGVkIjoxNjg3MTcxMTk2ODM4fSwi
VHZOTnNLZkRLTzNma1RwZSI6eyJkaXNjdXNzaW9uSWQiOiJ3UH
ZBanpKTWt6aHc4OXRwIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdH
VyZSIsImNyZWF0ZWQiOjE2ODcxNzEyNDcwMzJ9LCIwRXdwTmpu
Z0dZMEk2MkVDIjp7ImRpc2N1c3Npb25JZCI6IlprVXZ3ODd3al
I4RGNxQk8iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzEyOTgzNzV9LC
JBS0U0WUU3bzdPWWY2ZEYzIjp7ImRpc2N1c3Npb25JZCI6Ik1l
b3pEU3FrOTlOYmtIYVIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJGaXggY291cnNlIHN0cnVjdHVyZSB0byIsImNyZWF0
ZWQiOjE2ODcxNzE0MjUyNTV9LCJDRXFLMVRwNEpFUWFBV09kIj
p7ImRpc2N1c3Npb25JZCI6IkF2RjlqcHFDN1NpWEhrSjgiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZS
IsImNyZWF0ZWQiOjE2ODcxNzE0NTI3Mjd9LCI2OVVEWDB5VldB
QUlvbWE1Ijp7ImRpc2N1c3Npb25JZCI6ImpQenBGWlVOSHFWVU
9zeXIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3Jy
ZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYX
RlZCI6MTY4NzE3MTUyMDQ1Nn0sIm1zN1JjZDNTbG9mSVFsZGMi
OnsiZGlzY3Vzc2lvbklkIjoiQjVLbFpob3kzeGtmd3FQQSIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJl
IiwiY3JlYXRlZCI6MTY4NzE3MTUyOTg0N30sIldsWmNxNjdtdk
w0MlpJU3AiOnsiZGlzY3Vzc2lvbklkIjoia1FSdlFaMmY5Ynda
cWsydiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcn
JlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcxNTUyMzAz
fSwiZFp3TlpxemRuNVBQVkVHWiI6eyJkaXNjdXNzaW9uSWQiOi
JyNTBMaE9iTldQRzZkNnVmIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOj
E2ODcxNzE1NzU3MDR9LCJkUjhHeE4yRWFZWjRwYmhPIjp7ImRp
c2N1c3Npb25JZCI6IjBZazNCaFczd3dhSERhaWUiLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lT
IGFuZCB3cml0ZSBvdXQgaW4gbW9yZSBkZXRhaWwiLCJjcmVhdG
VkIjoxNjg3MTcxNjE5MzI4fSwidXd6R0pIS3dhVkRBOENoMSI6
eyJkaXNjdXNzaW9uSWQiOiIyako4Q1cwOHlsMUN5NVhFIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg3MTcxNjM4OTI4fSwiVnoxZlFhS0ZzYU
l0V0RPYyI6eyJkaXNjdXNzaW9uSWQiOiJNSUYxODZ3WjV4bmR6
WDU1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycm
VjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0
ZWQiOjE2ODcxNzE2NzcwNzF9LCJGdUlpY1pHenYxdlpGcWpYIj
p7ImRpc2N1c3Npb25JZCI6InVoaFRiRUxxeVIwdnNNMU8iLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZS
IsImNyZWF0ZWQiOjE2ODcxNzE3MDUzNjB9LCJ5Z1RONHNNOW5s
ZzR4N0N6Ijp7ImRpc2N1c3Npb25JZCI6ImsxakVZUTFrWmE2NW
JiTTAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3Jy
ZWN0IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeC
BzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNzQxMTU5fSwi
aGhreFZCa2hvaXMyZjIxZCI6eyJkaXNjdXNzaW9uSWQiOiIyWm
w4Q3FKQUV3cUt4RHZUIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNz
U2NTQ0fSwiUkVtbUJucVNkUjFnckhvTyI6eyJkaXNjdXNzaW9u
SWQiOiJBamViR2R2MkRtUnJFNkVwIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUywgd3JpdGUg
b3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZC
I6MTY4NzE3MTc5NTEwNH0sIlQyUzBmWVJPTGlRQVVoY3kiOnsi
ZGlzY3Vzc2lvbklkIjoiTUs0NnpEZk9UdjRvZXE2YiIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzE3MTgzMDM1OX0sIjVyVUxrZmNxZnAwM0
pIS1MiOnsiZGlzY3Vzc2lvbklkIjoiU0M1dzk2Ylg2aVNycUZv
QyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3
QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0
cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE4NTM3MTJ9LCJJQ1
JxVGpxc09zU1V1OW9PIjp7ImRpc2N1c3Npb25JZCI6InExaVY2
YkdwNWY0cmZGd1EiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE4NjYx
Mjh9LCJ4VGNGdThmTGo4czFzZmRTIjp7ImRpc2N1c3Npb25JZC
I6IjdwbU1HTlNvb1B6M0pnd0QiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJGaXggZm9yIFFHSVMsIHdyaXRlIG91dCBtb3
JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcx
NzE5NDkyNjV9LCI4aHd0Z3VLSVhGcVE4NXltIjp7ImRpc2N1c3
Npb25JZCI6InpCTVkwa3BGaXMwblo2amEiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJGaXggZm9yIFFHSVMsIHdyaXRlIG
91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQi
OjE2ODcxNzE5NzM0ODF9LCJXYWQzeTh6RXA2cmR4RnZxIjp7Im
Rpc2N1c3Npb25JZCI6ImNnV3RBVXR3cFhCOVVNVmYiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsIm
NyZWF0ZWQiOjE2ODcxNzE5ODQ0MjV9LCJjWVI4RkFlMTRIZ1d3
dXkyIjp7ImRpc2N1c3Npb25JZCI6IjM0ZXFzck9yaGpqT003T0
MiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODcxNzIwMDgxMjh9fSwiaGlzdG
9yeSI6Wy0xODUwNjY3NTQ2LC04OTE1OTkyMzNdfQ==
-->