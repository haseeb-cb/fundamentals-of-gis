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
oiMiJ9LCJIaHAwWnhDa0dueTV5RXRBIjp7InN0YXJ0IjoyOTA3
LCJlbmQiOjI5MDYsInRleHQiOiJUaXAifSwiWTdtMTlyZWt0en
F4ZHVCZCI6eyJzdGFydCI6MjkwNywiZW5kIjoyOTA4LCJ0ZXh0
IjoiNCJ9LCJXTlFRTTFSTGdyZmtacTM5Ijp7InN0YXJ0IjozNz
g4LCJlbmQiOjM3ODksInRleHQiOiI1In0sImlqcXZ0OXBLWHp0
dEt6NlciOnsic3RhcnQiOjQwOTMsImVuZCI6NDEwMywidGV4dC
I6IlF1ZXN0aW9uczoifSwid1B2QWp6Sk1remh3ODl0cCI6eyJz
dGFydCI6NDY2NSwiZW5kIjo0NjY2LCJ0ZXh0IjoiNiJ9LCJaa1
V2dzg3d2pSOERjcUJPIjp7InN0YXJ0Ijo1MDcwLCJlbmQiOjUw
NzYsInRleHQiOiJGaWd1cmUifSwiTWVvekRTcWs5OU5ia0hhUi
I6eyJzdGFydCI6OTc4LCJlbmQiOjEwMjMsInRleHQiOiIjIyMg
UGFydCAxOiBHZXR0aW5nIGZhbWlsaWFyIHdpdGggcmFzdGVyIG
RhdGEifSwiQXZGOWpwcUM3U2lYSGtKOCI6eyJzdGFydCI6NTk1
MSwiZW5kIjo1OTU3LCJ0ZXh0IjoiRmlndXJlIn0sImpQenBGWl
VOSHFWVU9zeXIiOnsic3RhcnQiOjU5OTksImVuZCI6NjAwMCwi
dGV4dCI6IjcifSwiQjVLbFpob3kzeGtmd3FQQSI6eyJzdGFydC
I6NjM0OCwiZW5kIjo2MzU0LCJ0ZXh0IjoiRmlndXJlIn0sImtR
UnZRWjJmOWJ3WnFrMnYiOnsic3RhcnQiOjYzNTYsImVuZCI6Nj
M1NywidGV4dCI6IjgifSwicjUwTGhPYk5XUEc2ZDZ1ZiI6eyJz
dGFydCI6NjQ5MiwiZW5kIjo2NDkzLCJ0ZXh0IjoiOSJ9LCIwWW
szQmhXM3d3YUhEYWllIjp7InN0YXJ0Ijo2Nzg0LCJlbmQiOjY3
ODYsInRleHQiOiIxMCJ9LCIyako4Q1cwOHlsMUN5NVhFIjp7In
N0YXJ0Ijo3MDU2LCJlbmQiOjcwNjIsInRleHQiOiJGaWd1cmUi
fSwiTUlGMTg2d1o1eG5kelg1NSI6eyJzdGFydCI6NzA2NCwiZW
5kIjo3MDY2LCJ0ZXh0IjoiMTEifSwidWhoVGJFTHF5UjB2c00x
TyI6eyJzdGFydCI6NzY0OSwiZW5kIjo3NjU1LCJ0ZXh0IjoiRm
lndXJlIn0sImsxakVZUTFrWmE2NWJiTTAiOnsic3RhcnQiOjc2
NTcsImVuZCI6NzY1OSwidGV4dCI6IjEyIn0sIjJabDhDcUpBRX
dxS3hEdlQiOnsic3RhcnQiOjgwMDUsImVuZCI6ODAxMSwidGV4
dCI6IkZpZ3VyZSJ9LCJBamViR2R2MkRtUnJFNkVwIjp7InN0YX
J0Ijo4MDUyLCJlbmQiOjgwNTQsInRleHQiOiIxMyJ9LCJNSzQ2
ekRmT1R2NG9lcTZiIjp7InN0YXJ0Ijo4NTIxLCJlbmQiOjg1Mj
ksInRleHQiOiItIEZpZ3VyZSJ9LCJTQzV3OTZiWDZpU3JxRm9D
Ijp7InN0YXJ0Ijo4NTMxLCJlbmQiOjg1MzMsInRleHQiOiIxNC
J9LCJxMWlWNmJHcDVmNHJmRndRIjp7InN0YXJ0Ijo4NjcwLCJl
bmQiOjg2NzYsInRleHQiOiJGaWd1cmUifSwiN3BtTUdOU29vUH
ozSmd3RCI6eyJzdGFydCI6OTE3NSwiZW5kIjo5MTc3LCJ0ZXh0
IjoiMTUifSwiekJNWTBrcEZpczBuWjZqYSI6eyJzdGFydCI6OT
M0OCwiZW5kIjo5MzQ5LCJ0ZXh0IjoiMTYifSwiY2dXdEFVdHdw
WEI5VU1WZiI6eyJzdGFydCI6OTM0MCwiZW5kIjo5MzQ2LCJ0ZX
h0IjoiRmlndXJlIn0sIjM0ZXFzck9yaGpqT003T0MiOnsic3Rh
cnQiOjk2MjcsImVuZCI6OTYzNSwidGV4dCI6Ii0gRmlndXJlIn
0sIlZXMkJtQm02ZmRjclhaZmQiOnsic3RhcnQiOjk2MzcsImVu
ZCI6OTYzOSwidGV4dCI6IjE3In0sIlNCb25zYk5oU0x3RGhnQm
IiOnsic3RhcnQiOjU3MSwiZW5kIjo1ODMsInRleHQiOiIjIyBE
QVRBIFVTRUQifSwiTUJyU3VnSVFBSjQxcGtIVyI6eyJzdGFydC
I6NzQsImVuZCI6OTUsInRleHQiOiIjIyBPVkVSVklFVyAmIFBV
UlBPU0UifX0sImNvbW1lbnRzIjp7IkdiTG9wVjRiNVBXcERPaV
QiOnsiZGlzY3Vzc2lvbklkIjoiNzZaVTFLQlZGNTNCTzQzdCIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlJld3JpdGUiLC
JjcmVhdGVkIjoxNjg3MTcwNzgxODQ3fSwibXY5aTJmSG9MV1lh
SVU4YSI6eyJkaXNjdXNzaW9uSWQiOiJINnp5OTZRSlh5Nk1McF
JtIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBp
Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcwODM1MjcwfSwicVVpd1
NqRUxUaDd0aUs1NSI6eyJkaXNjdXNzaW9uSWQiOiIyckpGU0FR
SlV2WXIwRndXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiRml4IHJlZmVyZW5jZSIsImNyZWF0ZWQiOjE2ODcxNzA4ODg3
NzR9LCJQOWV4bVhLUGs2SVROaUx3Ijp7ImRpc2N1c3Npb25JZC
I6IlJ0azByTlFCQnVGaHdCNUUiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJXcml0ZSBvdXQgaW5zdHJ1Y3Rpb25zIiwiY3
JlYXRlZCI6MTY4NzE3MDk1MzU0M30sIkE3czBSeDdKbVdZeWtX
ODYiOnsiZGlzY3Vzc2lvbklkIjoiSGhwMFp4Q2tHbnk1eUV0QS
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3Qg
Zm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcwOTk0ODg1fSwiQU
tVcHFwcXVhYzRWajFucCI6eyJkaXNjdXNzaW9uSWQiOiJZN20x
OXJla3R6cXhkdUJkIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdHVy
ZSIsImNyZWF0ZWQiOjE2ODcxNzEwNzI2NTR9LCJ0NWo5U29MWE
NWZGIyN0Q1Ijp7ImRpc2N1c3Npb25JZCI6IldOUVFNMVJMZ3Jm
a1pxMzkiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3
JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MTA4MTI5Nn0sInp6VXk1QWpScFZHc0RnSl
kiOnsiZGlzY3Vzc2lvbklkIjoiaWpxdnQ5cEtYenR0S3o2VyIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpZ3VyZSBvdX
Qgd2hhdCB0byBkbyB3aXRoIHRoZXNlIiwiY3JlYXRlZCI6MTY4
NzE3MTE5NjgzOH0sIlR2Tk5zS2ZES08zZmtUcGUiOnsiZGlzY3
Vzc2lvbklkIjoid1B2QWp6Sk1remh3ODl0cCIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW
5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMjQ3
MDMyfSwiMEV3cE5qbmdHWTBJNjJFQyI6eyJkaXNjdXNzaW9uSW
QiOiJaa1V2dzg3d2pSOERjcUJPIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNj
g3MTcxMjk4Mzc1fSwiQUtFNFlFN283T1lmNmRGMyI6eyJkaXNj
dXNzaW9uSWQiOiJNZW96RFNxazk5TmJrSGFSIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IGNvdXJzZSBzdHJ1Y3R1
cmUgdG8iLCJjcmVhdGVkIjoxNjg3MTcxNDI1MjU1fSwiQ0VxSz
FUcDRKRVFhQVdPZCI6eyJkaXNjdXNzaW9uSWQiOiJBdkY5anBx
QzdTaVhIa0o4Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNDUyNzI3
fSwiNjlVRFgweVZXQUFJb21hNSI6eyJkaXNjdXNzaW9uSWQiOi
JqUHpwRlpVTkhxVlVPc3lyIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cn
VjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE1MjA0NTZ9LCJtczdS
Y2QzU2xvZklRbGRjIjp7ImRpc2N1c3Npb25JZCI6IkI1S2xaaG
95M3hrZndxUEEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE1Mjk4ND
d9LCJXbFpjcTY3bXZMNDJaSVNwIjp7ImRpc2N1c3Npb25JZCI6
ImtRUnZRWjJmOWJ3WnFrMnYiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6
MTY4NzE3MTU1MjMwM30sImRad05acXpkbjVQUFZFR1oiOnsiZG
lzY3Vzc2lvbklkIjoicjUwTGhPYk5XUEc2ZDZ1ZiIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSV
MiLCJjcmVhdGVkIjoxNjg3MTcxNTc1NzA0fSwiZFI4R3hOMkVh
WVo0cGJoTyI6eyJkaXNjdXNzaW9uSWQiOiIwWWszQmhXM3d3YU
hEYWllIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29y
cmVjdCBmb3IgUUdJUyBhbmQgd3JpdGUgb3V0IGluIG1vcmUgZG
V0YWlsIiwiY3JlYXRlZCI6MTY4NzE3MTYxOTMyOH0sInV3ekdK
SEt3YVZEQThDaDEiOnsiZGlzY3Vzc2lvbklkIjoiMmpKOENXMD
h5bDFDeTVYRSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTYzODkyOH
0sIlZ6MWZRYUtGc2FJdFdET2MiOnsiZGlzY3Vzc2lvbklkIjoi
TUlGMTg2d1o1eG5kelg1NSIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1
Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNjc3MDcxfSwiRnVJaW
NaR3p2MXZaRnFqWCI6eyJkaXNjdXNzaW9uSWQiOiJ1aGhUYkVM
cXlSMHZzTTFPIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNzA1MzYw
fSwieWdUTjRzTTlubGc0eDdDeiI6eyJkaXNjdXNzaW9uSWQiOi
JrMWpFWVExa1phNjViYk0wIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUywgd3JpdGUgb3V0IG
1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4
NzE3MTc0MTE1OX0sImhoa3hWQmtob2lzMmYyMWQiOnsiZGlzY3
Vzc2lvbklkIjoiMlpsOENxSkFFd3FLeER2VCIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYX
RlZCI6MTY4NzE3MTc1NjU0NH0sIlJFbW1CbnFTZFIxZ3JIb08i
OnsiZGlzY3Vzc2lvbklkIjoiQWplYkdkdjJEbVJyRTZFcCIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9y
IFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdH
VyZSIsImNyZWF0ZWQiOjE2ODcxNzE3OTUxMDR9LCJUMlMwZllS
T0xpUUFVaGN5Ijp7ImRpc2N1c3Npb25JZCI6Ik1LNDZ6RGZPVH
Y0b2VxNmIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE4MzAzNTl9LC
I1clVMa2ZjcWZwMDNKSEtTIjp7ImRpc2N1c3Npb25JZCI6IlND
NXc5NmJYNmlTcnFGb0MiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJDb3JyZWN0IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9y
ZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MT
cxODUzNzEyfSwiSUNScVRqcXNPc1NVdTlvTyI6eyJkaXNjdXNz
aW9uSWQiOiJxMWlWNmJHcDVmNHJmRndRIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVk
IjoxNjg3MTcxODY2MTI4fSwieFRjRnU4ZkxqOHMxc2ZkUyI6ey
JkaXNjdXNzaW9uSWQiOiI3cG1NR05Tb29QejNKZ3dEIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IGZvciBRR0lTLC
B3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJj
cmVhdGVkIjoxNjg3MTcxOTQ5MjY1fSwiOGh3dGd1S0lYRnFROD
V5bSI6eyJkaXNjdXNzaW9uSWQiOiJ6Qk1ZMGtwRmlzMG5aNmph
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IGZvci
BRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1
cmUiLCJjcmVhdGVkIjoxNjg3MTcxOTczNDgxfSwiV2FkM3k4ek
VwNnJkeEZ2cSI6eyJkaXNjdXNzaW9uSWQiOiJjZ1d0QVV0d3BY
QjlVTVZmIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxOTg0NDI1fSwi
Y1lSOEZBZTE0SGdXd3V5MiI6eyJkaXNjdXNzaW9uSWQiOiIzNG
Vxc3JPcmhqak9NN09DIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcyMD
A4MTI4fSwiaEV6S1pwVWE1cVpLMzdSRSI6eyJkaXNjdXNzaW9u
SWQiOiJWVzJCbUJtNmZkY3JYWmZkIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiRml4IGZvciBRR0lTIiwiY3JlYXRlZCI6
MTY4NzE3MjA0Mjk2MH0sIm9UWHo3cjYxcjJISGRydGoiOnsiZG
lzY3Vzc2lvbklkIjoiU0JvbnNiTmhTTHdEaGdCYiIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCIsImNyZWF0ZWQiOj
E2ODcxNzIyMDE1MzV9LCJVRjM0VFl4Z1l2UjB5MVNSIjp7ImRp
c2N1c3Npb25JZCI6Ik1CclN1Z0lRQUo0MXBrSFciLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQiLCJjcmVhdGVkIjox
Njg3MTcyMjA1NDg2fX0sImhpc3RvcnkiOlsxMDkzMzEyODE5LD
I4NDUyMzA4Niw4NDAxNTQzOSwtODkxNTk5MjMzXX0=
-->