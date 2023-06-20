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

8. Next, you have to convert the newly created buffer zone -layer to raster format. As learned before in this practical, use the *Rasterize (Vector to Raster)* tool to make this rasterization. Choose “FID” as the field to assign the values to the output raster and check that the cell size matches DEM.

9.  Next navigate to Spatial Analyst Tools → Reclass → Reclassify. In order for the further calculations to succeed, you have to make the NoData acceptable because those areas are the ones without water. Make the changes as below and save the file as “reclass_water”.

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
MwOSwidGV4dCI6IkZpZ3VyZSJ9LCJrUVJ2UVoyZjlid1pxazJ2
Ijp7InN0YXJ0Ijo2MzUzLCJlbmQiOjYzNTIsInRleHQiOiI4In
0sInI1MExoT2JOV1BHNmQ2dWYiOnsic3RhcnQiOjY1MDgsImVu
ZCI6NjUwNywidGV4dCI6IjkifSwiMFlrM0JoVzN3d2FIRGFpZS
I6eyJzdGFydCI6NjgxMiwiZW5kIjo2ODExLCJ0ZXh0IjoiMTAi
fSwiMmpKOENXMDh5bDFDeTVYRSI6eyJzdGFydCI6NzA4MiwiZW
5kIjo3MDg4LCJ0ZXh0IjoiRmlndXJlIn0sIk1JRjE4NndaNXhu
ZHpYNTUiOnsic3RhcnQiOjcwOTAsImVuZCI6NzA5MSwidGV4dC
I6IjExIn0sInVoaFRiRUxxeVIwdnNNMU8iOnsic3RhcnQiOjc2
NzUsImVuZCI6NzY4MSwidGV4dCI6IkZpZ3VyZSJ9LCJrMWpFWV
Exa1phNjViYk0wIjp7InN0YXJ0Ijo3NjgzLCJlbmQiOjc2ODQs
InRleHQiOiIxMiJ9LCIyWmw4Q3FKQUV3cUt4RHZUIjp7InN0YX
J0Ijo4MDMxLCJlbmQiOjgwMzcsInRleHQiOiJGaWd1cmUifSwi
QWplYkdkdjJEbVJyRTZFcCI6eyJzdGFydCI6ODA3OCwiZW5kIj
o4MDc5LCJ0ZXh0IjoiMTMifSwiTUs0NnpEZk9UdjRvZXE2YiI6
eyJzdGFydCI6ODU0NywiZW5kIjo4NTU1LCJ0ZXh0IjoiLSBGaW
d1cmUifSwiU0M1dzk2Ylg2aVNycUZvQyI6eyJzdGFydCI6ODU1
NywiZW5kIjo4NTU4LCJ0ZXh0IjoiMTQifSwicTFpVjZiR3A1Zj
RyZkZ3USI6eyJzdGFydCI6ODY5NiwiZW5kIjo4NzAyLCJ0ZXh0
IjoiRmlndXJlIn0sIjdwbU1HTlNvb1B6M0pnd0QiOnsic3Rhcn
QiOjkyMDEsImVuZCI6OTIwMiwidGV4dCI6IjE1In0sInpCTVkw
a3BGaXMwblo2amEiOnsic3RhcnQiOjkzNzQsImVuZCI6OTM3NS
widGV4dCI6IjE2In0sImNnV3RBVXR3cFhCOVVNVmYiOnsic3Rh
cnQiOjkzNjYsImVuZCI6OTM3MiwidGV4dCI6IkZpZ3VyZSJ9LC
IzNGVxc3JPcmhqak9NN09DIjp7InN0YXJ0Ijo5NjUzLCJlbmQi
Ojk2NjEsInRleHQiOiItIEZpZ3VyZSJ9LCJWVzJCbUJtNmZkY3
JYWmZkIjp7InN0YXJ0Ijo5NjYzLCJlbmQiOjk2NjQsInRleHQi
OiIxNyJ9LCJTQm9uc2JOaFNMd0RoZ0JiIjp7InN0YXJ0Ijo1Nz
EsImVuZCI6NTgzLCJ0ZXh0IjoiIyMgREFUQSBVU0VEIn0sIk1C
clN1Z0lRQUo0MXBrSFciOnsic3RhcnQiOjc0LCJlbmQiOjk1LC
J0ZXh0IjoiIyMgT1ZFUlZJRVcgJiBQVVJQT1NFIn0sIjZLSlhu
S2NwYXBRZnlEUU8iOnsic3RhcnQiOjQxNDMsImVuZCI6NDE4NC
widGV4dCI6IkFuc3dlciB0aGUgZm9sbG93aW5nIHF1ZXN0aW9u
cyBvbiBNb29kbGU6In19LCJjb21tZW50cyI6eyJHYkxvcFY0Yj
VQV3BET2lUIjp7ImRpc2N1c3Npb25JZCI6Ijc2WlUxS0JWRjUz
Qk80M3QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJSZX
dyaXRlIiwiY3JlYXRlZCI6MTY4NzE3MDc4MTg0N30sIm12OWky
ZkhvTFdZYUlVOGEiOnsiZGlzY3Vzc2lvbklkIjoiSDZ6eTk2UU
pYeTZNTHBSbSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MDgzNTI3MH
0sInFVaXdTakVMVGg3dGlLNTUiOnsiZGlzY3Vzc2lvbklkIjoi
MnJKRlNBUUpVdllyMEZ3VyIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkZpeCByZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3
MTcwODg4Nzc0fSwiMEV3cE5qbmdHWTBJNjJFQyI6eyJkaXNjdX
NzaW9uSWQiOiJaa1V2dzg3d2pSOERjcUJPIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdG
VkIjoxNjg3MTcxMjk4Mzc1fSwiQUtFNFlFN283T1lmNmRGMyI6
eyJkaXNjdXNzaW9uSWQiOiJNZW96RFNxazk5TmJrSGFSIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IGNvdXJzZSBz
dHJ1Y3R1cmUgdG8iLCJjcmVhdGVkIjoxNjg3MTcxNDI1MjU1fS
wiQ0VxSzFUcDRKRVFhQVdPZCI6eyJkaXNjdXNzaW9uSWQiOiJB
dkY5anBxQzdTaVhIa0o4Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcx
NDUyNzI3fSwiV2xaY3E2N212TDQyWklTcCI6eyJkaXNjdXNzaW
9uSWQiOiJrUVJ2UVoyZjlid1pxazJ2Iiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsImNyZW
F0ZWQiOjE2ODcxNzE1NTIzMDN9LCJkWndOWnF6ZG41UFBWRUda
Ijp7ImRpc2N1c3Npb25JZCI6InI1MExoT2JOV1BHNmQ2dWYiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZv
ciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MTU3NTcwNH0sImRSOE
d4TjJFYVlaNHBiaE8iOnsiZGlzY3Vzc2lvbklkIjoiMFlrM0Jo
VzN3d2FIRGFpZSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIHdyaXRlIG91dCBpbiBt
b3JlIGRldGFpbCIsImNyZWF0ZWQiOjE2ODcxNzE2MTkzMjh9LC
J1d3pHSkhLd2FWREE4Q2gxIjp7ImRpc2N1c3Npb25JZCI6IjJq
SjhDVzA4eWwxQ3k1WEUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE2
Mzg5Mjh9LCJWejFmUWFLRnNhSXRXRE9jIjp7ImRpc2N1c3Npb2
5JZCI6Ik1JRjE4NndaNXhuZHpYNTUiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIGFuZCBmaX
ggc3RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTY3NzA3MX0s
IkZ1SWljWkd6djF2WkZxalgiOnsiZGlzY3Vzc2lvbklkIjoidW
hoVGJFTHF5UjB2c00xTyIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MT
cwNTM2MH0sInlnVE40c005bmxnNHg3Q3oiOnsiZGlzY3Vzc2lv
bklkIjoiazFqRVlRMWtaYTY1YmJNMCIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMsIHdyaXRl
IG91dCBtb3JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZW
QiOjE2ODcxNzE3NDExNTl9LCJoaGt4VkJraG9pczJmMjFkIjp7
ImRpc2N1c3Npb25JZCI6IjJabDhDcUpBRXdxS3hEdlQiLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIs
ImNyZWF0ZWQiOjE2ODcxNzE3NTY1NDR9LCJSRW1tQm5xU2RSMW
dySG9PIjp7ImRpc2N1c3Npb25JZCI6IkFqZWJHZHYyRG1SckU2
RXAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZW
N0IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBz
dHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNzk1MTA0fSwiVD
JTMGZZUk9MaVFBVWhjeSI6eyJkaXNjdXNzaW9uSWQiOiJNSzQ2
ekRmT1R2NG9lcTZiIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxODMw
MzU5fSwiNXJVTGtmY3FmcDAzSkhLUyI6eyJkaXNjdXNzaW9uSW
QiOiJTQzV3OTZiWDZpU3JxRm9DIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUywgd3JpdGUgb3
V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3JlYXRlZCI6
MTY4NzE3MTg1MzcxMn0sIklDUnFUanFzT3NTVXU5b08iOnsiZG
lzY3Vzc2lvbklkIjoicTFpVjZiR3A1ZjRyZkZ3USIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3
JlYXRlZCI6MTY4NzE3MTg2NjEyOH0sInhUY0Z1OGZMajhzMXNm
ZFMiOnsiZGlzY3Vzc2lvbklkIjoiN3BtTUdOU29vUHozSmd3RC
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3Ig
UUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dX
JlIiwiY3JlYXRlZCI6MTY4NzE3MTk0OTI2NX0sIjhod3RndUtJ
WEZxUTg1eW0iOnsiZGlzY3Vzc2lvbklkIjoiekJNWTBrcEZpcz
BuWjZqYSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZp
eCBmb3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3
RydWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTk3MzQ4MX0sIldh
ZDN5OHpFcDZyZHhGdnEiOnsiZGlzY3Vzc2lvbklkIjoiY2dXdE
FVdHdwWEI5VU1WZiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTk4ND
QyNX0sImNZUjhGQWUxNEhnV3d1eTIiOnsiZGlzY3Vzc2lvbklk
IjoiMzRlcXNyT3JoampPTTdPQyIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4
NzE3MjAwODEyOH0sImhFektacFVhNXFaSzM3UkUiOnsiZGlzY3
Vzc2lvbklkIjoiVlcyQm1CbTZmZGNyWFpmZCIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkZpeCBmb3IgUUdJUyIsImNyZW
F0ZWQiOjE2ODcxNzIwNDI5NjB9LCJvVFh6N3I2MXIySEhkcnRq
Ijp7ImRpc2N1c3Npb25JZCI6IlNCb25zYk5oU0x3RGhnQmIiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQiLCJjcmVh
dGVkIjoxNjg3MTcyMjAxNTM1fSwiVUYzNFRZeGdZdlIweTFTUi
I6eyJkaXNjdXNzaW9uSWQiOiJNQnJTdWdJUUFKNDFwa0hXIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIiwiY3JlYX
RlZCI6MTY4NzE3MjIwNTQ4Nn0sIm9VREJRM2t6M0g5YmhPMG0i
OnsiZGlzY3Vzc2lvbklkIjoiNktKWG5LY3BhcFFmeURRTyIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBzZWN0aW9u
IGluIG1vb2RsZSB3aGVyZSBwZW9wbGUgY2FuIGZpbGwgdGhlc2
UgaW4iLCJjcmVhdGVkIjoxNjg3MjM5NDEzMDUyfX0sImhpc3Rv
cnkiOlstMTUyMTQwMzY5NSwyODQ1MjMwODYsODQwMTU0MzksLT
g5MTU5OTIzM119
-->