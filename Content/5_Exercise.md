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

17. Now, you should see the optimal cultivation areas in the study area. You can add a basemap from the ArcGIS server as in the exercise 2 and see whether your optimal areas match with the real fields located in the area.

---

### Part 3: Map visualization time

For suitability analysis it’s common to make a map collection showing the criteria areas and the final suitability analysis map. Make a map collection with following rasters:

• Soil types
• Terrain (hill shade)
• Slopes with unsuitable gradient areas highlighted
• Water bodies (can be combined to terrain or slopes)
• Final suitability analysis map (final rank)

Visualize the rasters as desired. For this type of maps base maps are in general not used. Feel free to include any additional map visualizations.

Besides the map visualization we can also check the proportions of pixels belonging to different classifications from the layer’s attribute table. Open the attribute table and add the Count-value of each classification into the report. It can also be included in your map collection layout.

As your final task, write a short reflection on what was done and why and add it also to your report.

**Don’t forget to add map items for all maps.**

*Tip: Find inspiration for visualization by googling “suitability map cultivating”, “soil type map colors”, and so on.*

*Another tip: you can use one layout to create the map collection. This requires opening each map in it’s separate map-project. Google “multiple maps to a singly layout ArcGIS Pro” for extra tips.*
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
LCJ0ZXh0IjoiLSBGaWd1cmUifSwiVlcyQm1CbTZmZGNyWFpmZC
I6eyJzdGFydCI6OTA4OCwiZW5kIjo5MDkwLCJ0ZXh0IjoiMTci
fX0sImNvbW1lbnRzIjp7IkdiTG9wVjRiNVBXcERPaVQiOnsiZG
lzY3Vzc2lvbklkIjoiNzZaVTFLQlZGNTNCTzQzdCIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlJld3JpdGUiLCJjcmVhdG
VkIjoxNjg3MTcwNzgxODQ3fSwibXY5aTJmSG9MV1lhSVU4YSI6
eyJkaXNjdXNzaW9uSWQiOiJINnp5OTZRSlh5Nk1McFJtIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg3MTcwODM1MjcwfSwicVVpd1NqRUxUaD
d0aUs1NSI6eyJkaXNjdXNzaW9uSWQiOiIyckpGU0FRSlV2WXIw
RndXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IH
JlZmVyZW5jZSIsImNyZWF0ZWQiOjE2ODcxNzA4ODg3NzR9LCJQ
OWV4bVhLUGs2SVROaUx3Ijp7ImRpc2N1c3Npb25JZCI6IlJ0az
ByTlFCQnVGaHdCNUUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJXcml0ZSBvdXQgaW5zdHJ1Y3Rpb25zIiwiY3JlYXRlZC
I6MTY4NzE3MDk1MzU0M30sIlBUdFhiTmhvNzBRRDJ4OHgiOnsi
ZGlzY3Vzc2lvbklkIjoiWmUyUU9lWWJlZ3AzQXVqeCIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFH
SVMiLCJjcmVhdGVkIjoxNjg3MTcwOTc3MzE5fSwiQTdzMFJ4N0
ptV1l5a1c4NiI6eyJkaXNjdXNzaW9uSWQiOiJIaHAwWnhDa0du
eTV5RXRBIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ2
9ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzA5OTQ4
ODV9LCJBS1VwcXBxdWFjNFZqMW5wIjp7ImRpc2N1c3Npb25JZC
I6Ilk3bTE5cmVrdHpxeGR1QmQiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3
RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTA3MjY1NH0sInQ1
ajlTb0xYQ1ZkYjI3RDUiOnsiZGlzY3Vzc2lvbklkIjoiV05RUU
0xUkxncmZrWnEzOSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cm
UiLCJjcmVhdGVkIjoxNjg3MTcxMDgxMjk2fSwienpVeTVBalJw
VkdzRGdKWSI6eyJkaXNjdXNzaW9uSWQiOiJpanF2dDlwS1h6dH
RLejZXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRmln
dXJlIG91dCB3aGF0IHRvIGRvIHdpdGggdGhlc2UiLCJjcmVhdG
VkIjoxNjg3MTcxMTk2ODM4fSwiVHZOTnNLZkRLTzNma1RwZSI6
eyJkaXNjdXNzaW9uSWQiOiJ3UHZBanpKTWt6aHc4OXRwIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3Ig
UUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2OD
cxNzEyNDcwMzJ9LCIwRXdwTmpuZ0dZMEk2MkVDIjp7ImRpc2N1
c3Npb25JZCI6IlprVXZ3ODd3alI4RGNxQk8iLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0
ZWQiOjE2ODcxNzEyOTgzNzV9LCJBS0U0WUU3bzdPWWY2ZEYzIj
p7ImRpc2N1c3Npb25JZCI6Ik1lb3pEU3FrOTlOYmtIYVIiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggY291cnNlIH
N0cnVjdHVyZSB0byIsImNyZWF0ZWQiOjE2ODcxNzE0MjUyNTV9
LCJDRXFLMVRwNEpFUWFBV09kIjp7ImRpc2N1c3Npb25JZCI6Ik
F2RjlqcHFDN1NpWEhrSjgiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNz
E0NTI3Mjd9LCI2OVVEWDB5VldBQUlvbWE1Ijp7ImRpc2N1c3Np
b25JZCI6ImpQenBGWlVOSHFWVU9zeXIiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBm
aXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTUyMDQ1Nn
0sIm1zN1JjZDNTbG9mSVFsZGMiOnsiZGlzY3Vzc2lvbklkIjoi
QjVLbFpob3kzeGtmd3FQQSIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3
MTUyOTg0N30sIldsWmNxNjdtdkw0MlpJU3AiOnsiZGlzY3Vzc2
lvbklkIjoia1FSdlFaMmY5YndacWsydiIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcm
VhdGVkIjoxNjg3MTcxNTUyMzAzfSwiZFp3TlpxemRuNVBQVkVH
WiI6eyJkaXNjdXNzaW9uSWQiOiJyNTBMaE9iTldQRzZkNnVmIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzE1NzU3MDR9LCJkUj
hHeE4yRWFZWjRwYmhPIjp7ImRpc2N1c3Npb25JZCI6IjBZazNC
aFczd3dhSERhaWUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCB3cml0ZSBvdXQgaW4g
bW9yZSBkZXRhaWwiLCJjcmVhdGVkIjoxNjg3MTcxNjE5MzI4fS
widXd6R0pIS3dhVkRBOENoMSI6eyJkaXNjdXNzaW9uSWQiOiIy
ako4Q1cwOHlsMUN5NVhFIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcx
NjM4OTI4fSwiVnoxZlFhS0ZzYUl0V0RPYyI6eyJkaXNjdXNzaW
9uSWQiOiJNSUYxODZ3WjV4bmR6WDU1Iiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZm
l4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE2NzcwNzF9
LCJGdUlpY1pHenYxdlpGcWpYIjp7ImRpc2N1c3Npb25JZCI6In
VoaFRiRUxxeVIwdnNNMU8iLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNz
E3MDUzNjB9LCJ5Z1RONHNNOW5sZzR4N0N6Ijp7ImRpc2N1c3Np
b25JZCI6ImsxakVZUTFrWmE2NWJiTTAiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTLCB3cml0
ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdG
VkIjoxNjg3MTcxNzQxMTU5fSwiaGhreFZCa2hvaXMyZjIxZCI6
eyJkaXNjdXNzaW9uSWQiOiIyWmw4Q3FKQUV3cUt4RHZUIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg3MTcxNzU2NTQ0fSwiUkVtbUJucVNkUj
FnckhvTyI6eyJkaXNjdXNzaW9uSWQiOiJBamViR2R2MkRtUnJF
NkVwIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycm
VjdCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXgg
c3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc5NTEwNH0sIl
QyUzBmWVJPTGlRQVVoY3kiOnsiZGlzY3Vzc2lvbklkIjoiTUs0
NnpEZk9UdjRvZXE2YiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTgz
MDM1OX0sIjVyVUxrZmNxZnAwM0pIS1MiOnsiZGlzY3Vzc2lvbk
lkIjoiU0M1dzk2Ylg2aVNycUZvQyIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMsIHdyaXRlIG
91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQi
OjE2ODcxNzE4NTM3MTJ9LCJJQ1JxVGpxc09zU1V1OW9PIjp7Im
Rpc2N1c3Npb25JZCI6InExaVY2YkdwNWY0cmZGd1EiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsIm
NyZWF0ZWQiOjE2ODcxNzE4NjYxMjh9LCJ4VGNGdThmTGo4czFz
ZmRTIjp7ImRpc2N1c3Npb25JZCI6IjdwbU1HTlNvb1B6M0pnd0
QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggZm9y
IFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdH
VyZSIsImNyZWF0ZWQiOjE2ODcxNzE5NDkyNjV9LCI4aHd0Z3VL
SVhGcVE4NXltIjp7ImRpc2N1c3Npb25JZCI6InpCTVkwa3BGaX
Mwblo2amEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJG
aXggZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IH
N0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE5NzM0ODF9LCJX
YWQzeTh6RXA2cmR4RnZxIjp7ImRpc2N1c3Npb25JZCI6ImNnV3
RBVXR3cFhCOVVNVmYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE5OD
Q0MjV9LCJjWVI4RkFlMTRIZ1d3dXkyIjp7ImRpc2N1c3Npb25J
ZCI6IjM0ZXFzck9yaGpqT003T0MiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzIwMDgxMjh9LCJoRXpLWnBVYTVxWkszN1JFIjp7ImRpc2
N1c3Npb25JZCI6IlZXMkJtQm02ZmRjclhaZmQiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJGaXggZm9yIFFHSVMiLCJjcm
VhdGVkIjoxNjg3MTcyMDQyOTYwfX0sImhpc3RvcnkiOlstODQ0
NzMyNjY3LC04OTE1OTkyMzNdfQ==
-->