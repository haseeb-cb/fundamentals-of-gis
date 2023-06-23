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

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/5_Exercise/5_Exercise_diagram.drawio.png)

#### 2.1: Defining the unsuitable areas

8. Start off with the water criteria. Go to Buffer -tool and make a 10-meter buffer for the Bodies_of_Water -layer without dissolving. (Hint: Exercise 4)

9. Next, you have to convert the newly created buffer zone -layer to raster format. As learned before in this practical, use the *Rasterize (Vector to Raster)* tool to make this rasterization. Choose “Pinta” as the field to assign the values to the output raster and check that the cell size matches DEM.

10.  For further calculations we need to reclassify the data of the water buffer raster layer.
		- Open the *Reclassify by table* tool
		- Add the reclassification table as pictured below
		- Run the tool and save the output

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/5_Exercise/5_Exercise_water_reclassification.png)

11. Let’s continue with defining the unsuitable areas by determining the “bad slopes”. 
	- Use the *Reclassify by table* tool again, choose this time the slope raster as the input
	- Add the reclassification table as pictured below
		- What do you think the 1 and 0 values represent in this analysis?
	- Run the tool and save the output

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/5_Exercise/5_Exercise_slope_reclassification.png)

The “water buffer” and the “bad slopes” will be classified as “0” so that they can be removed from the calculations later on with multiplication.

12. Now let’s combine the bad criteria layers
	- Open the *Merge* tool from the *Processing Toolbox* (GDAL > Raster micellaneous > Merge) 
	- Select the reclassified water layer and reclassified slope layer as input layers, leave the rest on default
	- As you will notice, the output has a border around it with the value 0, this is because the merge tool used the extend of the largest layer, which is the water bodies because we added a 10m buffer to this. This is outside our study area, so we need to clip this to the Muurla_Frame again, use the instructions given earlier to do this and save the clipped result for the next steps. 

The unsuitable areas:
![](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Assets/5_Exercise/5_Exercise_unsuitable.png?raw=true)

#### 2.2: Defining the suitable areas

13. Now after you have identified the unsuitable areas, your next task it to rank the suitable ones.
	- To make the “slope rank” go once again to *Reclassify by table*
	- Choose the original Slope_Muurla file as the input raster
	- Add the reclassification table as pictured below

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/5_Exercise/5_Exercise_slope_rank.png)

Let’s move on to ranking the soil. You can see the explanation for the soil codes below.

| No. | Soil type |
|--|--|
| 3 | Water |
| 4 | Ballast |
| 11 | Sphagnum peat |
| 12 | Coarse sand |
| 13 | Silt |
| 14 | Medium sand |
| 15 | Gravelly till |
| 16 | Sandy till |
| 17 | Clay |
| 18 | Fine sand |
| 19 | Rock |
| 21 | Sedge peat |
| 22 | Muddy silt |


14. Open the *Reclassify by table* tool , use the soil raster we converted earlier and specify the values as in the figure below. The higher the value the better the soil fits for cultivation.
	- This time set the *Range boundaries* under *Advanced Parameters* on "min <= value <= max", why do you think this is necessary? (hint: <= means less than or equal to")

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/5_Exercise/5_Exercise_soil_ranking_classifications.png)

***Note**: for simplicity, we did not identify an ‘unsuitable_soil’ layer but only the soil_rank, i.e. areas with soil type as rock will show a low suitability, but they will not be identified as completely unsuitable if they e.g. are located in a suitable slope pixel. This is ok for the purpose of the exercise, but it is good to keep it in mind. As an optional task, you can add them to unsuitable areas and make another analysis as well.*

#### 2.3: Identifying the final suitability ranking

15. In the last part we will use all the components created to get the suitability map. 
	- Open the *Raster calculator*
	- Use the expression from the figure below, don't forget to adjust the names of the layers to correspond to yours
	- Set the reference layer to the original filled DEM layer (why do you think this reference is necessary?)
	- Run the calculation and save the output

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/5_Exercise/5_Exericse_final_expression.png)

16. Open once more *Reclassify by table* and select the suitable areas layer as the input. Reclassify the layer so to have 4 classes so that one represents unsuitable values (0) and others have interval of 1 (with rank values 0, 1, 2, 3, see the figure below)

![](https://github.com/rowan8k/fundamentals-of-gis/blob/master/Assets/5_Exercise/5_Exericse_final_classifications.png?raw=true)

17. Now, you should see the optimal cultivation areas in the study area. You can add a basemap from XYZ tiles or QMS  and see whether your optimal areas match with the real fields located in the area.

---

### Part 3: Map visualization time

For suitability analysis it’s common to make a map collection showing the criteria areas and the final suitability analysis map. Make maps with following rasters:

• Soil types
• Terrain (hill shade)
• Slopes with unsuitable gradient areas highlighted
• Water bodies (can be combined to terrain or slopes)
• Final suitability analysis map (final rank)

Visualize the rasters as desired (hint: you can change the symbology of raster layers as well). For this type of maps base maps are in general not used. Feel free to include any additional map visualizations.

As your final task, write a short reflection on what was done and why and add it also to your report.

**Don’t forget to add map items for all maps.**

*Tip: Find inspiration for visualization by googling “suitability map cultivating”, “soil type map colors”, and so on.*
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
V0dGluZyBmYW1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sIlNC
b25zYk5oU0x3RGhnQmIiOnsic3RhcnQiOjU3MSwiZW5kIjo1OD
MsInRleHQiOiIjIyBEQVRBIFVTRUQifSwiTUJyU3VnSVFBSjQx
cGtIVyI6eyJzdGFydCI6NzQsImVuZCI6OTUsInRleHQiOiIjIy
BPVkVSVklFVyAmIFBVUlBPU0UifSwiNktKWG5LY3BhcFFmeURR
TyI6eyJzdGFydCI6NDYwOSwiZW5kIjo0NjUwLCJ0ZXh0IjoiQW
5zd2VyIHRoZSBmb2xsb3dpbmcgcXVlc3Rpb25zIG9uIE1vb2Rs
ZToifSwiT0dOUEowaHU5aFJRRTlpViI6eyJzdGFydCI6Mjk0OC
wiZW5kIjoyOTYyLCJ0ZXh0IjoiZmlsbCBpdHMgc2lua3MifSwi
VUp3aWx4OXhuRkhYUHB1MCI6eyJzdGFydCI6MzMxMywiZW5kIj
ozMzE3LCJ0ZXh0IjoiaWNvbiJ9LCI4dUdpZEh2bllqcDFERE5k
Ijp7InN0YXJ0Ijo5MTU5LCJlbmQiOjkxOTYsInRleHQiOiIjIy
MjIDIuMjogRGVmaW5pbmcgdGhlIHN1aXRhYmxlIGFyZWFzIn19
LCJjb21tZW50cyI6eyJHYkxvcFY0YjVQV3BET2lUIjp7ImRpc2
N1c3Npb25JZCI6Ijc2WlUxS0JWRjUzQk80M3QiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJSZXdyaXRlIiwiY3JlYXRlZC
I6MTY4NzE3MDc4MTg0N30sIm12OWkyZkhvTFdZYUlVOGEiOnsi
ZGlzY3Vzc2lvbklkIjoiSDZ6eTk2UUpYeTZNTHBSbSIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwi
Y3JlYXRlZCI6MTY4NzE3MDgzNTI3MH0sInFVaXdTakVMVGg3dG
lLNTUiOnsiZGlzY3Vzc2lvbklkIjoiMnJKRlNBUUpVdllyMEZ3
VyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCByZW
ZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3MTcwODg4Nzc0fSwiMEV3
cE5qbmdHWTBJNjJFQyI6eyJkaXNjdXNzaW9uSWQiOiJaa1V2dz
g3d2pSOERjcUJPIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMjk4Mz
c1fSwiQUtFNFlFN283T1lmNmRGMyI6eyJkaXNjdXNzaW9uSWQi
OiJNZW96RFNxazk5TmJrSGFSIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiRml4IGNvdXJzZSBzdHJ1Y3R1cmUgdG8iLCJj
cmVhdGVkIjoxNjg3MTcxNDI1MjU1fSwib1RYejdyNjFyMkhIZH
J0aiI6eyJkaXNjdXNzaW9uSWQiOiJTQm9uc2JOaFNMd0RoZ0Ji
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIiwiY3
JlYXRlZCI6MTY4NzE3MjIwMTUzNX0sIlVGMzRUWXhnWXZSMHkx
U1IiOnsiZGlzY3Vzc2lvbklkIjoiTUJyU3VnSVFBSjQxcGtIVy
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCIsImNy
ZWF0ZWQiOjE2ODcxNzIyMDU0ODZ9LCJvVURCUTNrejNIOWJoTz
BtIjp7ImRpc2N1c3Npb25JZCI6IjZLSlhuS2NwYXBRZnlEUU8i
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgc2VjdG
lvbiBpbiBtb29kbGUgd2hlcmUgcGVvcGxlIGNhbiBmaWxsIHRo
ZXNlIGluIiwiY3JlYXRlZCI6MTY4NzIzOTQxMzA1Mn0sIkV6Z3
F6M0tvbXRMZ1ljWkMiOnsiZGlzY3Vzc2lvbklkIjoiT0dOUEow
aHU5aFJRRTlpViIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IldoYXQ/IiwiY3JlYXRlZCI6MTY4NzI0MzY3MTAzNX0sIkFh
MEphZjBoVUZLSTBXeWgiOnsiZGlzY3Vzc2lvbklkIjoiVUp3aW
x4OXhuRkhYUHB1MCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzI0Mzg5NT
g5OX0sInl2WGN0VE82dm5WQ0xvNEQiOnsiZGlzY3Vzc2lvbklk
IjoiOHVHaWRIdm5ZanAxREROZCIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkZyb20gaGVyZSBpdCBjb3VsZCBiZSBtYWRl
IG9wdGlvbmFsL2Fub3RoZXIgZXhlcmNpc2UiLCJjcmVhdGVkIj
oxNjg3MjQ3NjI1Nzc4fX0sImhpc3RvcnkiOlstNzYxNjI0MDQw
LDE1ODI1NzczNzQsOTIyODUwOTY3LDEyODg5OTk4NDYsLTkzMT
IwNzE2OCwtMzcxNTgxNzg3LC0xNzQ2NDQxOTU2LC0xNzQ1Nzg2
Mjg0LC0xODA5MTk3NzE1LC0xNDAyMjI0MzMwLDE4MzgwNDA5OT
MsLTEyNjkxNTM3ODAsNDk4NzcwMDQ2LC00MTMyNjQ2ODEsMTU4
MjI3OTcwNywtODg3MjI0NTYwLDI4MTkwNzQxLC0yMTA4MTA0OD
Q4LDI4NDUyMzA4Niw4NDAxNTQzOV19
-->