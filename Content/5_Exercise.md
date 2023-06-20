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
- 

5. One of the important features of DEM is that it can be used to create a hillshade relief. Hillshade is mostly used in visualization to create an imposing 3D-effect of the surface. Let's create a hillshade using this DEM. 
	- Open the *Hillshade* tool (Remember where we search for all our tools?)
	- Choose the clipped DEM as the Elevation layer
	- Try out how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.
	- Choose settings that you think are good and make that layer permanent, you can remove your test layers

*Tip: Again, name the files! Good name for the first Hillshade could be for example “HillShade_Muurla_def” or “HS_Muurla_def” indicating that it’s a hillshade, study area and default settings – for the next one you could change the name to for example “HS_Muurla_Az180” and so on, based on the chosen settings.*

6. Another very useful feature of a DEM is the possibility to identify the gradient of the raster surface. 
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

In the earlier phase you already clipped the DEM, calculated the slope and made the feature to raster conversion for the soil so some phases are already done. The following flow chart shows the different stages of the optimal cultivation areas analysis.

- Figure

#### 2.1: Defining the unsuitable areas

7. Start off with the water criteria. Go to Buffer -tool and make a 10-meter buffer for the Bodies_of_Water -layer without dissolving. (Hint: Exercise 4)

8. Next, you have to convert the newly created buffer zone -layer to raster format. As learned before in this practical, use the *Rasterize (Vector to Raster)* tool to make this rasterization. Choose “Pinta” as the field to assign the values to the output raster and check that the cell size matches DEM.

9.  For further calcuations we need to reclassify the data of the water buffer raster layer.
	- Open the *Reclassify by table* tool
	- Add the reclassification table as pictured below
	- Set the ouput no data value to 1, no data in this case means land
		- What do you think the 1 and 0 values represent in this analysis?
	- Run the tool, save the output

- Figure

10. Let’s continue with defining the unsuitable areas by determining the “bad slopes”. 
	- Use the Reclassify -tool again, choose this time the slope raster as the input
	- Add the reclassification table as pictured below
		- Hint about earlier question: 1 = suitable, 0 = unsuitable
	- Run the tool, save the output

The “water buffer” and the “bad slopes” will be classified as “0” so that they can be removed from the calculations later on with multiplication.

- Figure

11. Now let’s combine the bad criteria layers with the Raster Calculator -tool which can be found under Map Algebra in Spatial Analyst Tools within Toolbox. Multiply the “Reclass_Water” with “BadSlope” layer in the calculator to create an “Unsuitable_areas”-layer. Always choose the layers and tools from the menus above to ensure correct form.

- Figure

#### 2.2: Defining the suitable areas

12. Now after you have identified the unsuitable areas, your next task it to rank the suitable ones. To make the “slope rank” go once again to Reclassify. Choose the original Slope_Muurla file as the input raster and open the classify window. Choose 4 classes and give the following break values 3, 7, 15, 54. Rank the classes as in the Figure 4 and name the file “slope_rank”.

Let’s move on to ranking the soil. You can see the explanation for the soil codes below.

- Figure

13. Open the Reclassify -tool and specify the values as in the Figure 5. The higher the value the better the soil fits for cultivation.

- Figure

***Note**: for simplicity, we did not identify an ‘unsuitable_soil’ layer but only the soil_rank, i.e. areas with soil type as rock will show a low suitability, but they will not be identified as completely unsuitable if they e.g. are located in a suitable slope pixel. This is ok for the purpose of the exercise, but it is good to keep it in mind. As an optional task, you can add them to unsuitable areas and make another analysis as well.*

#### 2.3: Identifying the final suitability ranking

14. In the last part we will use all the components created to get the suitability map. Use the raster calculator following the formula as shown in the Figure 6.

- Figure

15. Open once more Reclassify and select the suitable areas layer as the input. Reclassify the layer so to have 4 classes so that one represents unsuitable values (0) and others have interval of 1 (with rank values 0, 1, 2, 3, see Figure 7) and name the output as “Final_Rank”.

- Figure

16. Now, you should see the optimal cultivation areas in the study area. You can add a basemap from the ArcGIS server as in the exercise 2 and see whether your optimal areas match with the real fields located in the area.

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
Y3FCTyI6eyJzdGFydCI6NTQ4MiwiZW5kIjo1NDg4LCJ0ZXh0Ij
oiRmlndXJlIn0sIk1lb3pEU3FrOTlOYmtIYVIiOnsic3RhcnQi
Ojk3OCwiZW5kIjoxMDIzLCJ0ZXh0IjoiIyMjIFBhcnQgMTogR2
V0dGluZyBmYW1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sIkF2
RjlqcHFDN1NpWEhrSjgiOnsic3RhcnQiOjYzNjMsImVuZCI6Nj
M2OSwidGV4dCI6IkZpZ3VyZSJ9LCIyako4Q1cwOHlsMUN5NVhF
Ijp7InN0YXJ0Ijo3MjMxLCJlbmQiOjcyMzcsInRleHQiOiJGaW
d1cmUifSwiTUlGMTg2d1o1eG5kelg1NSI6eyJzdGFydCI6NzIz
OSwiZW5kIjo3MjQwLCJ0ZXh0IjoiMTEifSwidWhoVGJFTHF5Uj
B2c00xTyI6eyJzdGFydCI6NzcwNiwiZW5kIjo3NzEyLCJ0ZXh0
IjoiRmlndXJlIn0sImsxakVZUTFrWmE2NWJiTTAiOnsic3Rhcn
QiOjc3MTQsImVuZCI6NzcxNSwidGV4dCI6IjEyIn0sIjJabDhD
cUpBRXdxS3hEdlQiOnsic3RhcnQiOjgwNjIsImVuZCI6ODA2OC
widGV4dCI6IkZpZ3VyZSJ9LCJBamViR2R2MkRtUnJFNkVwIjp7
InN0YXJ0Ijo4MTA5LCJlbmQiOjgxMTAsInRleHQiOiIxMyJ9LC
JNSzQ2ekRmT1R2NG9lcTZiIjp7InN0YXJ0Ijo4NTc4LCJlbmQi
Ojg1ODYsInRleHQiOiItIEZpZ3VyZSJ9LCJTQzV3OTZiWDZpU3
JxRm9DIjp7InN0YXJ0Ijo4NTg4LCJlbmQiOjg1ODksInRleHQi
OiIxNCJ9LCJxMWlWNmJHcDVmNHJmRndRIjp7InN0YXJ0Ijo4Nz
I3LCJlbmQiOjg3MzMsInRleHQiOiJGaWd1cmUifSwiN3BtTUdO
U29vUHozSmd3RCI6eyJzdGFydCI6OTIzMiwiZW5kIjo5MjMzLC
J0ZXh0IjoiMTUifSwiekJNWTBrcEZpczBuWjZqYSI6eyJzdGFy
dCI6OTQwNSwiZW5kIjo5NDA2LCJ0ZXh0IjoiMTYifSwiY2dXdE
FVdHdwWEI5VU1WZiI6eyJzdGFydCI6OTM5NywiZW5kIjo5NDAz
LCJ0ZXh0IjoiRmlndXJlIn0sIjM0ZXFzck9yaGpqT003T0MiOn
sic3RhcnQiOjk2ODQsImVuZCI6OTY5MiwidGV4dCI6Ii0gRmln
dXJlIn0sIlZXMkJtQm02ZmRjclhaZmQiOnsic3RhcnQiOjk2OT
QsImVuZCI6OTY5NSwidGV4dCI6IjE3In0sIlNCb25zYk5oU0x3
RGhnQmIiOnsic3RhcnQiOjU3MSwiZW5kIjo1ODMsInRleHQiOi
IjIyBEQVRBIFVTRUQifSwiTUJyU3VnSVFBSjQxcGtIVyI6eyJz
dGFydCI6NzQsImVuZCI6OTUsInRleHQiOiIjIyBPVkVSVklFVy
AmIFBVUlBPU0UifSwiNktKWG5LY3BhcFFmeURRTyI6eyJzdGFy
dCI6NDIwMywiZW5kIjo0MjQ0LCJ0ZXh0IjoiQW5zd2VyIHRoZS
Bmb2xsb3dpbmcgcXVlc3Rpb25zIG9uIE1vb2RsZToifSwiT0dO
UEowaHU5aFJRRTlpViI6eyJzdGFydCI6Mjk0OCwiZW5kIjoyOT
YyLCJ0ZXh0IjoiZmlsbCBpdHMgc2lua3MifX0sImNvbW1lbnRz
Ijp7IkdiTG9wVjRiNVBXcERPaVQiOnsiZGlzY3Vzc2lvbklkIj
oiNzZaVTFLQlZGNTNCTzQzdCIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IlJld3JpdGUiLCJjcmVhdGVkIjoxNjg3MTcwNz
gxODQ3fSwibXY5aTJmSG9MV1lhSVU4YSI6eyJkaXNjdXNzaW9u
SWQiOiJINnp5OTZRSlh5Nk1McFJtIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjox
Njg3MTcwODM1MjcwfSwicVVpd1NqRUxUaDd0aUs1NSI6eyJkaX
NjdXNzaW9uSWQiOiIyckpGU0FRSlV2WXIwRndXIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IHJlZmVyZW5jZSIsIm
NyZWF0ZWQiOjE2ODcxNzA4ODg3NzR9LCIwRXdwTmpuZ0dZMEk2
MkVDIjp7ImRpc2N1c3Npb25JZCI6IlprVXZ3ODd3alI4RGNxQk
8iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODcxNzEyOTgzNzV9LCJBS0U0WU
U3bzdPWWY2ZEYzIjp7ImRpc2N1c3Npb25JZCI6Ik1lb3pEU3Fr
OTlOYmtIYVIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JGaXggY291cnNlIHN0cnVjdHVyZSB0byIsImNyZWF0ZWQiOjE2
ODcxNzE0MjUyNTV9LCJDRXFLMVRwNEpFUWFBV09kIjp7ImRpc2
N1c3Npb25JZCI6IkF2RjlqcHFDN1NpWEhrSjgiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODcxNzE0NTI3Mjd9LCJ1d3pHSkhLd2FWREE4Q2gx
Ijp7ImRpc2N1c3Npb25JZCI6IjJqSjhDVzA4eWwxQ3k1WEUiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVy
ZSIsImNyZWF0ZWQiOjE2ODcxNzE2Mzg5Mjh9LCJWejFmUWFLRn
NhSXRXRE9jIjp7ImRpc2N1c3Npb25JZCI6Ik1JRjE4NndaNXhu
ZHpYNTUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3
JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MTY3NzA3MX0sIkZ1SWljWkd6djF2WkZxal
giOnsiZGlzY3Vzc2lvbklkIjoidWhoVGJFTHF5UjB2c00xTyIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dX
JlIiwiY3JlYXRlZCI6MTY4NzE3MTcwNTM2MH0sInlnVE40c005
bmxnNHg3Q3oiOnsiZGlzY3Vzc2lvbklkIjoiazFqRVlRMWtaYT
Y1YmJNMCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNv
cnJlY3QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZm
l4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3NDExNTl9
LCJoaGt4VkJraG9pczJmMjFkIjp7ImRpc2N1c3Npb25JZCI6Ij
JabDhDcUpBRXdxS3hEdlQiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNz
E3NTY1NDR9LCJSRW1tQm5xU2RSMWdySG9PIjp7ImRpc2N1c3Np
b25JZCI6IkFqZWJHZHYyRG1SckU2RXAiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTLCB3cml0
ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdG
VkIjoxNjg3MTcxNzk1MTA0fSwiVDJTMGZZUk9MaVFBVWhjeSI6
eyJkaXNjdXNzaW9uSWQiOiJNSzQ2ekRmT1R2NG9lcTZiIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg3MTcxODMwMzU5fSwiNXJVTGtmY3FmcD
AzSkhLUyI6eyJkaXNjdXNzaW9uSWQiOiJTQzV3OTZiWDZpU3Jx
Rm9DIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycm
VjdCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXgg
c3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTg1MzcxMn0sIk
lDUnFUanFzT3NTVXU5b08iOnsiZGlzY3Vzc2lvbklkIjoicTFp
VjZiR3A1ZjRyZkZ3USIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTg2
NjEyOH0sInhUY0Z1OGZMajhzMXNmZFMiOnsiZGlzY3Vzc2lvbk
lkIjoiN3BtTUdOU29vUHozSmd3RCIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJUywgd3JpdGUgb3V0IG
1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4
NzE3MTk0OTI2NX0sIjhod3RndUtJWEZxUTg1eW0iOnsiZGlzY3
Vzc2lvbklkIjoiekJNWTBrcEZpczBuWjZqYSIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJUywgd3JpdG
Ugb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRl
ZCI6MTY4NzE3MTk3MzQ4MX0sIldhZDN5OHpFcDZyZHhGdnEiOn
siZGlzY3Vzc2lvbklkIjoiY2dXdEFVdHdwWEI5VU1WZiIsInN1
YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIi
wiY3JlYXRlZCI6MTY4NzE3MTk4NDQyNX0sImNZUjhGQWUxNEhn
V3d1eTIiOnsiZGlzY3Vzc2lvbklkIjoiMzRlcXNyT3JoampPTT
dPQyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBw
aWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MjAwODEyOH0sImhFek
tacFVhNXFaSzM3UkUiOnsiZGlzY3Vzc2lvbklkIjoiVlcyQm1C
bTZmZGNyWFpmZCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkZpeCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzIwNDI5
NjB9LCJvVFh6N3I2MXIySEhkcnRqIjp7ImRpc2N1c3Npb25JZC
I6IlNCb25zYk5oU0x3RGhnQmIiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQiLCJjcmVhdGVkIjoxNjg3MTcyMjAxNT
M1fSwiVUYzNFRZeGdZdlIweTFTUiI6eyJkaXNjdXNzaW9uSWQi
OiJNQnJTdWdJUUFKNDFwa0hXIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIiwiY3JlYXRlZCI6MTY4NzE3MjIwNTQ4
Nn0sIm9VREJRM2t6M0g5YmhPMG0iOnsiZGlzY3Vzc2lvbklkIj
oiNktKWG5LY3BhcFFmeURRTyIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkFkZCBzZWN0aW9uIGluIG1vb2RsZSB3aGVyZS
BwZW9wbGUgY2FuIGZpbGwgdGhlc2UgaW4iLCJjcmVhdGVkIjox
Njg3MjM5NDEzMDUyfSwiRXpncXozS29tdExnWWNaQyI6eyJkaX
NjdXNzaW9uSWQiOiJPR05QSjBodTloUlFFOWlWIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiV2hhdD8iLCJjcmVhdGVkIj
oxNjg3MjQzNjcxMDM1fX0sImhpc3RvcnkiOlstMjUxNzE5OTIx
LDE1ODIyNzk3MDcsLTg4NzIyNDU2MCwyODE5MDc0MSwtMjEwOD
EwNDg0OCwyODQ1MjMwODYsODQwMTU0MzksLTg5MTU5OTIzM119

-->