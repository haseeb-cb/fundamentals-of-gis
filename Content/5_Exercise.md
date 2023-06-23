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

- Figure

16. Open once more *Reclassify by table* and select the suitable areas layer as the input. Reclassify the layer so to have 4 classes so that one represents unsuitable values (0) and others have interval of 1 (with rank values 0, 1, 2, 3, see the figure below)

- Figure

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
V0dGluZyBmYW1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sImNn
V3RBVXR3cFhCOVVNVmYiOnsic3RhcnQiOjExMzQ2LCJlbmQiOj
ExMzUyLCJ0ZXh0IjoiRmlndXJlIn0sIjM0ZXFzck9yaGpqT003
T0MiOnsic3RhcnQiOjExNjE1LCJlbmQiOjExNjIzLCJ0ZXh0Ij
oiLSBGaWd1cmUifSwiVlcyQm1CbTZmZGNyWFpmZCI6eyJzdGFy
dCI6MTE2MjUsImVuZCI6MTE2MjYsInRleHQiOiIxNyJ9LCJTQm
9uc2JOaFNMd0RoZ0JiIjp7InN0YXJ0Ijo1NzEsImVuZCI6NTgz
LCJ0ZXh0IjoiIyMgREFUQSBVU0VEIn0sIk1CclN1Z0lRQUo0MX
BrSFciOnsic3RhcnQiOjc0LCJlbmQiOjk1LCJ0ZXh0IjoiIyMg
T1ZFUlZJRVcgJiBQVVJQT1NFIn0sIjZLSlhuS2NwYXBRZnlEUU
8iOnsic3RhcnQiOjQ2MDksImVuZCI6NDY1MCwidGV4dCI6IkFu
c3dlciB0aGUgZm9sbG93aW5nIHF1ZXN0aW9ucyBvbiBNb29kbG
U6In0sIk9HTlBKMGh1OWhSUUU5aVYiOnsic3RhcnQiOjI5NDgs
ImVuZCI6Mjk2MiwidGV4dCI6ImZpbGwgaXRzIHNpbmtzIn0sIl
VKd2lseDl4bkZIWFBwdTAiOnsic3RhcnQiOjMzMTMsImVuZCI6
MzMxNywidGV4dCI6Imljb24ifSwiOHVHaWRIdm5ZanAxREROZC
I6eyJzdGFydCI6OTE1OSwiZW5kIjo5MTk2LCJ0ZXh0IjoiIyMj
IyAyLjI6IERlZmluaW5nIHRoZSBzdWl0YWJsZSBhcmVhcyJ9fS
wiY29tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVCI6eyJkaXNj
dXNzaW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsImNyZWF0ZWQi
OjE2ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJVThhIjp7Im
Rpc2N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm0iLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsIm
NyZWF0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2pFTFRoN3Rp
SzU1Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFKVXZZcjBGd1
ciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVm
ZXJlbmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3NH0sIjBFd3
BOam5nR1kwSTYyRUMiOnsiZGlzY3Vzc2lvbklkIjoiWmtVdnc4
N3dqUjhEY3FCTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI5ODM3
NX0sIkFLRTRZRTdvN09ZZjZkRjMiOnsiZGlzY3Vzc2lvbklkIj
oiTWVvekRTcWs5OU5ia0hhUiIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkZpeCBjb3Vyc2Ugc3RydWN0dXJlIHRvIiwiY3
JlYXRlZCI6MTY4NzE3MTQyNTI1NX0sIldhZDN5OHpFcDZyZHhG
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
IwNTQ4Nn0sIm9VREJRM2t6M0g5YmhPMG0iOnsiZGlzY3Vzc2lv
bklkIjoiNktKWG5LY3BhcFFmeURRTyIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkFkZCBzZWN0aW9uIGluIG1vb2RsZSB3
aGVyZSBwZW9wbGUgY2FuIGZpbGwgdGhlc2UgaW4iLCJjcmVhdG
VkIjoxNjg3MjM5NDEzMDUyfSwiRXpncXozS29tdExnWWNaQyI6
eyJkaXNjdXNzaW9uSWQiOiJPR05QSjBodTloUlFFOWlWIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiV2hhdD8iLCJjcmVh
dGVkIjoxNjg3MjQzNjcxMDM1fSwiQWEwSmFmMGhVRktJMFd5aC
I6eyJkaXNjdXNzaW9uSWQiOiJVSndpbHg5eG5GSFhQcHUwIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cm
UiLCJjcmVhdGVkIjoxNjg3MjQzODk1ODk5fSwieXZYY3RUTzZ2
blZDTG80RCI6eyJkaXNjdXNzaW9uSWQiOiI4dUdpZEh2bllqcD
FERE5kIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRnJv
bSBoZXJlIGl0IGNvdWxkIGJlIG1hZGUgb3B0aW9uYWwvYW5vdG
hlciBleGVyY2lzZSIsImNyZWF0ZWQiOjE2ODcyNDc2MjU3Nzh9
fSwiaGlzdG9yeSI6WzgwMDQ3NzUzLDE1ODI1NzczNzQsOTIyOD
UwOTY3LDEyODg5OTk4NDYsLTkzMTIwNzE2OCwtMzcxNTgxNzg3
LC0xNzQ2NDQxOTU2LC0xNzQ1Nzg2Mjg0LC0xODA5MTk3NzE1LC
0xNDAyMjI0MzMwLDE4MzgwNDA5OTMsLTEyNjkxNTM3ODAsNDk4
NzcwMDQ2LC00MTMyNjQ2ODEsMTU4MjI3OTcwNywtODg3MjI0NT
YwLDI4MTkwNzQxLC0yMTA4MTA0ODQ4LDI4NDUyMzA4Niw4NDAx
NTQzOV19
-->