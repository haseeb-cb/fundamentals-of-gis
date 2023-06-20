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
	- The DEM is a large raster image file and thus rather heavy to process. To make the program run smoother, let's clip the DEM to a smaller extent (Remember what clipping is from the previous theory?). 
		- Our study area for this exercise is the same as the Muurla_Frame -layer, so we can use this it for the clipping extent.
		- Since we are clipping a raster, we need to use the *Clip raster by mask layer* tool, open this from the *Processing Toolbox*
		- Set the input layer to your DEM and the mask layer ot Muurla_Frame
		- Click run, make the temporary layer permanent by right-clicking the layer and *Export* > *Save as...* (Temporary raster layers don't have the "Make permanent" option)
		- You should now have the DEM only for the Muurla_Frame, you can remove the original full-size DEM 

*Reminder: Don't forget to give your files and layers informative names and save them in a folder for this exercise*

4. One of the important features of DEM is that it can be used to create a hillshade relief. Hillshade is mostly used in visualization to create an imposing 3D-effect of the surface. Let's create a hillshade using this DEM. 
	- Open the *Hillshade* tool (Remember where we search for all our tools?)
	- Choose the clipped DEM as the Elevation layer
	- Try out how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.
	- Choose settings that you think are good and make that layer permanent, you can remove your test layers

*Tip: Again, name the files! Good name for the first Hillshade could be for example “HillShade_Muurla_def” or “HS_Muurla_def” indicating that it’s a hillshade, study area and default settings – for the next one you could change the name to for example “HS_Muurla_Az180” and so on, based on the chosen settings.*

5. Another very useful feature of a DEM is the possibility to identify the gradient of the raster surface. 
	- Open the *Slope* tool
	- Use the clipped DEM again, you can use the default settings 
	- Remember to make your layer permanent again

**Answer the following questions on Moodle:**
- What do the hill shade parameters azimuth and altitude mean?
- What is the maximum slope of the study area based on the DEM10m_Muurla?
- How about the mean slope of the study area based on the DEM10m_Muurla?

*Hint: Layer Properties contain information about the layers, including some statistics)*

#### 1.2: Data type conversions - feature to raster
It is quite common in GIS that data has to be converted from one type to another; some analyses for instance require a certain file type to work. In part two of this exercise you are going to need the shapefile “Muurla_Soil.shp” as a raster file to be able to perform the raster overlay analyses.

6. Let's convert the Muurla_Soil.shp to a raster file
So, without further ado, navigate to Conversion Tools -> To Raster and select Feature to Raster, as you are rasterizing a shapefile. Raster can’t have multiple attributes like shapefiles do. Column “PINTA” has the information which we want to use for the analysis, so this is the column you should select for “Field” -parameter. Name the file and choose the same cell size as you chose for the DEM.

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
QiOjE0NTksInRleHQiOiJNb29kbGUifSwid1B2QWp6Sk1remh3
ODl0cCI6eyJzdGFydCI6NDgzOSwiZW5kIjo0ODQwLCJ0ZXh0Ij
oiNiJ9LCJaa1V2dzg3d2pSOERjcUJPIjp7InN0YXJ0Ijo1Mjk1
LCJlbmQiOjUzMDEsInRleHQiOiJGaWd1cmUifSwiTWVvekRTcW
s5OU5ia0hhUiI6eyJzdGFydCI6OTc4LCJlbmQiOjEwMjMsInRl
eHQiOiIjIyMgUGFydCAxOiBHZXR0aW5nIGZhbWlsaWFyIHdpdG
ggcmFzdGVyIGRhdGEifSwiQXZGOWpwcUM3U2lYSGtKOCI6eyJz
dGFydCI6NjE3NiwiZW5kIjo2MTgyLCJ0ZXh0IjoiRmlndXJlIn
0sImpQenBGWlVOSHFWVU9zeXIiOnsic3RhcnQiOjYyMjQsImVu
ZCI6NjIyNSwidGV4dCI6IjcifSwiQjVLbFpob3kzeGtmd3FQQS
I6eyJzdGFydCI6NjU3MywiZW5kIjo2NTc5LCJ0ZXh0IjoiRmln
dXJlIn0sImtRUnZRWjJmOWJ3WnFrMnYiOnsic3RhcnQiOjY1OD
EsImVuZCI6NjU4MiwidGV4dCI6IjgifSwicjUwTGhPYk5XUEc2
ZDZ1ZiI6eyJzdGFydCI6NjcxNywiZW5kIjo2NzE4LCJ0ZXh0Ij
oiOSJ9LCIwWWszQmhXM3d3YUhEYWllIjp7InN0YXJ0Ijo3MDA5
LCJlbmQiOjcwMTEsInRleHQiOiIxMCJ9LCIyako4Q1cwOHlsMU
N5NVhFIjp7InN0YXJ0Ijo3MjgxLCJlbmQiOjcyODcsInRleHQi
OiJGaWd1cmUifSwiTUlGMTg2d1o1eG5kelg1NSI6eyJzdGFydC
I6NzI4OSwiZW5kIjo3MjkxLCJ0ZXh0IjoiMTEifSwidWhoVGJF
THF5UjB2c00xTyI6eyJzdGFydCI6Nzg3NCwiZW5kIjo3ODgwLC
J0ZXh0IjoiRmlndXJlIn0sImsxakVZUTFrWmE2NWJiTTAiOnsi
c3RhcnQiOjc4ODIsImVuZCI6Nzg4NCwidGV4dCI6IjEyIn0sIj
JabDhDcUpBRXdxS3hEdlQiOnsic3RhcnQiOjgyMzAsImVuZCI6
ODIzNiwidGV4dCI6IkZpZ3VyZSJ9LCJBamViR2R2MkRtUnJFNk
VwIjp7InN0YXJ0Ijo4Mjc3LCJlbmQiOjgyNzksInRleHQiOiIx
MyJ9LCJNSzQ2ekRmT1R2NG9lcTZiIjp7InN0YXJ0Ijo4NzQ2LC
JlbmQiOjg3NTQsInRleHQiOiItIEZpZ3VyZSJ9LCJTQzV3OTZi
WDZpU3JxRm9DIjp7InN0YXJ0Ijo4NzU2LCJlbmQiOjg3NTgsIn
RleHQiOiIxNCJ9LCJxMWlWNmJHcDVmNHJmRndRIjp7InN0YXJ0
Ijo4ODk1LCJlbmQiOjg5MDEsInRleHQiOiJGaWd1cmUifSwiN3
BtTUdOU29vUHozSmd3RCI6eyJzdGFydCI6OTQwMCwiZW5kIjo5
NDAyLCJ0ZXh0IjoiMTUifSwiekJNWTBrcEZpczBuWjZqYSI6ey
JzdGFydCI6OTU3MywiZW5kIjo5NTc0LCJ0ZXh0IjoiMTYifSwi
Y2dXdEFVdHdwWEI5VU1WZiI6eyJzdGFydCI6OTU2NSwiZW5kIj
o5NTcxLCJ0ZXh0IjoiRmlndXJlIn0sIjM0ZXFzck9yaGpqT003
T0MiOnsic3RhcnQiOjk4NTIsImVuZCI6OTg2MCwidGV4dCI6Ii
0gRmlndXJlIn0sIlZXMkJtQm02ZmRjclhaZmQiOnsic3RhcnQi
Ojk4NjIsImVuZCI6OTg2NCwidGV4dCI6IjE3In0sIlNCb25zYk
5oU0x3RGhnQmIiOnsic3RhcnQiOjU3MSwiZW5kIjo1ODMsInRl
eHQiOiIjIyBEQVRBIFVTRUQifSwiTUJyU3VnSVFBSjQxcGtIVy
I6eyJzdGFydCI6NzQsImVuZCI6OTUsInRleHQiOiIjIyBPVkVS
VklFVyAmIFBVUlBPU0UifSwiNktKWG5LY3BhcFFmeURRTyI6ey
JzdGFydCI6NDE0MywiZW5kIjo0MTg0LCJ0ZXh0IjoiQW5zd2Vy
IHRoZSBmb2xsb3dpbmcgcXVlc3Rpb25zIG9uIE1vb2RsZToifX
0sImNvbW1lbnRzIjp7IkdiTG9wVjRiNVBXcERPaVQiOnsiZGlz
Y3Vzc2lvbklkIjoiNzZaVTFLQlZGNTNCTzQzdCIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IlJld3JpdGUiLCJjcmVhdGVk
IjoxNjg3MTcwNzgxODQ3fSwibXY5aTJmSG9MV1lhSVU4YSI6ey
JkaXNjdXNzaW9uSWQiOiJINnp5OTZRSlh5Nk1McFJtIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLC
JjcmVhdGVkIjoxNjg3MTcwODM1MjcwfSwicVVpd1NqRUxUaDd0
aUs1NSI6eyJkaXNjdXNzaW9uSWQiOiIyckpGU0FRSlV2WXIwRn
dXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IHJl
ZmVyZW5jZSIsImNyZWF0ZWQiOjE2ODcxNzA4ODg3NzR9LCJUdk
5Oc0tmREtPM2ZrVHBlIjp7ImRpc2N1c3Npb25JZCI6IndQdkFq
ekpNa3podzg5dHAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJl
IiwiY3JlYXRlZCI6MTY4NzE3MTI0NzAzMn0sIjBFd3BOam5nR1
kwSTYyRUMiOnsiZGlzY3Vzc2lvbklkIjoiWmtVdnc4N3dqUjhE
Y3FCTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI5ODM3NX0sIkFL
RTRZRTdvN09ZZjZkRjMiOnsiZGlzY3Vzc2lvbklkIjoiTWVvek
RTcWs5OU5ia0hhUiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkZpeCBjb3Vyc2Ugc3RydWN0dXJlIHRvIiwiY3JlYXRlZC
I6MTY4NzE3MTQyNTI1NX0sIkNFcUsxVHA0SkVRYUFXT2QiOnsi
ZGlzY3Vzc2lvbklkIjoiQXZGOWpwcUM3U2lYSGtKOCIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzE3MTQ1MjcyN30sIjY5VURYMHlWV0FBSW
9tYTUiOnsiZGlzY3Vzc2lvbklkIjoialB6cEZaVU5IcVZVT3N5
ciIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3
QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVk
IjoxNjg3MTcxNTIwNDU2fSwibXM3UmNkM1Nsb2ZJUWxkYyI6ey
JkaXNjdXNzaW9uSWQiOiJCNUtsWmhveTN4a2Z3cVBBIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLC
JjcmVhdGVkIjoxNjg3MTcxNTI5ODQ3fSwiV2xaY3E2N212TDQy
WklTcCI6eyJkaXNjdXNzaW9uSWQiOiJrUVJ2UVoyZjlid1pxaz
J2Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVj
dCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzE1NTIzMDN9LC
JkWndOWnF6ZG41UFBWRUdaIjp7ImRpc2N1c3Npb25JZCI6InI1
MExoT2JOV1BHNmQ2dWYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4
NzE3MTU3NTcwNH0sImRSOEd4TjJFYVlaNHBiaE8iOnsiZGlzY3
Vzc2lvbklkIjoiMFlrM0JoVzN3d2FIRGFpZSIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW
5kIHdyaXRlIG91dCBpbiBtb3JlIGRldGFpbCIsImNyZWF0ZWQi
OjE2ODcxNzE2MTkzMjh9LCJ1d3pHSkhLd2FWREE4Q2gxIjp7Im
Rpc2N1c3Npb25JZCI6IjJqSjhDVzA4eWwxQ3k1WEUiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsIm
NyZWF0ZWQiOjE2ODcxNzE2Mzg5Mjh9LCJWejFmUWFLRnNhSXRX
RE9jIjp7ImRpc2N1c3Npb25JZCI6Ik1JRjE4NndaNXhuZHpYNT
UiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0
IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZC
I6MTY4NzE3MTY3NzA3MX0sIkZ1SWljWkd6djF2WkZxalgiOnsi
ZGlzY3Vzc2lvbklkIjoidWhoVGJFTHF5UjB2c00xTyIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzE3MTcwNTM2MH0sInlnVE40c005bmxnNH
g3Q3oiOnsiZGlzY3Vzc2lvbklkIjoiazFqRVlRMWtaYTY1YmJN
MCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3
QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0
cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3NDExNTl9LCJoaG
t4VkJraG9pczJmMjFkIjp7ImRpc2N1c3Npb25JZCI6IjJabDhD
cUpBRXdxS3hEdlQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3NTY1
NDR9LCJSRW1tQm5xU2RSMWdySG9PIjp7ImRpc2N1c3Npb25JZC
I6IkFqZWJHZHYyRG1SckU2RXAiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTLCB3cml0ZSBvdX
QgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjox
Njg3MTcxNzk1MTA0fSwiVDJTMGZZUk9MaVFBVWhjeSI6eyJkaX
NjdXNzaW9uSWQiOiJNSzQ2ekRmT1R2NG9lcTZiIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcm
VhdGVkIjoxNjg3MTcxODMwMzU5fSwiNXJVTGtmY3FmcDAzSkhL
UyI6eyJkaXNjdXNzaW9uSWQiOiJTQzV3OTZiWDZpU3JxRm9DIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydW
N0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTg1MzcxMn0sIklDUnFU
anFzT3NTVXU5b08iOnsiZGlzY3Vzc2lvbklkIjoicTFpVjZiR3
A1ZjRyZkZ3USIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTg2NjEyOH
0sInhUY0Z1OGZMajhzMXNmZFMiOnsiZGlzY3Vzc2lvbklkIjoi
N3BtTUdOU29vUHozSmd3RCIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkZpeCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUs
IGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MT
k0OTI2NX0sIjhod3RndUtJWEZxUTg1eW0iOnsiZGlzY3Vzc2lv
bklkIjoiekJNWTBrcEZpczBuWjZqYSIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJUywgd3JpdGUgb3V0
IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MT
Y4NzE3MTk3MzQ4MX0sIldhZDN5OHpFcDZyZHhGdnEiOnsiZGlz
Y3Vzc2lvbklkIjoiY2dXdEFVdHdwWEI5VU1WZiIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MTk4NDQyNX0sImNZUjhGQWUxNEhnV3d1eT
IiOnsiZGlzY3Vzc2lvbklkIjoiMzRlcXNyT3JoampPTTdPQyIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dX
JlIiwiY3JlYXRlZCI6MTY4NzE3MjAwODEyOH0sImhFektacFVh
NXFaSzM3UkUiOnsiZGlzY3Vzc2lvbklkIjoiVlcyQm1CbTZmZG
NyWFpmZCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZp
eCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzIwNDI5NjB9LC
JvVFh6N3I2MXIySEhkcnRqIjp7ImRpc2N1c3Npb25JZCI6IlNC
b25zYk5oU0x3RGhnQmIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQiLCJjcmVhdGVkIjoxNjg3MTcyMjAxNTM1fSwi
VUYzNFRZeGdZdlIweTFTUiI6eyJkaXNjdXNzaW9uSWQiOiJNQn
JTdWdJUUFKNDFwa0hXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQWRkIiwiY3JlYXRlZCI6MTY4NzE3MjIwNTQ4Nn0sIm
9VREJRM2t6M0g5YmhPMG0iOnsiZGlzY3Vzc2lvbklkIjoiNktK
WG5LY3BhcFFmeURRTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBzZWN0aW9uIGluIG1vb2RsZSB3aGVyZSBwZW9w
bGUgY2FuIGZpbGwgdGhlc2UgaW4iLCJjcmVhdGVkIjoxNjg3Mj
M5NDEzMDUyfX0sImhpc3RvcnkiOlsxMzk3NDk4NTk3LDI4NDUy
MzA4Niw4NDAxNTQzOSwtODkxNTk5MjMzXX0=
-->