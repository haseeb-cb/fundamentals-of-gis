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
	- Open the *Hillshade* tool from the *Processing Toolbox*
	- Choose the clipped DEM as the Elevation layer
	- Try out how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.
	- Choose settings that you think are good and make that layer permanent, you can remove your 

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
QiOjE0NTksInRleHQiOiJNb29kbGUifSwiSGhwMFp4Q2tHbnk1
eUV0QSI6eyJzdGFydCI6MjkwNywiZW5kIjoyOTA2LCJ0ZXh0Ij
oiVGlwIn0sIlk3bTE5cmVrdHpxeGR1QmQiOnsic3RhcnQiOjI5
MDcsImVuZCI6MjkwOCwidGV4dCI6IjQifSwiV05RUU0xUkxncm
ZrWnEzOSI6eyJzdGFydCI6Mzg2OSwiZW5kIjozODcwLCJ0ZXh0
IjoiNSJ9LCJpanF2dDlwS1h6dHRLejZXIjp7InN0YXJ0Ijo0MT
c0LCJlbmQiOjQxODQsInRleHQiOiJRdWVzdGlvbnM6In0sIndQ
dkFqekpNa3podzg5dHAiOnsic3RhcnQiOjQ3NDYsImVuZCI6ND
c0NywidGV4dCI6IjYifSwiWmtVdnc4N3dqUjhEY3FCTyI6eyJz
dGFydCI6NTE1MSwiZW5kIjo1MTU3LCJ0ZXh0IjoiRmlndXJlIn
0sIk1lb3pEU3FrOTlOYmtIYVIiOnsic3RhcnQiOjk3OCwiZW5k
IjoxMDIzLCJ0ZXh0IjoiIyMjIFBhcnQgMTogR2V0dGluZyBmYW
1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sIkF2RjlqcHFDN1Np
WEhrSjgiOnsic3RhcnQiOjYwMzIsImVuZCI6NjAzOCwidGV4dC
I6IkZpZ3VyZSJ9LCJqUHpwRlpVTkhxVlVPc3lyIjp7InN0YXJ0
Ijo2MDgwLCJlbmQiOjYwODEsInRleHQiOiI3In0sIkI1S2xaaG
95M3hrZndxUEEiOnsic3RhcnQiOjY0MjksImVuZCI6NjQzNSwi
dGV4dCI6IkZpZ3VyZSJ9LCJrUVJ2UVoyZjlid1pxazJ2Ijp7In
N0YXJ0Ijo2NDM3LCJlbmQiOjY0MzgsInRleHQiOiI4In0sInI1
MExoT2JOV1BHNmQ2dWYiOnsic3RhcnQiOjY1NzMsImVuZCI6Nj
U3NCwidGV4dCI6IjkifSwiMFlrM0JoVzN3d2FIRGFpZSI6eyJz
dGFydCI6Njg2NSwiZW5kIjo2ODY3LCJ0ZXh0IjoiMTAifSwiMm
pKOENXMDh5bDFDeTVYRSI6eyJzdGFydCI6NzEzNywiZW5kIjo3
MTQzLCJ0ZXh0IjoiRmlndXJlIn0sIk1JRjE4NndaNXhuZHpYNT
UiOnsic3RhcnQiOjcxNDUsImVuZCI6NzE0NywidGV4dCI6IjEx
In0sInVoaFRiRUxxeVIwdnNNMU8iOnsic3RhcnQiOjc3MzAsIm
VuZCI6NzczNiwidGV4dCI6IkZpZ3VyZSJ9LCJrMWpFWVExa1ph
NjViYk0wIjp7InN0YXJ0Ijo3NzM4LCJlbmQiOjc3NDAsInRleH
QiOiIxMiJ9LCIyWmw4Q3FKQUV3cUt4RHZUIjp7InN0YXJ0Ijo4
MDg2LCJlbmQiOjgwOTIsInRleHQiOiJGaWd1cmUifSwiQWplYk
dkdjJEbVJyRTZFcCI6eyJzdGFydCI6ODEzMywiZW5kIjo4MTM1
LCJ0ZXh0IjoiMTMifSwiTUs0NnpEZk9UdjRvZXE2YiI6eyJzdG
FydCI6ODYwMiwiZW5kIjo4NjEwLCJ0ZXh0IjoiLSBGaWd1cmUi
fSwiU0M1dzk2Ylg2aVNycUZvQyI6eyJzdGFydCI6ODYxMiwiZW
5kIjo4NjE0LCJ0ZXh0IjoiMTQifSwicTFpVjZiR3A1ZjRyZkZ3
USI6eyJzdGFydCI6ODc1MSwiZW5kIjo4NzU3LCJ0ZXh0IjoiRm
lndXJlIn0sIjdwbU1HTlNvb1B6M0pnd0QiOnsic3RhcnQiOjky
NTYsImVuZCI6OTI1OCwidGV4dCI6IjE1In0sInpCTVkwa3BGaX
Mwblo2amEiOnsic3RhcnQiOjk0MjksImVuZCI6OTQzMCwidGV4
dCI6IjE2In0sImNnV3RBVXR3cFhCOVVNVmYiOnsic3RhcnQiOj
k0MjEsImVuZCI6OTQyNywidGV4dCI6IkZpZ3VyZSJ9LCIzNGVx
c3JPcmhqak9NN09DIjp7InN0YXJ0Ijo5NzA4LCJlbmQiOjk3MT
YsInRleHQiOiItIEZpZ3VyZSJ9LCJWVzJCbUJtNmZkY3JYWmZk
Ijp7InN0YXJ0Ijo5NzE4LCJlbmQiOjk3MjAsInRleHQiOiIxNy
J9LCJTQm9uc2JOaFNMd0RoZ0JiIjp7InN0YXJ0Ijo1NzEsImVu
ZCI6NTgzLCJ0ZXh0IjoiIyMgREFUQSBVU0VEIn0sIk1CclN1Z0
lRQUo0MXBrSFciOnsic3RhcnQiOjc0LCJlbmQiOjk1LCJ0ZXh0
IjoiIyMgT1ZFUlZJRVcgJiBQVVJQT1NFIn19LCJjb21tZW50cy
I6eyJHYkxvcFY0YjVQV3BET2lUIjp7ImRpc2N1c3Npb25JZCI6
Ijc2WlUxS0JWRjUzQk80M3QiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJSZXdyaXRlIiwiY3JlYXRlZCI6MTY4NzE3MDc4
MTg0N30sIm12OWkyZkhvTFdZYUlVOGEiOnsiZGlzY3Vzc2lvbk
lkIjoiSDZ6eTk2UUpYeTZNTHBSbSIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MT
Y4NzE3MDgzNTI3MH0sInFVaXdTakVMVGg3dGlLNTUiOnsiZGlz
Y3Vzc2lvbklkIjoiMnJKRlNBUUpVdllyMEZ3VyIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCByZWZlcmVuY2UiLCJj
cmVhdGVkIjoxNjg3MTcwODg4Nzc0fSwiQTdzMFJ4N0ptV1l5a1
c4NiI6eyJkaXNjdXNzaW9uSWQiOiJIaHAwWnhDa0dueTV5RXRB
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdC
Bmb3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzA5OTQ4ODV9LCJB
S1VwcXBxdWFjNFZqMW5wIjp7ImRpc2N1c3Npb25JZCI6Ilk3bT
E5cmVrdHpxeGR1QmQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3RydWN0dX
JlIiwiY3JlYXRlZCI6MTY4NzE3MTA3MjY1NH0sInQ1ajlTb0xY
Q1ZkYjI3RDUiOnsiZGlzY3Vzc2lvbklkIjoiV05RUU0xUkxncm
ZrWnEzOSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNv
cnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcm
VhdGVkIjoxNjg3MTcxMDgxMjk2fSwienpVeTVBalJwVkdzRGdK
WSI6eyJkaXNjdXNzaW9uSWQiOiJpanF2dDlwS1h6dHRLejZXIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRmlndXJlIG91
dCB3aGF0IHRvIGRvIHdpdGggdGhlc2UiLCJjcmVhdGVkIjoxNj
g3MTcxMTk2ODM4fSwiVHZOTnNLZkRLTzNma1RwZSI6eyJkaXNj
dXNzaW9uSWQiOiJ3UHZBanpKTWt6aHc4OXRwIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBh
bmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzEyND
cwMzJ9LCIwRXdwTmpuZ0dZMEk2MkVDIjp7ImRpc2N1c3Npb25J
ZCI6IlprVXZ3ODd3alI4RGNxQk8iLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzEyOTgzNzV9LCJBS0U0WUU3bzdPWWY2ZEYzIjp7ImRpc2
N1c3Npb25JZCI6Ik1lb3pEU3FrOTlOYmtIYVIiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJGaXggY291cnNlIHN0cnVjdH
VyZSB0byIsImNyZWF0ZWQiOjE2ODcxNzE0MjUyNTV9LCJDRXFL
MVRwNEpFUWFBV09kIjp7ImRpc2N1c3Npb25JZCI6IkF2RjlqcH
FDN1NpWEhrSjgiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE0NTI3Mj
d9LCI2OVVEWDB5VldBQUlvbWE1Ijp7ImRpc2N1c3Npb25JZCI6
ImpQenBGWlVOSHFWVU9zeXIiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaXggc3Ry
dWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTUyMDQ1Nn0sIm1zN1
JjZDNTbG9mSVFsZGMiOnsiZGlzY3Vzc2lvbklkIjoiQjVLbFpo
b3kzeGtmd3FQQSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTUyOTg0
N30sIldsWmNxNjdtdkw0MlpJU3AiOnsiZGlzY3Vzc2lvbklkIj
oia1FSdlFaMmY5YndacWsydiIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIj
oxNjg3MTcxNTUyMzAzfSwiZFp3TlpxemRuNVBQVkVHWiI6eyJk
aXNjdXNzaW9uSWQiOiJyNTBMaE9iTldQRzZkNnVmIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJ
UyIsImNyZWF0ZWQiOjE2ODcxNzE1NzU3MDR9LCJkUjhHeE4yRW
FZWjRwYmhPIjp7ImRpc2N1c3Npb25JZCI6IjBZazNCaFczd3dh
SERhaWUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3
JyZWN0IGZvciBRR0lTIGFuZCB3cml0ZSBvdXQgaW4gbW9yZSBk
ZXRhaWwiLCJjcmVhdGVkIjoxNjg3MTcxNjE5MzI4fSwidXd6R0
pIS3dhVkRBOENoMSI6eyJkaXNjdXNzaW9uSWQiOiIyako4Q1cw
OHlsMUN5NVhFIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNjM4OTI4
fSwiVnoxZlFhS0ZzYUl0V0RPYyI6eyJkaXNjdXNzaW9uSWQiOi
JNSUYxODZ3WjV4bmR6WDU1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cn
VjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE2NzcwNzF9LCJGdUlp
Y1pHenYxdlpGcWpYIjp7ImRpc2N1c3Npb25JZCI6InVoaFRiRU
xxeVIwdnNNMU8iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3MDUzNj
B9LCJ5Z1RONHNNOW5sZzR4N0N6Ijp7ImRpc2N1c3Npb25JZCI6
ImsxakVZUTFrWmE2NWJiTTAiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTLCB3cml0ZSBvdXQg
bW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNj
g3MTcxNzQxMTU5fSwiaGhreFZCa2hvaXMyZjIxZCI6eyJkaXNj
dXNzaW9uSWQiOiIyWmw4Q3FKQUV3cUt4RHZUIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVh
dGVkIjoxNjg3MTcxNzU2NTQ0fSwiUkVtbUJucVNkUjFnckhvTy
I6eyJkaXNjdXNzaW9uSWQiOiJBamViR2R2MkRtUnJFNkVwIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3
IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0
dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc5NTEwNH0sIlQyUzBmWV
JPTGlRQVVoY3kiOnsiZGlzY3Vzc2lvbklkIjoiTUs0NnpEZk9U
djRvZXE2YiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTgzMDM1OX0s
IjVyVUxrZmNxZnAwM0pIS1MiOnsiZGlzY3Vzc2lvbklkIjoiU0
M1dzk2Ylg2aVNycUZvQyIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3
JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcx
NzE4NTM3MTJ9LCJJQ1JxVGpxc09zU1V1OW9PIjp7ImRpc2N1c3
Npb25JZCI6InExaVY2YkdwNWY0cmZGd1EiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZW
QiOjE2ODcxNzE4NjYxMjh9LCJ4VGNGdThmTGo4czFzZmRTIjp7
ImRpc2N1c3Npb25JZCI6IjdwbU1HTlNvb1B6M0pnd0QiLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggZm9yIFFHSVMs
IHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVyZSIsIm
NyZWF0ZWQiOjE2ODcxNzE5NDkyNjV9LCI4aHd0Z3VLSVhGcVE4
NXltIjp7ImRpc2N1c3Npb25JZCI6InpCTVkwa3BGaXMwblo2am
EiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggZm9y
IFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdH
VyZSIsImNyZWF0ZWQiOjE2ODcxNzE5NzM0ODF9LCJXYWQzeTh6
RXA2cmR4RnZxIjp7ImRpc2N1c3Npb25JZCI6ImNnV3RBVXR3cF
hCOVVNVmYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE5ODQ0MjV9LC
JjWVI4RkFlMTRIZ1d3dXkyIjp7ImRpc2N1c3Npb25JZCI6IjM0
ZXFzck9yaGpqT003T0MiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzIw
MDgxMjh9LCJoRXpLWnBVYTVxWkszN1JFIjp7ImRpc2N1c3Npb2
5JZCI6IlZXMkJtQm02ZmRjclhaZmQiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJGaXggZm9yIFFHSVMiLCJjcmVhdGVkIj
oxNjg3MTcyMDQyOTYwfSwib1RYejdyNjFyMkhIZHJ0aiI6eyJk
aXNjdXNzaW9uSWQiOiJTQm9uc2JOaFNMd0RoZ0JiIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIiwiY3JlYXRlZCI6
MTY4NzE3MjIwMTUzNX0sIlVGMzRUWXhnWXZSMHkxU1IiOnsiZG
lzY3Vzc2lvbklkIjoiTUJyU3VnSVFBSjQxcGtIVyIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCIsImNyZWF0ZWQiOj
E2ODcxNzIyMDU0ODZ9fSwiaGlzdG9yeSI6Wy05OTQ5MTYxNiwy
ODQ1MjMwODYsODQwMTU0MzksLTg5MTU5OTIzM119
-->