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

4. Before we can use the DEM, we need to fill its sinks
	- Open the *Fill sinks (Wang & Liu)* tool (Remember where we search for all our tools?)
	- Choose the clipped DEM as the DEM, leave the rest as default
	- Run the tool, you can remove the flow directions and watershed basins outputs, save the Filled DEM
		- The output of this will be the DEM we will be using from now on! 
	- As you can see by the icon next to the filled DEM, there is no CRS associated with it, give it the same CRS as the original DEM

5. One of the important features of DEM is that it can be used to create a hillshade relief. Hillshade is mostly used in visualization to create an imposing 3D-effect of the surface. Let's create a hillshade using this DEM. 
	- Open the *Hillshade* tool 
	- Choose the filled DEM as the Elevation layer
	- Try out how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.
	- Choose settings that you think are good and make that layer permanent, you can remove your test layers

*Tip: Again, name the files! Good name for the first Hillshade could be for example “HillShade_Muurla_def” or “HS_Muurla_def” indicating that it’s a hillshade, study area and default settings – for the next one you could change the name to for example “HS_Muurla_Az180” and so on, based on the chosen settings.*

6. Another very useful feature of a DEM is the possibility to identify the gradient of the raster surface. 
	- Open the *Slope* tool
	- Use the filled DEM again, you can use the default settings 
	- Remember to make your layer permanent again

**Answer the following questions on Moodle:**
- What do the hill shade parameters azimuth and altitude mean?
- What is the maximum slope of the study area based on the DEM10m_Muurla?
- How about the mean slope of the study area based on the DEM10m_Muurla?

*Hint: Layer Properties contain information about the layers, including some statistics)*

#### 1.2: Data type conversions - feature to raster
It is quite common in GIS that data has to be converted from one type to another; some analyses for instance require a certain file type to work. In part two of this exercise you are going to need the shapefile “Muurla_Soil.shp” as a raster file to be able to perform the raster overlay analyses.

7. Let's convert the Muurla_Soil.shp to a raster file
	- Open the *Rasterize (Vector to Raster)* tool
	- Use the Muurla_soil layer as the input
	- Since rasters can’t have multiple attributes like shapefiles we need to select which field to use, column “PINTA” has the information which we want to use for the analysis, so this is the column you should select for “Field to use for a burn-in value” -parameter. 
	- Set the size units to Georeferenced units, and the resolution to the same as the resolution of the DEM 
	- Run the tool
	- Don't forget to make your layer permanent

- Figure

---

### 2: Modelling optimal cultivation areas

Southwest Finland is sometimes called as the bread-basket of Finland that refers to its plentiful fields and agricultural productivity. In this exercise your task is to model optimal cultivation areas using raster data analyses in Muurla, which is a district of Salo, a city between Turku and Helsinki.

The aim is to classify the study area based on its suitability for cultivation. The criteria are the following:

- Good or moderate soil
- Slope < 15°
- Minimum distance of 10m from the bodies of water
- The soil factor is twice as important as the slope factor

In the earlier phase you already clipped the DEM, filled the DEM, calculated the slope and made the feature to raster conversion for the soil so some phases are already done. The following flow chart shows the different stages of the optimal cultivation areas analysis.

- Figure

#### 2.1: Defining the unsuitable areas

8. Start off with the water criteria. Go to Buffer -tool and make a 10-meter buffer for the Bodies_of_Water -layer without dissolving. (Hint: Exercise 4)

9. Next, you have to convert the newly created buffer zone -layer to raster format. As learned before in this practical, use the *Rasterize (Vector to Raster)* tool to make this rasterization. Choose “Pinta” as the field to assign the values to the output raster and check that the cell size matches DEM.

10.  For further calcuations we need to reclassify the data of the water buffer raster layer.
	- Open the *Reclassify by table* tool
	- Add the reclassification table as pictured below
	- Set the ouput no data value to 1, no data in this case means land
		- What do you think the 1 and 0 values represent in this analysis?
	- Run the tool, save the output

- Figure

11. Let’s continue with defining the unsuitable areas by determining the “bad slopes”. 
	- Use the Reclassify -tool again, choose this time the slope raster as the input
	- Add the reclassification table as pictured below
		- Hint about earlier question: 1 = suitable, 0 = unsuitable
	- Run the tool, save the output

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
QiOjE0NTksInRleHQiOiJNb29kbGUifSwiWmtVdnc4N3dqUjhE
Y3FCTyI6eyJzdGFydCI6NTg4OCwiZW5kIjo1ODk0LCJ0ZXh0Ij
oiRmlndXJlIn0sIk1lb3pEU3FrOTlOYmtIYVIiOnsic3RhcnQi
Ojk3OCwiZW5kIjoxMDIzLCJ0ZXh0IjoiIyMjIFBhcnQgMTogR2
V0dGluZyBmYW1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sIkF2
RjlqcHFDN1NpWEhrSjgiOnsic3RhcnQiOjY3ODUsImVuZCI6Nj
c5MSwidGV4dCI6IkZpZ3VyZSJ9LCIyako4Q1cwOHlsMUN5NVhF
Ijp7InN0YXJ0Ijo3NjU0LCJlbmQiOjc2NjAsInRleHQiOiJGaW
d1cmUifSwiTUlGMTg2d1o1eG5kelg1NSI6eyJzdGFydCI6NzY2
MiwiZW5kIjo3NjYzLCJ0ZXh0IjoiMTEifSwidWhoVGJFTHF5Uj
B2c00xTyI6eyJzdGFydCI6ODEyOSwiZW5kIjo4MTM1LCJ0ZXh0
IjoiRmlndXJlIn0sImsxakVZUTFrWmE2NWJiTTAiOnsic3Rhcn
QiOjgxMzcsImVuZCI6ODEzOCwidGV4dCI6IjEyIn0sIjJabDhD
cUpBRXdxS3hEdlQiOnsic3RhcnQiOjg0ODUsImVuZCI6ODQ5MS
widGV4dCI6IkZpZ3VyZSJ9LCJBamViR2R2MkRtUnJFNkVwIjp7
InN0YXJ0Ijo4NTMyLCJlbmQiOjg1MzMsInRleHQiOiIxMyJ9LC
JNSzQ2ekRmT1R2NG9lcTZiIjp7InN0YXJ0Ijo5MDAxLCJlbmQi
OjkwMDksInRleHQiOiItIEZpZ3VyZSJ9LCJTQzV3OTZiWDZpU3
JxRm9DIjp7InN0YXJ0Ijo5MDExLCJlbmQiOjkwMTIsInRleHQi
OiIxNCJ9LCJxMWlWNmJHcDVmNHJmRndRIjp7InN0YXJ0Ijo5MT
UwLCJlbmQiOjkxNTYsInRleHQiOiJGaWd1cmUifSwiN3BtTUdO
U29vUHozSmd3RCI6eyJzdGFydCI6OTY1NSwiZW5kIjo5NjU2LC
J0ZXh0IjoiMTUifSwiekJNWTBrcEZpczBuWjZqYSI6eyJzdGFy
dCI6OTgyOCwiZW5kIjo5ODI5LCJ0ZXh0IjoiMTYifSwiY2dXdE
FVdHdwWEI5VU1WZiI6eyJzdGFydCI6OTgyMCwiZW5kIjo5ODI2
LCJ0ZXh0IjoiRmlndXJlIn0sIjM0ZXFzck9yaGpqT003T0MiOn
sic3RhcnQiOjEwMTA3LCJlbmQiOjEwMTE1LCJ0ZXh0IjoiLSBG
aWd1cmUifSwiVlcyQm1CbTZmZGNyWFpmZCI6eyJzdGFydCI6MT
AxMTcsImVuZCI6MTAxMTgsInRleHQiOiIxNyJ9LCJTQm9uc2JO
aFNMd0RoZ0JiIjp7InN0YXJ0Ijo1NzEsImVuZCI6NTgzLCJ0ZX
h0IjoiIyMgREFUQSBVU0VEIn0sIk1CclN1Z0lRQUo0MXBrSFci
Onsic3RhcnQiOjc0LCJlbmQiOjk1LCJ0ZXh0IjoiIyMgT1ZFUl
ZJRVcgJiBQVVJQT1NFIn0sIjZLSlhuS2NwYXBRZnlEUU8iOnsi
c3RhcnQiOjQ2MDksImVuZCI6NDY1MCwidGV4dCI6IkFuc3dlci
B0aGUgZm9sbG93aW5nIHF1ZXN0aW9ucyBvbiBNb29kbGU6In0s
Ik9HTlBKMGh1OWhSUUU5aVYiOnsic3RhcnQiOjI5NDgsImVuZC
I6Mjk2MiwidGV4dCI6ImZpbGwgaXRzIHNpbmtzIn0sIlVKd2ls
eDl4bkZIWFBwdTAiOnsic3RhcnQiOjMzMTMsImVuZCI6MzMxNy
widGV4dCI6Imljb24ifX0sImNvbW1lbnRzIjp7IkdiTG9wVjRi
NVBXcERPaVQiOnsiZGlzY3Vzc2lvbklkIjoiNzZaVTFLQlZGNT
NCTzQzdCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlJl
d3JpdGUiLCJjcmVhdGVkIjoxNjg3MTcwNzgxODQ3fSwibXY5aT
JmSG9MV1lhSVU4YSI6eyJkaXNjdXNzaW9uSWQiOiJINnp5OTZR
Slh5Nk1McFJtIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcwODM1Mjcw
fSwicVVpd1NqRUxUaDd0aUs1NSI6eyJkaXNjdXNzaW9uSWQiOi
IyckpGU0FRSlV2WXIwRndXIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiRml4IHJlZmVyZW5jZSIsImNyZWF0ZWQiOjE2OD
cxNzA4ODg3NzR9LCIwRXdwTmpuZ0dZMEk2MkVDIjp7ImRpc2N1
c3Npb25JZCI6IlprVXZ3ODd3alI4RGNxQk8iLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0
ZWQiOjE2ODcxNzEyOTgzNzV9LCJBS0U0WUU3bzdPWWY2ZEYzIj
p7ImRpc2N1c3Npb25JZCI6Ik1lb3pEU3FrOTlOYmtIYVIiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggY291cnNlIH
N0cnVjdHVyZSB0byIsImNyZWF0ZWQiOjE2ODcxNzE0MjUyNTV9
LCJDRXFLMVRwNEpFUWFBV09kIjp7ImRpc2N1c3Npb25JZCI6Ik
F2RjlqcHFDN1NpWEhrSjgiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNz
E0NTI3Mjd9LCJ1d3pHSkhLd2FWREE4Q2gxIjp7ImRpc2N1c3Np
b25JZCI6IjJqSjhDVzA4eWwxQ3k1WEUiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQi
OjE2ODcxNzE2Mzg5Mjh9LCJWejFmUWFLRnNhSXRXRE9jIjp7Im
Rpc2N1c3Npb25JZCI6Ik1JRjE4NndaNXhuZHpYNTUiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0
lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3
MTY3NzA3MX0sIkZ1SWljWkd6djF2WkZxalgiOnsiZGlzY3Vzc2
lvbklkIjoidWhoVGJFTHF5UjB2c00xTyIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZC
I6MTY4NzE3MTcwNTM2MH0sInlnVE40c005bmxnNHg3Q3oiOnsi
ZGlzY3Vzc2lvbklkIjoiazFqRVlRMWtaYTY1YmJNMCIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFH
SVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVyZS
IsImNyZWF0ZWQiOjE2ODcxNzE3NDExNTl9LCJoaGt4VkJraG9p
czJmMjFkIjp7ImRpc2N1c3Npb25JZCI6IjJabDhDcUpBRXdxS3
hEdlQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
cGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3NTY1NDR9LCJSRW
1tQm5xU2RSMWdySG9PIjp7ImRpc2N1c3Npb25JZCI6IkFqZWJH
ZHYyRG1SckU2RXAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDb3JyZWN0IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwg
YW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNz
k1MTA0fSwiVDJTMGZZUk9MaVFBVWhjeSI6eyJkaXNjdXNzaW9u
SWQiOiJNSzQ2ekRmT1R2NG9lcTZiIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjox
Njg3MTcxODMwMzU5fSwiNXJVTGtmY3FmcDAzSkhLUyI6eyJkaX
NjdXNzaW9uSWQiOiJTQzV3OTZiWDZpU3JxRm9DIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUy
wgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzE3MTg1MzcxMn0sIklDUnFUanFzT3NTVX
U5b08iOnsiZGlzY3Vzc2lvbklkIjoicTFpVjZiR3A1ZjRyZkZ3
USIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaW
N0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTg2NjEyOH0sInhUY0Z1
OGZMajhzMXNmZFMiOnsiZGlzY3Vzc2lvbklkIjoiN3BtTUdOU2
9vUHozSmd3RCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkZpeCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaX
ggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTk0OTI2NX0s
Ijhod3RndUtJWEZxUTg1eW0iOnsiZGlzY3Vzc2lvbklkIjoiek
JNWTBrcEZpczBuWjZqYSIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkZpeCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIG
FuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTk3
MzQ4MX0sIldhZDN5OHpFcDZyZHhGdnEiOnsiZGlzY3Vzc2lvbk
lkIjoiY2dXdEFVdHdwWEI5VU1WZiIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MT
Y4NzE3MTk4NDQyNX0sImNZUjhGQWUxNEhnV3d1eTIiOnsiZGlz
Y3Vzc2lvbklkIjoiMzRlcXNyT3JoampPTTdPQyIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MjAwODEyOH0sImhFektacFVhNXFaSzM3Uk
UiOnsiZGlzY3Vzc2lvbklkIjoiVlcyQm1CbTZmZGNyWFpmZCIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUU
dJUyIsImNyZWF0ZWQiOjE2ODcxNzIwNDI5NjB9LCJvVFh6N3I2
MXIySEhkcnRqIjp7ImRpc2N1c3Npb25JZCI6IlNCb25zYk5oU0
x3RGhnQmIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQiLCJjcmVhdGVkIjoxNjg3MTcyMjAxNTM1fSwiVUYzNFRZeG
dZdlIweTFTUiI6eyJkaXNjdXNzaW9uSWQiOiJNQnJTdWdJUUFK
NDFwa0hXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIiwiY3JlYXRlZCI6MTY4NzE3MjIwNTQ4Nn0sIm9VREJRM2t6
M0g5YmhPMG0iOnsiZGlzY3Vzc2lvbklkIjoiNktKWG5LY3BhcF
FmeURRTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFk
ZCBzZWN0aW9uIGluIG1vb2RsZSB3aGVyZSBwZW9wbGUgY2FuIG
ZpbGwgdGhlc2UgaW4iLCJjcmVhdGVkIjoxNjg3MjM5NDEzMDUy
fSwiRXpncXozS29tdExnWWNaQyI6eyJkaXNjdXNzaW9uSWQiOi
JPR05QSjBodTloUlFFOWlWIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiV2hhdD8iLCJjcmVhdGVkIjoxNjg3MjQzNjcxMD
M1fSwiQWEwSmFmMGhVRktJMFd5aCI6eyJkaXNjdXNzaW9uSWQi
OiJVSndpbHg5eG5GSFhQcHUwIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3
MjQzODk1ODk5fX0sImhpc3RvcnkiOlstNDEzMjY0NjgxLDE1OD
IyNzk3MDcsLTg4NzIyNDU2MCwyODE5MDc0MSwtMjEwODEwNDg0
OCwyODQ1MjMwODYsODQwMTU0MzksLTg5MTU5OTIzM119
-->