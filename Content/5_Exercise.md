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

Answer the following questions on Moodle:
- What do the hill shade parameters azimuth and altitude mean?
- What is the maximum slope of the study area based on the DEM10m_Muurla? (Hint: Layer Prope
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
QiOjE0NTksInRleHQiOiJNb29kbGUifSwiaWpxdnQ5cEtYenR0
S3o2VyI6eyJzdGFydCI6NDE4MiwiZW5kIjo0MTQxLCJ0ZXh0Ij
oiUXVlc3Rpb25zOiJ9LCJ3UHZBanpKTWt6aHc4OXRwIjp7InN0
YXJ0Ijo0NzYzLCJlbmQiOjQ3NjQsInRleHQiOiI2In0sIlprVX
Z3ODd3alI4RGNxQk8iOnsic3RhcnQiOjUxNjgsImVuZCI6NTE3
NCwidGV4dCI6IkZpZ3VyZSJ9LCJNZW96RFNxazk5TmJrSGFSIj
p7InN0YXJ0Ijo5NzgsImVuZCI6MTAyMywidGV4dCI6IiMjIyBQ
YXJ0IDE6IEdldHRpbmcgZmFtaWxpYXIgd2l0aCByYXN0ZXIgZG
F0YSJ9LCJBdkY5anBxQzdTaVhIa0o4Ijp7InN0YXJ0Ijo2MDQ5
LCJlbmQiOjYwNTUsInRleHQiOiJGaWd1cmUifSwialB6cEZaVU
5IcVZVT3N5ciI6eyJzdGFydCI6NjA5NywiZW5kIjo2MDk4LCJ0
ZXh0IjoiNyJ9LCJCNUtsWmhveTN4a2Z3cVBBIjp7InN0YXJ0Ij
o2NDQ2LCJlbmQiOjY0NTIsInRleHQiOiJGaWd1cmUifSwia1FS
dlFaMmY5YndacWsydiI6eyJzdGFydCI6NjQ1NCwiZW5kIjo2ND
U1LCJ0ZXh0IjoiOCJ9LCJyNTBMaE9iTldQRzZkNnVmIjp7InN0
YXJ0Ijo2NTkwLCJlbmQiOjY1OTEsInRleHQiOiI5In0sIjBZaz
NCaFczd3dhSERhaWUiOnsic3RhcnQiOjY4ODIsImVuZCI6Njg4
NCwidGV4dCI6IjEwIn0sIjJqSjhDVzA4eWwxQ3k1WEUiOnsic3
RhcnQiOjcxNTQsImVuZCI6NzE2MCwidGV4dCI6IkZpZ3VyZSJ9
LCJNSUYxODZ3WjV4bmR6WDU1Ijp7InN0YXJ0Ijo3MTYyLCJlbm
QiOjcxNjQsInRleHQiOiIxMSJ9LCJ1aGhUYkVMcXlSMHZzTTFP
Ijp7InN0YXJ0Ijo3NzQ3LCJlbmQiOjc3NTMsInRleHQiOiJGaW
d1cmUifSwiazFqRVlRMWtaYTY1YmJNMCI6eyJzdGFydCI6Nzc1
NSwiZW5kIjo3NzU3LCJ0ZXh0IjoiMTIifSwiMlpsOENxSkFFd3
FLeER2VCI6eyJzdGFydCI6ODEwMywiZW5kIjo4MTA5LCJ0ZXh0
IjoiRmlndXJlIn0sIkFqZWJHZHYyRG1SckU2RXAiOnsic3Rhcn
QiOjgxNTAsImVuZCI6ODE1MiwidGV4dCI6IjEzIn0sIk1LNDZ6
RGZPVHY0b2VxNmIiOnsic3RhcnQiOjg2MTksImVuZCI6ODYyNy
widGV4dCI6Ii0gRmlndXJlIn0sIlNDNXc5NmJYNmlTcnFGb0Mi
Onsic3RhcnQiOjg2MjksImVuZCI6ODYzMSwidGV4dCI6IjE0In
0sInExaVY2YkdwNWY0cmZGd1EiOnsic3RhcnQiOjg3NjgsImVu
ZCI6ODc3NCwidGV4dCI6IkZpZ3VyZSJ9LCI3cG1NR05Tb29Qej
NKZ3dEIjp7InN0YXJ0Ijo5MjczLCJlbmQiOjkyNzUsInRleHQi
OiIxNSJ9LCJ6Qk1ZMGtwRmlzMG5aNmphIjp7InN0YXJ0Ijo5ND
Q2LCJlbmQiOjk0NDcsInRleHQiOiIxNiJ9LCJjZ1d0QVV0d3BY
QjlVTVZmIjp7InN0YXJ0Ijo5NDM4LCJlbmQiOjk0NDQsInRleH
QiOiJGaWd1cmUifSwiMzRlcXNyT3JoampPTTdPQyI6eyJzdGFy
dCI6OTcyNSwiZW5kIjo5NzMzLCJ0ZXh0IjoiLSBGaWd1cmUifS
wiVlcyQm1CbTZmZGNyWFpmZCI6eyJzdGFydCI6OTczNSwiZW5k
Ijo5NzM3LCJ0ZXh0IjoiMTcifSwiU0JvbnNiTmhTTHdEaGdCYi
I6eyJzdGFydCI6NTcxLCJlbmQiOjU4MywidGV4dCI6IiMjIERB
VEEgVVNFRCJ9LCJNQnJTdWdJUUFKNDFwa0hXIjp7InN0YXJ0Ij
o3NCwiZW5kIjo5NSwidGV4dCI6IiMjIE9WRVJWSUVXICYgUFVS
UE9TRSJ9fSwiY29tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVC
I6eyJkaXNjdXNzaW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsIm
NyZWF0ZWQiOjE2ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJ
VThhIjp7ImRpc2N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm
0iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2
pFTFRoN3RpSzU1Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFK
VXZZcjBGd1ciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JGaXggcmVmZXJlbmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3
NH0sInp6VXk1QWpScFZHc0RnSlkiOnsiZGlzY3Vzc2lvbklkIj
oiaWpxdnQ5cEtYenR0S3o2VyIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkZpZ3VyZSBvdXQgd2hhdCB0byBkbyB3aXRoIH
RoZXNlIiwiY3JlYXRlZCI6MTY4NzE3MTE5NjgzOH0sIlR2Tk5z
S2ZES08zZmtUcGUiOnsiZGlzY3Vzc2lvbklkIjoid1B2QWp6Sk
1remh3ODl0cCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLC
JjcmVhdGVkIjoxNjg3MTcxMjQ3MDMyfSwiMEV3cE5qbmdHWTBJ
NjJFQyI6eyJkaXNjdXNzaW9uSWQiOiJaa1V2dzg3d2pSOERjcU
JPIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBp
Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxMjk4Mzc1fSwiQUtFNF
lFN283T1lmNmRGMyI6eyJkaXNjdXNzaW9uSWQiOiJNZW96RFNx
azk5TmJrSGFSIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiRml4IGNvdXJzZSBzdHJ1Y3R1cmUgdG8iLCJjcmVhdGVkIjox
Njg3MTcxNDI1MjU1fSwiQ0VxSzFUcDRKRVFhQVdPZCI6eyJkaX
NjdXNzaW9uSWQiOiJBdkY5anBxQzdTaVhIa0o4Iiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcm
VhdGVkIjoxNjg3MTcxNDUyNzI3fSwiNjlVRFgweVZXQUFJb21h
NSI6eyJkaXNjdXNzaW9uSWQiOiJqUHpwRlpVTkhxVlVPc3lyIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOj
E2ODcxNzE1MjA0NTZ9LCJtczdSY2QzU2xvZklRbGRjIjp7ImRp
c2N1c3Npb25JZCI6IkI1S2xaaG95M3hrZndxUEEiLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNy
ZWF0ZWQiOjE2ODcxNzE1Mjk4NDd9LCJXbFpjcTY3bXZMNDJaSV
NwIjp7ImRpc2N1c3Npb25JZCI6ImtRUnZRWjJmOWJ3WnFrMnYi
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IG
ZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MTU1MjMwM30sImRa
d05acXpkbjVQUFZFR1oiOnsiZGlzY3Vzc2lvbklkIjoicjUwTG
hPYk5XUEc2ZDZ1ZiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkNvcnJlY3QgZm9yIFFHSVMiLCJjcmVhdGVkIjoxNjg3MT
cxNTc1NzA0fSwiZFI4R3hOMkVhWVo0cGJoTyI6eyJkaXNjdXNz
aW9uSWQiOiIwWWszQmhXM3d3YUhEYWllIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyBhbmQg
d3JpdGUgb3V0IGluIG1vcmUgZGV0YWlsIiwiY3JlYXRlZCI6MT
Y4NzE3MTYxOTMyOH0sInV3ekdKSEt3YVZEQThDaDEiOnsiZGlz
Y3Vzc2lvbklkIjoiMmpKOENXMDh5bDFDeTVYRSIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NzE3MTYzODkyOH0sIlZ6MWZRYUtGc2FJdFdET2
MiOnsiZGlzY3Vzc2lvbklkIjoiTUlGMTg2d1o1eG5kelg1NSIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgZm
9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjox
Njg3MTcxNjc3MDcxfSwiRnVJaWNaR3p2MXZaRnFqWCI6eyJkaX
NjdXNzaW9uSWQiOiJ1aGhUYkVMcXlSMHZzTTFPIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcm
VhdGVkIjoxNjg3MTcxNzA1MzYwfSwieWdUTjRzTTlubGc0eDdD
eiI6eyJkaXNjdXNzaW9uSWQiOiJrMWpFWVExa1phNjViYk0wIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUywgd3JpdGUgb3V0IG1vcmUsIGFuZCBmaXggc3RydW
N0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc0MTE1OX0sImhoa3hW
Qmtob2lzMmYyMWQiOnsiZGlzY3Vzc2lvbklkIjoiMlpsOENxSk
FFd3FLeER2VCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MTc1NjU0NH
0sIlJFbW1CbnFTZFIxZ3JIb08iOnsiZGlzY3Vzc2lvbklkIjoi
QWplYkdkdjJEbVJyRTZFcCIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkNvcnJlY3QgZm9yIFFHSVMsIHdyaXRlIG91dCBt
b3JlLCBhbmQgZml4IHN0cnVjdHVyZSIsImNyZWF0ZWQiOjE2OD
cxNzE3OTUxMDR9LCJUMlMwZllST0xpUUFVaGN5Ijp7ImRpc2N1
c3Npb25JZCI6Ik1LNDZ6RGZPVHY0b2VxNmIiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0
ZWQiOjE2ODcxNzE4MzAzNTl9LCI1clVMa2ZjcWZwMDNKSEtTIj
p7ImRpc2N1c3Npb25JZCI6IlNDNXc5NmJYNmlTcnFGb0MiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0IGZvci
BRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW5kIGZpeCBzdHJ1Y3R1
cmUiLCJjcmVhdGVkIjoxNjg3MTcxODUzNzEyfSwiSUNScVRqcX
NPc1NVdTlvTyI6eyJkaXNjdXNzaW9uSWQiOiJxMWlWNmJHcDVm
NHJmRndRIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxODY2MTI4fSwi
eFRjRnU4ZkxqOHMxc2ZkUyI6eyJkaXNjdXNzaW9uSWQiOiI3cG
1NR05Tb29QejNKZ3dEIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiRml4IGZvciBRR0lTLCB3cml0ZSBvdXQgbW9yZSwgYW
5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3MTcxOTQ5
MjY1fSwiOGh3dGd1S0lYRnFRODV5bSI6eyJkaXNjdXNzaW9uSW
QiOiJ6Qk1ZMGtwRmlzMG5aNmphIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiRml4IGZvciBRR0lTLCB3cml0ZSBvdXQgbW
9yZSwgYW5kIGZpeCBzdHJ1Y3R1cmUiLCJjcmVhdGVkIjoxNjg3
MTcxOTczNDgxfSwiV2FkM3k4ekVwNnJkeEZ2cSI6eyJkaXNjdX
NzaW9uSWQiOiJjZ1d0QVV0d3BYQjlVTVZmIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdG
VkIjoxNjg3MTcxOTg0NDI1fSwiY1lSOEZBZTE0SGdXd3V5MiI6
eyJkaXNjdXNzaW9uSWQiOiIzNGVxc3JPcmhqak9NN09DIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg3MTcyMDA4MTI4fSwiaEV6S1pwVWE1cV
pLMzdSRSI6eyJkaXNjdXNzaW9uSWQiOiJWVzJCbUJtNmZkY3JY
WmZkIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IG
ZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MjA0Mjk2MH0sIm9U
WHo3cjYxcjJISGRydGoiOnsiZGlzY3Vzc2lvbklkIjoiU0Jvbn
NiTmhTTHdEaGdCYiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCIsImNyZWF0ZWQiOjE2ODcxNzIyMDE1MzV9LCJVRj
M0VFl4Z1l2UjB5MVNSIjp7ImRpc2N1c3Npb25JZCI6Ik1CclN1
Z0lRQUo0MXBrSFciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJBZGQiLCJjcmVhdGVkIjoxNjg3MTcyMjA1NDg2fX0sImhp
c3RvcnkiOlsxNzcyNTU3MDA4LDI4NDUyMzA4Niw4NDAxNTQzOS
wtODkxNTk5MjMzXX0=
-->