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

1. Start the exercise by downloading the data “Exercise7.zip” from the course portal in Moodle, saving it in a folder for this exercise, and adding the data to your project.

2. You have to download the Digital Elevation Model (DEM) from PaITuli. 
	- Open the following link: https://paituli.csc.fi/download.html
	- Select the following settings:
		- Producer: National Land Survey of Finland
		- Data: Elevation Model
		- Scale: 10 m x 10 m
	- Type "L3343" in the search bar
	- Download as zip file

3. Add the Digital Elevation Model you downloaded from PaITuli to QGIS (What type of data is this? How do you add that?).
	-  The program will probably ask whether you want to add pyramids – in this case just press yes. 
	- The DEM is a large raster image file and thus rather heavy to process. To make the program run smoother, clip the DEM to a smaller extent. Study area for the practical is the same as Muurla_Frame -layer, use it for the clipping extent.

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
d0I1RSI6eyJzdGFydCI6MTU0MCwiZW5kIjoxNTQxLCJ0ZXh0Ij
oiMiJ9LCJaZTJRT2VZYmVncDNBdWp4Ijp7InN0YXJ0IjoxNjc3
LCJlbmQiOjE2MTMsInRleHQiOiIzIn0sIkhocDBaeENrR255NX
lFdEEiOnsic3RhcnQiOjIzMjgsImVuZCI6MjMzMSwidGV4dCI6
IlRpcCJ9LCJZN20xOXJla3R6cXhkdUJkIjp7InN0YXJ0IjoyNT
M4LCJlbmQiOjI1MzksInRleHQiOiI0In0sIldOUVFNMVJMZ3Jm
a1pxMzkiOnsic3RhcnQiOjM0MTksImVuZCI6MzQyMCwidGV4dC
I6IjUifSwiaWpxdnQ5cEtYenR0S3o2VyI6eyJzdGFydCI6Mzcy
NCwiZW5kIjozNzM0LCJ0ZXh0IjoiUXVlc3Rpb25zOiJ9LCJ3UH
ZBanpKTWt6aHc4OXRwIjp7InN0YXJ0Ijo0Mjk2LCJlbmQiOjQy
OTcsInRleHQiOiI2In0sIlprVXZ3ODd3alI4RGNxQk8iOnsic3
RhcnQiOjQ3MDEsImVuZCI6NDcwNywidGV4dCI6IkZpZ3VyZSJ9
LCJNZW96RFNxazk5TmJrSGFSIjp7InN0YXJ0Ijo5NzgsImVuZC
I6MTAyMywidGV4dCI6IiMjIyBQYXJ0IDE6IEdldHRpbmcgZmFt
aWxpYXIgd2l0aCByYXN0ZXIgZGF0YSJ9LCJBdkY5anBxQzdTaV
hIa0o4Ijp7InN0YXJ0Ijo1NTgyLCJlbmQiOjU1ODgsInRleHQi
OiJGaWd1cmUifSwialB6cEZaVU5IcVZVT3N5ciI6eyJzdGFydC
I6NTYzMCwiZW5kIjo1NjMxLCJ0ZXh0IjoiNyJ9LCJCNUtsWmhv
eTN4a2Z3cVBBIjp7InN0YXJ0Ijo1OTc5LCJlbmQiOjU5ODUsIn
RleHQiOiJGaWd1cmUifSwia1FSdlFaMmY5YndacWsydiI6eyJz
dGFydCI6NTk4NywiZW5kIjo1OTg4LCJ0ZXh0IjoiOCJ9LCJyNT
BMaE9iTldQRzZkNnVmIjp7InN0YXJ0Ijo2MTIzLCJlbmQiOjYx
MjQsInRleHQiOiI5In0sIjBZazNCaFczd3dhSERhaWUiOnsic3
RhcnQiOjY0MTUsImVuZCI6NjQxNywidGV4dCI6IjEwIn0sIjJq
SjhDVzA4eWwxQ3k1WEUiOnsic3RhcnQiOjY2ODcsImVuZCI6Nj
Y5MywidGV4dCI6IkZpZ3VyZSJ9LCJNSUYxODZ3WjV4bmR6WDU1
Ijp7InN0YXJ0Ijo2Njk1LCJlbmQiOjY2OTcsInRleHQiOiIxMS
J9LCJ1aGhUYkVMcXlSMHZzTTFPIjp7InN0YXJ0Ijo3MjgwLCJl
bmQiOjcyODYsInRleHQiOiJGaWd1cmUifSwiazFqRVlRMWtaYT
Y1YmJNMCI6eyJzdGFydCI6NzI4OCwiZW5kIjo3MjkwLCJ0ZXh0
IjoiMTIifSwiMlpsOENxSkFFd3FLeER2VCI6eyJzdGFydCI6Nz
YzNiwiZW5kIjo3NjQyLCJ0ZXh0IjoiRmlndXJlIn0sIkFqZWJH
ZHYyRG1SckU2RXAiOnsic3RhcnQiOjc2ODMsImVuZCI6NzY4NS
widGV4dCI6IjEzIn0sIk1LNDZ6RGZPVHY0b2VxNmIiOnsic3Rh
cnQiOjgxNTIsImVuZCI6ODE2MCwidGV4dCI6Ii0gRmlndXJlIn
0sIlNDNXc5NmJYNmlTcnFGb0MiOnsic3RhcnQiOjgxNjIsImVu
ZCI6ODE2NCwidGV4dCI6IjE0In0sInExaVY2YkdwNWY0cmZGd1
EiOnsic3RhcnQiOjgzMDEsImVuZCI6ODMwNywidGV4dCI6IkZp
Z3VyZSJ9LCI3cG1NR05Tb29QejNKZ3dEIjp7InN0YXJ0Ijo4OD
A2LCJlbmQiOjg4MDgsInRleHQiOiIxNSJ9LCJ6Qk1ZMGtwRmlz
MG5aNmphIjp7InN0YXJ0Ijo4OTc5LCJlbmQiOjg5ODAsInRleH
QiOiIxNiJ9LCJjZ1d0QVV0d3BYQjlVTVZmIjp7InN0YXJ0Ijo4
OTcxLCJlbmQiOjg5NzcsInRleHQiOiJGaWd1cmUifSwiMzRlcX
NyT3JoampPTTdPQyI6eyJzdGFydCI6OTI1OCwiZW5kIjo5MjY2
LCJ0ZXh0IjoiLSBGaWd1cmUifSwiVlcyQm1CbTZmZGNyWFpmZC
I6eyJzdGFydCI6OTI2OCwiZW5kIjo5MjcwLCJ0ZXh0IjoiMTci
fSwiU0JvbnNiTmhTTHdEaGdCYiI6eyJzdGFydCI6NTcxLCJlbm
QiOjU4MywidGV4dCI6IiMjIERBVEEgVVNFRCJ9LCJNQnJTdWdJ
UUFKNDFwa0hXIjp7InN0YXJ0Ijo3NCwiZW5kIjo5NSwidGV4dC
I6IiMjIE9WRVJWSUVXICYgUFVSUE9TRSJ9fSwiY29tbWVudHMi
OnsiR2JMb3BWNGI1UFdwRE9pVCI6eyJkaXNjdXNzaW9uSWQiOi
I3NlpVMUtCVkY1M0JPNDN0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiUmV3cml0ZSIsImNyZWF0ZWQiOjE2ODcxNzA3OD
E4NDd9LCJtdjlpMmZIb0xXWWFJVThhIjp7ImRpc2N1c3Npb25J
ZCI6Ikg2enk5NlFKWHk2TUxwUm0iLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzA4MzUyNzB9LCJxVWl3U2pFTFRoN3RpSzU1Ijp7ImRpc2
N1c3Npb25JZCI6IjJySkZTQVFKVXZZcjBGd1ciLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVmZXJlbmNlIiwiY3
JlYXRlZCI6MTY4NzE3MDg4ODc3NH0sIlA5ZXhtWEtQazZJVE5p
THciOnsiZGlzY3Vzc2lvbklkIjoiUnRrMHJOUUJCdUZod0I1RS
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IldyaXRlIG91
dCBpbnN0cnVjdGlvbnMiLCJjcmVhdGVkIjoxNjg3MTcwOTUzNT
QzfSwiUFR0WGJOaG83MFFEMng4eCI6eyJkaXNjdXNzaW9uSWQi
OiJaZTJRT2VZYmVncDNBdWp4Iiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQi
OjE2ODcxNzA5NzczMTl9LCJBN3MwUng3Sm1XWXlrVzg2Ijp7Im
Rpc2N1c3Npb25JZCI6IkhocDBaeENrR255NXlFdEEiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0
lTIiwiY3JlYXRlZCI6MTY4NzE3MDk5NDg4NX0sIkFLVXBxcHF1
YWM0VmoxbnAiOnsiZGlzY3Vzc2lvbklkIjoiWTdtMTlyZWt0en
F4ZHVCZCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNv
cnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcm
VhdGVkIjoxNjg3MTcxMDcyNjU0fSwidDVqOVNvTFhDVmRiMjdE
NSI6eyJkaXNjdXNzaW9uSWQiOiJXTlFRTTFSTGdyZmtacTM5Ii
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOj
E2ODcxNzEwODEyOTZ9LCJ6elV5NUFqUnBWR3NEZ0pZIjp7ImRp
c2N1c3Npb25JZCI6ImlqcXZ0OXBLWHp0dEt6NlciLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJGaWd1cmUgb3V0IHdoYXQg
dG8gZG8gd2l0aCB0aGVzZSIsImNyZWF0ZWQiOjE2ODcxNzExOT
Y4Mzh9LCJUdk5Oc0tmREtPM2ZrVHBlIjp7ImRpc2N1c3Npb25J
ZCI6IndQdkFqekpNa3podzg5dHAiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXgg
c3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI0NzAzMn0sIj
BFd3BOam5nR1kwSTYyRUMiOnsiZGlzY3Vzc2lvbklkIjoiWmtV
dnc4N3dqUjhEY3FCTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI5
ODM3NX0sIkFLRTRZRTdvN09ZZjZkRjMiOnsiZGlzY3Vzc2lvbk
lkIjoiTWVvekRTcWs5OU5ia0hhUiIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkZpeCBjb3Vyc2Ugc3RydWN0dXJlIHRvIi
wiY3JlYXRlZCI6MTY4NzE3MTQyNTI1NX0sIkNFcUsxVHA0SkVR
YUFXT2QiOnsiZGlzY3Vzc2lvbklkIjoiQXZGOWpwcUM3U2lYSG
tKOCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBw
aWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTQ1MjcyN30sIjY5VU
RYMHlWV0FBSW9tYTUiOnsiZGlzY3Vzc2lvbklkIjoialB6cEZa
VU5IcVZVT3N5ciIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUi
LCJjcmVhdGVkIjoxNjg3MTcxNTIwNDU2fSwibXM3UmNkM1Nsb2
ZJUWxkYyI6eyJkaXNjdXNzaW9uSWQiOiJCNUtsWmhveTN4a2Z3
cVBBIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIH
BpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNTI5ODQ3fSwiV2xa
Y3E2N212TDQyWklTcCI6eyJkaXNjdXNzaW9uSWQiOiJrUVJ2UV
oyZjlid1pxazJ2Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNz
E1NTIzMDN9LCJkWndOWnF6ZG41UFBWRUdaIjp7ImRpc2N1c3Np
b25JZCI6InI1MExoT2JOV1BHNmQ2dWYiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3Jl
YXRlZCI6MTY4NzE3MTU3NTcwNH0sImRSOEd4TjJFYVlaNHBiaE
8iOnsiZGlzY3Vzc2lvbklkIjoiMFlrM0JoVzN3d2FIRGFpZSIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm
9yIFFHSVMgYW5kIHdyaXRlIG91dCBpbiBtb3JlIGRldGFpbCIs
ImNyZWF0ZWQiOjE2ODcxNzE2MTkzMjh9LCJ1d3pHSkhLd2FWRE
E4Q2gxIjp7ImRpc2N1c3Npb25JZCI6IjJqSjhDVzA4eWwxQ3k1
WEUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcG
ljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE2Mzg5Mjh9LCJWejFm
UWFLRnNhSXRXRE9jIjp7ImRpc2N1c3Npb25JZCI6Ik1JRjE4Nn
daNXhuZHpYNTUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIi
wiY3JlYXRlZCI6MTY4NzE3MTY3NzA3MX0sIkZ1SWljWkd6djF2
WkZxalgiOnsiZGlzY3Vzc2lvbklkIjoidWhoVGJFTHF5UjB2c0
0xTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBw
aWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTcwNTM2MH0sInlnVE
40c005bmxnNHg3Q3oiOnsiZGlzY3Vzc2lvbklkIjoiazFqRVlR
MWtaYTY1YmJNMCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkNvcnJlY3QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBh
bmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3ND
ExNTl9LCJoaGt4VkJraG9pczJmMjFkIjp7ImRpc2N1c3Npb25J
ZCI6IjJabDhDcUpBRXdxS3hEdlQiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzE3NTY1NDR9LCJSRW1tQm5xU2RSMWdySG9PIjp7ImRpc2
N1c3Npb25JZCI6IkFqZWJHZHYyRG1SckU2RXAiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTLC
B3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJj
cmVhdGVkIjoxNjg3MTcxNzk1MTA0fSwiVDJTMGZZUk9MaVFBVW
hjeSI6eyJkaXNjdXNzaW9uSWQiOiJNSzQ2ekRmT1R2NG9lcTZi
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3
R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxODMwMzU5fSwiNXJVTGtm
Y3FmcDAzSkhLUyI6eyJkaXNjdXNzaW9uSWQiOiJTQzV3OTZiWD
ZpU3JxRm9DIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
Q29ycmVjdCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZC
BmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTg1Mzcx
Mn0sIklDUnFUanFzT3NTVXU5b08iOnsiZGlzY3Vzc2lvbklkIj
oicTFpVjZiR3A1ZjRyZkZ3USIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Nz
E3MTg2NjEyOH0sInhUY0Z1OGZMajhzMXNmZFMiOnsiZGlzY3Vz
c2lvbklkIjoiN3BtTUdOU29vUHozSmd3RCIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJUywgd3JpdGUg
b3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZC
I6MTY4NzE3MTk0OTI2NX0sIjhod3RndUtJWEZxUTg1eW0iOnsi
ZGlzY3Vzc2lvbklkIjoiekJNWTBrcEZpczBuWjZqYSIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJUywg
d3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3
JlYXRlZCI6MTY4NzE3MTk3MzQ4MX0sIldhZDN5OHpFcDZyZHhG
dnEiOnsiZGlzY3Vzc2lvbklkIjoiY2dXdEFVdHdwWEI5VU1WZi
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0
dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTk4NDQyNX0sImNZUjhGQW
UxNEhnV3d1eTIiOnsiZGlzY3Vzc2lvbklkIjoiMzRlcXNyT3Jo
ampPTTdPQyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MjAwODEyOH0s
ImhFektacFVhNXFaSzM3UkUiOnsiZGlzY3Vzc2lvbklkIjoiVl
cyQm1CbTZmZGNyWFpmZCIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkZpeCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNz
IwNDI5NjB9LCJvVFh6N3I2MXIySEhkcnRqIjp7ImRpc2N1c3Np
b25JZCI6IlNCb25zYk5oU0x3RGhnQmIiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQiLCJjcmVhdGVkIjoxNjg3MTcy
MjAxNTM1fSwiVUYzNFRZeGdZdlIweTFTUiI6eyJkaXNjdXNzaW
9uSWQiOiJNQnJTdWdJUUFKNDFwa0hXIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQWRkIiwiY3JlYXRlZCI6MTY4NzE3Mj
IwNTQ4Nn19LCJoaXN0b3J5IjpbNzk0MDEwNDgxLDI4NDUyMzA4
Niw4NDAxNTQzOSwtODkxNTk5MjMzXX0=
-->