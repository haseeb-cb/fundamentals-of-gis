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

9.  Open the . In order for the further calculations to succeed, you have to make the NoData acceptable because those areas are the ones without water. Make the changes as below and save the file as “reclass_water”.

- Figure

10. Let’s continue with defining the unsuitable areas by determining the “bad slopes”. Use the Reclassify -tool again, choose this time the slope raster as the input and press the classify button. In the new window choose reduce the number of classes to 2 and set the upper break values on the right manually as 15 and 54. Return to the first page by pressing OK and fill in the rest of the form using the image below as your support.

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
Y3FCTyI6eyJzdGFydCI6NTQyMiwiZW5kIjo1NDI4LCJ0ZXh0Ij
oiRmlndXJlIn0sIk1lb3pEU3FrOTlOYmtIYVIiOnsic3RhcnQi
Ojk3OCwiZW5kIjoxMDIzLCJ0ZXh0IjoiIyMjIFBhcnQgMTogR2
V0dGluZyBmYW1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sIkF2
RjlqcHFDN1NpWEhrSjgiOnsic3RhcnQiOjYzMDMsImVuZCI6Nj
MwOSwidGV4dCI6IkZpZ3VyZSJ9LCIwWWszQmhXM3d3YUhEYWll
Ijp7InN0YXJ0Ijo2ODE0LCJlbmQiOjY4MTQsInRleHQiOiIxMC
J9LCIyako4Q1cwOHlsMUN5NVhFIjp7InN0YXJ0Ijo3MDMyLCJl
bmQiOjcwMzgsInRleHQiOiJGaWd1cmUifSwiTUlGMTg2d1o1eG
5kelg1NSI6eyJzdGFydCI6NzA0MCwiZW5kIjo3MDQxLCJ0ZXh0
IjoiMTEifSwidWhoVGJFTHF5UjB2c00xTyI6eyJzdGFydCI6Nz
YyNSwiZW5kIjo3NjMxLCJ0ZXh0IjoiRmlndXJlIn0sImsxakVZ
UTFrWmE2NWJiTTAiOnsic3RhcnQiOjc2MzMsImVuZCI6NzYzNC
widGV4dCI6IjEyIn0sIjJabDhDcUpBRXdxS3hEdlQiOnsic3Rh
cnQiOjc5ODEsImVuZCI6Nzk4NywidGV4dCI6IkZpZ3VyZSJ9LC
JBamViR2R2MkRtUnJFNkVwIjp7InN0YXJ0Ijo4MDI4LCJlbmQi
OjgwMjksInRleHQiOiIxMyJ9LCJNSzQ2ekRmT1R2NG9lcTZiIj
p7InN0YXJ0Ijo4NDk3LCJlbmQiOjg1MDUsInRleHQiOiItIEZp
Z3VyZSJ9LCJTQzV3OTZiWDZpU3JxRm9DIjp7InN0YXJ0Ijo4NT
A3LCJlbmQiOjg1MDgsInRleHQiOiIxNCJ9LCJxMWlWNmJHcDVm
NHJmRndRIjp7InN0YXJ0Ijo4NjQ2LCJlbmQiOjg2NTIsInRleH
QiOiJGaWd1cmUifSwiN3BtTUdOU29vUHozSmd3RCI6eyJzdGFy
dCI6OTE1MSwiZW5kIjo5MTUyLCJ0ZXh0IjoiMTUifSwiekJNWT
BrcEZpczBuWjZqYSI6eyJzdGFydCI6OTMyNCwiZW5kIjo5MzI1
LCJ0ZXh0IjoiMTYifSwiY2dXdEFVdHdwWEI5VU1WZiI6eyJzdG
FydCI6OTMxNiwiZW5kIjo5MzIyLCJ0ZXh0IjoiRmlndXJlIn0s
IjM0ZXFzck9yaGpqT003T0MiOnsic3RhcnQiOjk2MDMsImVuZC
I6OTYxMSwidGV4dCI6Ii0gRmlndXJlIn0sIlZXMkJtQm02ZmRj
clhaZmQiOnsic3RhcnQiOjk2MTMsImVuZCI6OTYxNCwidGV4dC
I6IjE3In0sIlNCb25zYk5oU0x3RGhnQmIiOnsic3RhcnQiOjU3
MSwiZW5kIjo1ODMsInRleHQiOiIjIyBEQVRBIFVTRUQifSwiTU
JyU3VnSVFBSjQxcGtIVyI6eyJzdGFydCI6NzQsImVuZCI6OTUs
InRleHQiOiIjIyBPVkVSVklFVyAmIFBVUlBPU0UifSwiNktKWG
5LY3BhcFFmeURRTyI6eyJzdGFydCI6NDE0MywiZW5kIjo0MTg0
LCJ0ZXh0IjoiQW5zd2VyIHRoZSBmb2xsb3dpbmcgcXVlc3Rpb2
5zIG9uIE1vb2RsZToifX0sImNvbW1lbnRzIjp7IkdiTG9wVjRi
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
E0NTI3Mjd9LCJkUjhHeE4yRWFZWjRwYmhPIjp7ImRpc2N1c3Np
b25JZCI6IjBZazNCaFczd3dhSERhaWUiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCB3
cml0ZSBvdXQgaW4gbW9yZSBkZXRhaWwiLCJjcmVhdGVkIjoxNj
g3MTcxNjE5MzI4fSwidXd6R0pIS3dhVkRBOENoMSI6eyJkaXNj
dXNzaW9uSWQiOiIyako4Q1cwOHlsMUN5NVhFIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVh
dGVkIjoxNjg3MTcxNjM4OTI4fSwiVnoxZlFhS0ZzYUl0V0RPYy
I6eyJkaXNjdXNzaW9uSWQiOiJNSUYxODZ3WjV4bmR6WDU1Iiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3
IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzE2NzcwNzF9LCJGdUlpY1pHenYxdlpGcWpYIjp7ImRpc2
N1c3Npb25JZCI6InVoaFRiRUxxeVIwdnNNMU8iLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODcxNzE3MDUzNjB9LCJ5Z1RONHNNOW5sZzR4N0N6
Ijp7ImRpc2N1c3Npb25JZCI6ImsxakVZUTFrWmE2NWJiTTAiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZv
ciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3
R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNzQxMTU5fSwiaGhreFZC
a2hvaXMyZjIxZCI6eyJkaXNjdXNzaW9uSWQiOiIyWmw4Q3FKQU
V3cUt4RHZUIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNzU2NTQ0fS
wiUkVtbUJucVNkUjFnckhvTyI6eyJkaXNjdXNzaW9uSWQiOiJB
amViR2R2MkRtUnJFNkVwIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUywgd3JpdGUgb3V0IG1v
cmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4Nz
E3MTc5NTEwNH0sIlQyUzBmWVJPTGlRQVVoY3kiOnsiZGlzY3Vz
c2lvbklkIjoiTUs0NnpEZk9UdjRvZXE2YiIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRl
ZCI6MTY4NzE3MTgzMDM1OX0sIjVyVUxrZmNxZnAwM0pIS1MiOn
siZGlzY3Vzc2lvbklkIjoiU0M1dzk2Ylg2aVNycUZvQyIsInN1
YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIF
FHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVy
ZSIsImNyZWF0ZWQiOjE2ODcxNzE4NTM3MTJ9LCJJQ1JxVGpxc0
9zU1V1OW9PIjp7ImRpc2N1c3Npb25JZCI6InExaVY2YkdwNWY0
cmZGd1EiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZG
QgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE4NjYxMjh9LCJ4
VGNGdThmTGo4czFzZmRTIjp7ImRpc2N1c3Npb25JZCI6IjdwbU
1HTlNvb1B6M0pnd0QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJGaXggZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbm
QgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE5NDky
NjV9LCI4aHd0Z3VLSVhGcVE4NXltIjp7ImRpc2N1c3Npb25JZC
I6InpCTVkwa3BGaXMwblo2amEiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJGaXggZm9yIFFHSVMsIHdyaXRlIG91dCBtb3
JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcx
NzE5NzM0ODF9LCJXYWQzeTh6RXA2cmR4RnZxIjp7ImRpc2N1c3
Npb25JZCI6ImNnV3RBVXR3cFhCOVVNVmYiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZW
QiOjE2ODcxNzE5ODQ0MjV9LCJjWVI4RkFlMTRIZ1d3dXkyIjp7
ImRpc2N1c3Npb25JZCI6IjM0ZXFzck9yaGpqT003T0MiLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIs
ImNyZWF0ZWQiOjE2ODcxNzIwMDgxMjh9LCJoRXpLWnBVYTVxWk
szN1JFIjp7ImRpc2N1c3Npb25JZCI6IlZXMkJtQm02ZmRjclha
ZmQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggZm
9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcyMDQyOTYwfSwib1RY
ejdyNjFyMkhIZHJ0aiI6eyJkaXNjdXNzaW9uSWQiOiJTQm9uc2
JOaFNMd0RoZ0JiIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQWRkIiwiY3JlYXRlZCI6MTY4NzE3MjIwMTUzNX0sIlVGMz
RUWXhnWXZSMHkxU1IiOnsiZGlzY3Vzc2lvbklkIjoiTUJyU3Vn
SVFBSjQxcGtIVyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkFkZCIsImNyZWF0ZWQiOjE2ODcxNzIyMDU0ODZ9LCJvVURC
UTNrejNIOWJoTzBtIjp7ImRpc2N1c3Npb25JZCI6IjZLSlhuS2
NwYXBRZnlEUU8iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgc2VjdGlvbiBpbiBtb29kbGUgd2hlcmUgcGVvcGxlIG
NhbiBmaWxsIHRoZXNlIGluIiwiY3JlYXRlZCI6MTY4NzIzOTQx
MzA1Mn19LCJoaXN0b3J5IjpbMjEzOTEzNjczMSwtODg3MjI0NT
YwLDI4MTkwNzQxLC0yMTA4MTA0ODQ4LDI4NDUyMzA4Niw4NDAx
NTQzOSwtODkxNTk5MjMzXX0=
-->