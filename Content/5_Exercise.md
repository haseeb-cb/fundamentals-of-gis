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
	- Run the tool and save the output

- Figure

11. Let’s continue with defining the unsuitable areas by determining the “bad slopes”. 
	- Use the *Reclassify by table* tool again, choose this time the slope raster as the input
	- Add the reclassification table as pictured below
		- Hint about earlier question: 1 = suitable, 0 = unsuitable
	- Run the tool and save the output

The “water buffer” and the “bad slopes” will be classified as “0” so that they can be removed from the calculations later on with multiplication.

- Figure

12. Now let’s combine the bad criteria layers
	- Open the *Merge* tool from the *Processing Toolbox* (GDAL > Raster micellaneous > Merge) 
	- Select the reclassified water layer and reclassified slope layer as input layers, leave the rest on default
	- As you will notice, the output has a border around it with the value 0, this is because the merge tool used the extend of the largest layer, which is the water bodies because we added a 10m buffer to this. This is outside our study area, so we need to clip this to the Muurla_Frame again, use the instructions given earlier to do this and save the clipped result for the next steps. 

- Figure of unsuitable areas

#### 2.2: Defining the suitable areas

13. Now after you have identified the unsuitable areas, your next task it to rank the suitable ones.
	- To make the “slope rank” go once again to *Reclassify by table*
	- Choose the original Slope_Muurla file as the input raster
	- Add the reclassification table as pictured below

- Figure of slope rank classifications

Let’s move on to ranking the soil. You can see the explanation for the soil codes below.

- Figure

14. Open the *Reclassify by table* tool , use the soil raster we converted earlier and specify the values as in the figure below. The higher the value the better the soil fits for cultivation.
	- This time set the *Range boundaries* under *Advanced Parameters* on "min <= value <= max", why do you think this is necessary? 

- Figure

***Note**: for simplicity, we did not identify an ‘unsuitable_soil’ layer but only the soil_rank, i.e. areas with soil type as rock will show a low suitability, but they will not be identified as completely unsuitable if they e.g. are located in a suitable slope pixel. This is ok for the purpose of the exercise, but it is good to keep it in mind. As an optional task, you can add them to unsuitable areas and make another analysis as well.*

#### 2.3: Identifying the final suitability ranking

15. In the last part we will use all the components created to get the suitability map. 
	- Open the *Raster calculator*
	- Use the expression from the figure below, don't forget to adjust the names of the layers to correspond to yours
	- Set the reference layer to the original filled DEM layer (why do you think this reference is necessary?)
	- Run the calculation and save the output

- Figure

16. Open once more *Reclassify by table* and select the suitable areas layer as the input. Reclassify the layer so to have 4 classes so that one represents unsuitable values (0) and others have interval of 1 (with rank values 0, 1, 2, 3, see the figure below
	- Set the *Range boundaries* under *Advanced Parameters* to "min <= value <= max" again (hint: <= means less than or equal to")

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
Ijp7InN0YXJ0Ijo3NjU3LCJlbmQiOjc2NjMsInRleHQiOiJGaW
d1cmUifSwidWhoVGJFTHF5UjB2c00xTyI6eyJzdGFydCI6ODE0
NSwiZW5kIjo4MTUxLCJ0ZXh0IjoiRmlndXJlIn0sIk1LNDZ6RG
ZPVHY0b2VxNmIiOnsic3RhcnQiOjkyNzIsImVuZCI6OTI4MCwi
dGV4dCI6Ii0gRmlndXJlIn0sInExaVY2YkdwNWY0cmZGd1EiOn
sic3RhcnQiOjk2MDksImVuZCI6OTYxNSwidGV4dCI6IkZpZ3Vy
ZSJ9LCJ6Qk1ZMGtwRmlzMG5aNmphIjp7InN0YXJ0IjoxMDUxMi
wiZW5kIjoxMDUxMywidGV4dCI6IjE2In0sImNnV3RBVXR3cFhC
OVVNVmYiOnsic3RhcnQiOjEwNTA0LCJlbmQiOjEwNTEwLCJ0ZX
h0IjoiRmlndXJlIn0sIjM0ZXFzck9yaGpqT003T0MiOnsic3Rh
cnQiOjEwOTAxLCJlbmQiOjEwOTA5LCJ0ZXh0IjoiLSBGaWd1cm
UifSwiVlcyQm1CbTZmZGNyWFpmZCI6eyJzdGFydCI6MTA5MTEs
ImVuZCI6MTA5MTIsInRleHQiOiIxNyJ9LCJTQm9uc2JOaFNMd0
RoZ0JiIjp7InN0YXJ0Ijo1NzEsImVuZCI6NTgzLCJ0ZXh0Ijoi
IyMgREFUQSBVU0VEIn0sIk1CclN1Z0lRQUo0MXBrSFciOnsic3
RhcnQiOjc0LCJlbmQiOjk1LCJ0ZXh0IjoiIyMgT1ZFUlZJRVcg
JiBQVVJQT1NFIn0sIjZLSlhuS2NwYXBRZnlEUU8iOnsic3Rhcn
QiOjQ2MDksImVuZCI6NDY1MCwidGV4dCI6IkFuc3dlciB0aGUg
Zm9sbG93aW5nIHF1ZXN0aW9ucyBvbiBNb29kbGU6In0sIk9HTl
BKMGh1OWhSUUU5aVYiOnsic3RhcnQiOjI5NDgsImVuZCI6Mjk2
MiwidGV4dCI6ImZpbGwgaXRzIHNpbmtzIn0sIlVKd2lseDl4bk
ZIWFBwdTAiOnsic3RhcnQiOjMzMTMsImVuZCI6MzMxNywidGV4
dCI6Imljb24ifSwiQlFqazJTWkliUmFMUzRIeSI6eyJzdGFydC
I6ODc5MSwiZW5kIjo4Nzk5LCJ0ZXh0IjoiLSBGaWd1cmUifSwi
OHVHaWRIdm5ZanAxREROZCI6eyJzdGFydCI6ODgyMSwiZW5kIj
o4ODU4LCJ0ZXh0IjoiIyMjIyAyLjI6IERlZmluaW5nIHRoZSBz
dWl0YWJsZSBhcmVhcyJ9LCJwdFFHMVNTTzNUR2xqRWkwIjp7In
N0YXJ0Ijo5MTQyLCJlbmQiOjkxODAsInRleHQiOiItIEZpZ3Vy
ZSBvZiBzbG9wZSByYW5rIGNsYXNzaWZpY2F0aW9ucyJ9fSwiY2
9tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVCI6eyJkaXNjdXNz
aW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsImNyZWF0ZWQiOjE2
ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJVThhIjp7ImRpc2
N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm0iLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2pFTFRoN3RpSzU1
Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFKVXZZcjBGd1ciLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVmZXJl
bmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3NH0sIjBFd3BOam
5nR1kwSTYyRUMiOnsiZGlzY3Vzc2lvbklkIjoiWmtVdnc4N3dq
UjhEY3FCTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTI5ODM3NX0s
IkFLRTRZRTdvN09ZZjZkRjMiOnsiZGlzY3Vzc2lvbklkIjoiTW
VvekRTcWs5OU5ia0hhUiIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkZpeCBjb3Vyc2Ugc3RydWN0dXJlIHRvIiwiY3JlYX
RlZCI6MTY4NzE3MTQyNTI1NX0sIkNFcUsxVHA0SkVRYUFXT2Qi
OnsiZGlzY3Vzc2lvbklkIjoiQXZGOWpwcUM3U2lYSGtKOCIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJl
IiwiY3JlYXRlZCI6MTY4NzE3MTQ1MjcyN30sInV3ekdKSEt3YV
ZEQThDaDEiOnsiZGlzY3Vzc2lvbklkIjoiMmpKOENXMDh5bDFD
eTVYRSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTYzODkyOH0sIkZ1
SWljWkd6djF2WkZxalgiOnsiZGlzY3Vzc2lvbklkIjoidWhoVG
JFTHF5UjB2c00xTyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTcwNT
M2MH0sIlQyUzBmWVJPTGlRQVVoY3kiOnsiZGlzY3Vzc2lvbklk
IjoiTUs0NnpEZk9UdjRvZXE2YiIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4
NzE3MTgzMDM1OX0sIklDUnFUanFzT3NTVXU5b08iOnsiZGlzY3
Vzc2lvbklkIjoicTFpVjZiR3A1ZjRyZkZ3USIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYX
RlZCI6MTY4NzE3MTg2NjEyOH0sIjhod3RndUtJWEZxUTg1eW0i
OnsiZGlzY3Vzc2lvbklkIjoiekJNWTBrcEZpczBuWjZqYSIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJ
Uywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIi
wiY3JlYXRlZCI6MTY4NzE3MTk3MzQ4MX0sIldhZDN5OHpFcDZy
ZHhGdnEiOnsiZGlzY3Vzc2lvbklkIjoiY2dXdEFVdHdwWEI5VU
1WZiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBw
aWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTk4NDQyNX0sImNZUj
hGQWUxNEhnV3d1eTIiOnsiZGlzY3Vzc2lvbklkIjoiMzRlcXNy
T3JoampPTTdPQyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MjAwODEy
OH0sImhFektacFVhNXFaSzM3UkUiOnsiZGlzY3Vzc2lvbklkIj
oiVlcyQm1CbTZmZGNyWFpmZCIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkZpeCBmb3IgUUdJUyIsImNyZWF0ZWQiOjE2OD
cxNzIwNDI5NjB9LCJvVFh6N3I2MXIySEhkcnRqIjp7ImRpc2N1
c3Npb25JZCI6IlNCb25zYk5oU0x3RGhnQmIiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQiLCJjcmVhdGVkIjoxNjg3
MTcyMjAxNTM1fSwiVUYzNFRZeGdZdlIweTFTUiI6eyJkaXNjdX
NzaW9uSWQiOiJNQnJTdWdJUUFKNDFwa0hXIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIiwiY3JlYXRlZCI6MTY4Nz
E3MjIwNTQ4Nn0sIm9VREJRM2t6M0g5YmhPMG0iOnsiZGlzY3Vz
c2lvbklkIjoiNktKWG5LY3BhcFFmeURRTyIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBzZWN0aW9uIGluIG1vb2Rs
ZSB3aGVyZSBwZW9wbGUgY2FuIGZpbGwgdGhlc2UgaW4iLCJjcm
VhdGVkIjoxNjg3MjM5NDEzMDUyfSwiRXpncXozS29tdExnWWNa
QyI6eyJkaXNjdXNzaW9uSWQiOiJPR05QSjBodTloUlFFOWlWIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiV2hhdD8iLCJj
cmVhdGVkIjoxNjg3MjQzNjcxMDM1fSwiQWEwSmFmMGhVRktJMF
d5aCI6eyJkaXNjdXNzaW9uSWQiOiJVSndpbHg5eG5GSFhQcHUw
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3
R1cmUiLCJjcmVhdGVkIjoxNjg3MjQzODk1ODk5fSwieFZxd1ls
TVBXaG1nMDZLWSI6eyJkaXNjdXNzaW9uSWQiOiJCUWprMlNaSW
JSYUxTNEh5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIGZpZ3VyZSIsImNyZWF0ZWQiOjE2ODcyNDc0NzU0MDF9LC
J5dlhjdFRPNnZuVkNMbzREIjp7ImRpc2N1c3Npb25JZCI6Ijh1
R2lkSHZuWWpwMURETmQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJGcm9tIGhlcmUgaXQgY291bGQgYmUgbWFkZSBvcHRp
b25hbC9hbm90aGVyIGV4ZXJjaXNlIiwiY3JlYXRlZCI6MTY4Nz
I0NzYyNTc3OH0sIm9HWUJxaWFyMzlkVjdUVVgiOnsiZGlzY3Vz
c2lvbklkIjoicHRRRzFTU08zVEdsakVpMCIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBmaWd1cmUiLCJjcmVhdGVk
IjoxNjg3MjQ4NTA0MDY0fX0sImhpc3RvcnkiOlszMDQ2ODkwMT
MsLTM3MTU4MTc4NywtMTc0NjQ0MTk1NiwtMTc0NTc4NjI4NCwt
MTgwOTE5NzcxNSwtMTQwMjIyNDMzMCwxODM4MDQwOTkzLC0xMj
Y5MTUzNzgwLDQ5ODc3MDA0NiwtNDEzMjY0NjgxLDE1ODIyNzk3
MDcsLTg4NzIyNDU2MCwyODE5MDc0MSwtMjEwODEwNDg0OCwyOD
Q1MjMwODYsODQwMTU0MzksLTg5MTU5OTIzM119
-->