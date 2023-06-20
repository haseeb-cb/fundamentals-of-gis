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

- Figure

7. Start off with the water criteria. Go to Buffer -tool and make a 10-meter buffer for the Bodies_of_Water -layer without dissolving.

8. Next, you have to convert the newly created buffer zone -layer to raster format. As learned before in this practical, use the Feature to Raster -tool to make this rasterization. Choose “FID” as the field to assign the values to the output raster and check that the cell size matches DEM.

1.  Next navigate to Spatial Analyst Tools → Reclass → Reclassify. In order for the further calculations to succeed, you have to make the NoData acceptable because those areas are the ones without water. Make the changes as below and save the file as “reclass_water”.

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
QiOjE0NTksInRleHQiOiJNb29kbGUifSwiWmtVdnc4N3dqUjhE
Y3FCTyI6eyJzdGFydCI6NTQyMiwiZW5kIjo1NDI4LCJ0ZXh0Ij
oiRmlndXJlIn0sIk1lb3pEU3FrOTlOYmtIYVIiOnsic3RhcnQi
Ojk3OCwiZW5kIjoxMDIzLCJ0ZXh0IjoiIyMjIFBhcnQgMTogR2
V0dGluZyBmYW1pbGlhciB3aXRoIHJhc3RlciBkYXRhIn0sIkF2
RjlqcHFDN1NpWEhrSjgiOnsic3RhcnQiOjYzMDMsImVuZCI6Nj
MwOSwidGV4dCI6IkZpZ3VyZSJ9LCJqUHpwRlpVTkhxVlVPc3ly
Ijp7InN0YXJ0Ijo2MzUxLCJlbmQiOjYzNTEsInRleHQiOiI3In
0sIkI1S2xaaG95M3hrZndxUEEiOnsic3RhcnQiOjYzNTQsImVu
ZCI6NjM2MCwidGV4dCI6IkZpZ3VyZSJ9LCJrUVJ2UVoyZjlid1
pxazJ2Ijp7InN0YXJ0Ijo2MzYzLCJlbmQiOjYzNjIsInRleHQi
OiI4In0sInI1MExoT2JOV1BHNmQ2dWYiOnsic3RhcnQiOjY0OT
ksImVuZCI6NjQ5OCwidGV4dCI6IjkifSwiMFlrM0JoVzN3d2FI
RGFpZSI6eyJzdGFydCI6Njc5MCwiZW5kIjo2NzkxLCJ0ZXh0Ij
oiMTAifSwiMmpKOENXMDh5bDFDeTVYRSI6eyJzdGFydCI6NzA2
MSwiZW5kIjo3MDY3LCJ0ZXh0IjoiRmlndXJlIn0sIk1JRjE4Nn
daNXhuZHpYNTUiOnsic3RhcnQiOjcwNjksImVuZCI6NzA3MSwi
dGV4dCI6IjExIn0sInVoaFRiRUxxeVIwdnNNMU8iOnsic3Rhcn
QiOjc2NTQsImVuZCI6NzY2MCwidGV4dCI6IkZpZ3VyZSJ9LCJr
MWpFWVExa1phNjViYk0wIjp7InN0YXJ0Ijo3NjYyLCJlbmQiOj
c2NjQsInRleHQiOiIxMiJ9LCIyWmw4Q3FKQUV3cUt4RHZUIjp7
InN0YXJ0Ijo4MDEwLCJlbmQiOjgwMTYsInRleHQiOiJGaWd1cm
UifSwiQWplYkdkdjJEbVJyRTZFcCI6eyJzdGFydCI6ODA1Nywi
ZW5kIjo4MDU5LCJ0ZXh0IjoiMTMifSwiTUs0NnpEZk9UdjRvZX
E2YiI6eyJzdGFydCI6ODUyNiwiZW5kIjo4NTM0LCJ0ZXh0Ijoi
LSBGaWd1cmUifSwiU0M1dzk2Ylg2aVNycUZvQyI6eyJzdGFydC
I6ODUzNiwiZW5kIjo4NTM4LCJ0ZXh0IjoiMTQifSwicTFpVjZi
R3A1ZjRyZkZ3USI6eyJzdGFydCI6ODY3NSwiZW5kIjo4NjgxLC
J0ZXh0IjoiRmlndXJlIn0sIjdwbU1HTlNvb1B6M0pnd0QiOnsi
c3RhcnQiOjkxODAsImVuZCI6OTE4MiwidGV4dCI6IjE1In0sIn
pCTVkwa3BGaXMwblo2amEiOnsic3RhcnQiOjkzNTMsImVuZCI6
OTM1NCwidGV4dCI6IjE2In0sImNnV3RBVXR3cFhCOVVNVmYiOn
sic3RhcnQiOjkzNDUsImVuZCI6OTM1MSwidGV4dCI6IkZpZ3Vy
ZSJ9LCIzNGVxc3JPcmhqak9NN09DIjp7InN0YXJ0Ijo5NjMyLC
JlbmQiOjk2NDAsInRleHQiOiItIEZpZ3VyZSJ9LCJWVzJCbUJt
NmZkY3JYWmZkIjp7InN0YXJ0Ijo5NjQyLCJlbmQiOjk2NDQsIn
RleHQiOiIxNyJ9LCJTQm9uc2JOaFNMd0RoZ0JiIjp7InN0YXJ0
Ijo1NzEsImVuZCI6NTgzLCJ0ZXh0IjoiIyMgREFUQSBVU0VEIn
0sIk1CclN1Z0lRQUo0MXBrSFciOnsic3RhcnQiOjc0LCJlbmQi
Ojk1LCJ0ZXh0IjoiIyMgT1ZFUlZJRVcgJiBQVVJQT1NFIn0sIj
ZLSlhuS2NwYXBRZnlEUU8iOnsic3RhcnQiOjQxNDMsImVuZCI6
NDE4NCwidGV4dCI6IkFuc3dlciB0aGUgZm9sbG93aW5nIHF1ZX
N0aW9ucyBvbiBNb29kbGU6In19LCJjb21tZW50cyI6eyJHYkxv
cFY0YjVQV3BET2lUIjp7ImRpc2N1c3Npb25JZCI6Ijc2WlUxS0
JWRjUzQk80M3QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJSZXdyaXRlIiwiY3JlYXRlZCI6MTY4NzE3MDc4MTg0N30sIm
12OWkyZkhvTFdZYUlVOGEiOnsiZGlzY3Vzc2lvbklkIjoiSDZ6
eTk2UUpYeTZNTHBSbSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MDgz
NTI3MH0sInFVaXdTakVMVGg3dGlLNTUiOnsiZGlzY3Vzc2lvbk
lkIjoiMnJKRlNBUUpVdllyMEZ3VyIsInN1YiI6ImdoOjQwMzA0
Nzg4IiwidGV4dCI6IkZpeCByZWZlcmVuY2UiLCJjcmVhdGVkIj
oxNjg3MTcwODg4Nzc0fSwiMEV3cE5qbmdHWTBJNjJFQyI6eyJk
aXNjdXNzaW9uSWQiOiJaa1V2dzg3d2pSOERjcUJPIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJj
cmVhdGVkIjoxNjg3MTcxMjk4Mzc1fSwiQUtFNFlFN283T1lmNm
RGMyI6eyJkaXNjdXNzaW9uSWQiOiJNZW96RFNxazk5TmJrSGFS
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IGNvdX
JzZSBzdHJ1Y3R1cmUgdG8iLCJjcmVhdGVkIjoxNjg3MTcxNDI1
MjU1fSwiQ0VxSzFUcDRKRVFhQVdPZCI6eyJkaXNjdXNzaW9uSW
QiOiJBdkY5anBxQzdTaVhIa0o4Iiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNj
g3MTcxNDUyNzI3fSwiNjlVRFgweVZXQUFJb21hNSI6eyJkaXNj
dXNzaW9uSWQiOiJqUHpwRlpVTkhxVlVPc3lyIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBh
bmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE1Mj
A0NTZ9LCJtczdSY2QzU2xvZklRbGRjIjp7ImRpc2N1c3Npb25J
ZCI6IkI1S2xaaG95M3hrZndxUEEiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODcxNzE1Mjk4NDd9LCJXbFpjcTY3bXZMNDJaSVNwIjp7ImRpc2
N1c3Npb25JZCI6ImtRUnZRWjJmOWJ3WnFrMnYiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTIi
wiY3JlYXRlZCI6MTY4NzE3MTU1MjMwM30sImRad05acXpkbjVQ
UFZFR1oiOnsiZGlzY3Vzc2lvbklkIjoicjUwTGhPYk5XUEc2ZD
Z1ZiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJl
Y3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MTcxNTc1NzA0fS
wiZFI4R3hOMkVhWVo0cGJoTyI6eyJkaXNjdXNzaW9uSWQiOiIw
WWszQmhXM3d3YUhEYWllIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQgd3JpdGUgb3V0
IGluIG1vcmUgZGV0YWlsIiwiY3JlYXRlZCI6MTY4NzE3MTYxOT
MyOH0sInV3ekdKSEt3YVZEQThDaDEiOnsiZGlzY3Vzc2lvbklk
IjoiMmpKOENXMDh5bDFDeTVYRSIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4
NzE3MTYzODkyOH0sIlZ6MWZRYUtGc2FJdFdET2MiOnsiZGlzY3
Vzc2lvbklkIjoiTUlGMTg2d1o1eG5kelg1NSIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW
5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxNjc3
MDcxfSwiRnVJaWNaR3p2MXZaRnFqWCI6eyJkaXNjdXNzaW9uSW
QiOiJ1aGhUYkVMcXlSMHZzTTFPIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNj
g3MTcxNzA1MzYwfSwieWdUTjRzTTlubGc0eDdDeiI6eyJkaXNj
dXNzaW9uSWQiOiJrMWpFWVExa1phNjViYk0wIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUywg
d3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydWN0dXJlIiwiY3
JlYXRlZCI6MTY4NzE3MTc0MTE1OX0sImhoa3hWQmtob2lzMmYy
MWQiOnsiZGlzY3Vzc2lvbklkIjoiMlpsOENxSkFFd3FLeER2VC
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0
dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc1NjU0NH0sIlJFbW1Cbn
FTZFIxZ3JIb08iOnsiZGlzY3Vzc2lvbklkIjoiQWplYkdkdjJE
bVJyRTZFcCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
NvcnJlY3QgZm9yIFFHSVMsIHdyaXRlIG91dCBtb3JlLCBhbmQg
Zml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2ODcxNzE3OTUxMD
R9LCJUMlMwZllST0xpUUFVaGN5Ijp7ImRpc2N1c3Npb25JZCI6
Ik1LNDZ6RGZPVHY0b2VxNmIiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODcx
NzE4MzAzNTl9LCI1clVMa2ZjcWZwMDNKSEtTIjp7ImRpc2N1c3
Npb25JZCI6IlNDNXc5NmJYNmlTcnFGb0MiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvciBRR0lTLCB3cm
l0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVh
dGVkIjoxNjg3MTcxODUzNzEyfSwiSUNScVRqcXNPc1NVdTlvTy
I6eyJkaXNjdXNzaW9uSWQiOiJxMWlWNmJHcDVmNHJmRndRIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cm
UiLCJjcmVhdGVkIjoxNjg3MTcxODY2MTI4fSwieFRjRnU4Zkxq
OHMxc2ZkUyI6eyJkaXNjdXNzaW9uSWQiOiI3cG1NR05Tb29Qej
NKZ3dEIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4
IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdH
J1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxOTQ5MjY1fSwiOGh3
dGd1S0lYRnFRODV5bSI6eyJkaXNjdXNzaW9uSWQiOiJ6Qk1ZMG
twRmlzMG5aNmphIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiRml4IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIG
ZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxOTczNDgx
fSwiV2FkM3k4ekVwNnJkeEZ2cSI6eyJkaXNjdXNzaW9uSWQiOi
JjZ1d0QVV0d3BYQjlVTVZmIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MT
cxOTg0NDI1fSwiY1lSOEZBZTE0SGdXd3V5MiI6eyJkaXNjdXNz
aW9uSWQiOiIzNGVxc3JPcmhqak9NN09DIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVk
IjoxNjg3MTcyMDA4MTI4fSwiaEV6S1pwVWE1cVpLMzdSRSI6ey
JkaXNjdXNzaW9uSWQiOiJWVzJCbUJtNmZkY3JYWmZkIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IGZvciBRR0lTIi
wiY3JlYXRlZCI6MTY4NzE3MjA0Mjk2MH0sIm9UWHo3cjYxcjJI
SGRydGoiOnsiZGlzY3Vzc2lvbklkIjoiU0JvbnNiTmhTTHdEaG
dCYiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCIs
ImNyZWF0ZWQiOjE2ODcxNzIyMDE1MzV9LCJVRjM0VFl4Z1l2Uj
B5MVNSIjp7ImRpc2N1c3Npb25JZCI6Ik1CclN1Z0lRQUo0MXBr
SFciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQiLC
JjcmVhdGVkIjoxNjg3MTcyMjA1NDg2fSwib1VEQlEza3ozSDli
aE8wbSI6eyJkaXNjdXNzaW9uSWQiOiI2S0pYbktjcGFwUWZ5RF
FPIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHNl
Y3Rpb24gaW4gbW9vZGxlIHdoZXJlIHBlb3BsZSBjYW4gZmlsbC
B0aGVzZSBpbiIsImNyZWF0ZWQiOjE2ODcyMzk0MTMwNTJ9fSwi
aGlzdG9yeSI6WzY1ODY5NTI2OCwyODQ1MjMwODYsODQwMTU0Mz
ksLTg5MTU5OTIzM119
-->