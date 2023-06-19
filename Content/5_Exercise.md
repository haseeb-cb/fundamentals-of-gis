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

### 1.1: Getting to know the digital elevation model

- Figure of DEM

1. Start the exercise by downloading the data “Exercise7.zip” from the course portal in Moodle and saving it in a folder for this exercise.

2. You have to download the Digital Elevation Model (DEM) from PaITuli. Select National Land Survey of Finland (NLS) Elevation Model as the data, 10m x 10m as the grid size (cell size), type L3343 to the search bar and download the given files.

3. Add the Digital Elevation Model you downloaded from PaITuli. The program will probably ask whether you want to add pyramids – in this case just press yes. The DEM is a large raster image file and thus rather heavy to process. To make the program run smoother, clip the DEM to a smaller extent. Study area for the practical is the same as Muurla_Frame -layer, use it for the clipping extent.

*Tip: there’s separate tools for vector and raster files. Clipping rasters happens with Clip Raster -tool. Don’t forget to name your output files! Great name for this file could be DEM10m_Muurla, for example.*

4. One of the important features of DEM is that it can be used to create a hillshade relief. Hillshade is mostly used in visualization to create an imposing 3D-effect of the surface. To create a hillshade, open Tools and navigate to Spatial Analyst Tools → Surface → Hillshade. Choose the clipped DEM as the input raster and set the output folder. Try first how the hillshade turns out with the default settings. You can change the result by adjusting these default values for azimuth and altitude. Basically, this adjusts from which angle the light hits the ground.

*Tip: Again, name the files! Good name for the first Hillshade could be for example “HillShade_Muurla_def” or “HS_Muurla_def” indicating that it’s a hillshade, study area and default settings – for the next one you could change the name to for example “HS_Muurla_Az180” and so on, based on the chosen settings.*

5. Another very useful feature of a DEM is the possibility to identify the gradient of the raster surface. This can be done with the Slope –tool, which can also be found under the Surface -tools. Again, use the clipped DEM as the input raster and perform the operation. You can use the default settings.

Questions:
- What do the hill shade parameters azimuth and altitude mean?
- What is the maximum slope of the study area based on the DEM10m_Muurla?
- How about the mean slope of the study area based on the DEM10m_Muurla?

### 1.2: Data type conversions - fe
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI3NlpVMUtCVkY1M0JPNDN0Ijp7In
N0YXJ0Ijo5OCwiZW5kIjoxMTEsInRleHQiOiIjIyBPQkpFQ1RJ
VkVTIn0sIkg2enk5NlFKWHk2TUxwUm0iOnsic3RhcnQiOjEwMz
IsImVuZCI6MTA0NywidGV4dCI6Ii0gRmlndXJlIG9mIERFTSJ9
LCIyckpGU0FRSlV2WXIwRndXIjp7InN0YXJ0IjoxMTM3LCJlbm
QiOjExNDMsInRleHQiOiJNb29kbGUifSwiUnRrMHJOUUJCdUZo
d0I1RSI6eyJzdGFydCI6MTE5MCwiZW5kIjoxMTkxLCJ0ZXh0Ij
oiMiJ9LCJaZTJRT2VZYmVncDNBdWp4Ijp7InN0YXJ0IjoxNDM2
LCJlbmQiOjE0MzcsInRleHQiOiIzIn0sIkhocDBaeENrR255NX
lFdEEiOnsic3RhcnQiOjE4MzIsImVuZCI6MTgzNSwidGV4dCI6
IlRpcCJ9LCJZN20xOXJla3R6cXhkdUJkIjp7InN0YXJ0IjoyMD
QyLCJlbmQiOjIwNDMsInRleHQiOiI0In0sIldOUVFNMVJMZ3Jm
a1pxMzkiOnsic3RhcnQiOjI5MjMsImVuZCI6MjkyNCwidGV4dC
I6IjUifSwiaWpxdnQ5cEtYenR0S3o2VyI6eyJzdGFydCI6MzIy
OCwiZW5kIjozMjM4LCJ0ZXh0IjoiUXVlc3Rpb25zOiJ9fSwiY2
9tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVCI6eyJkaXNjdXNz
aW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsImNyZWF0ZWQiOjE2
ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJVThhIjp7ImRpc2
N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm0iLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2pFTFRoN3RpSzU1
Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFKVXZZcjBGd1ciLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVmZXJl
bmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3NH0sIlA5ZXhtWE
tQazZJVE5pTHciOnsiZGlzY3Vzc2lvbklkIjoiUnRrMHJOUUJC
dUZod0I1RSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Il
dyaXRlIG91dCBpbnN0cnVjdGlvbnMiLCJjcmVhdGVkIjoxNjg3
MTcwOTUzNTQzfSwiUFR0WGJOaG83MFFEMng4eCI6eyJkaXNjdX
NzaW9uSWQiOiJaZTJRT2VZYmVncDNBdWp4Iiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBmb3IgUUdJUyIsIm
NyZWF0ZWQiOjE2ODcxNzA5NzczMTl9LCJBN3MwUng3Sm1XWXlr
Vzg2Ijp7ImRpc2N1c3Npb25JZCI6IkhocDBaeENrR255NXlFdE
EiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb3JyZWN0
IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3MDk5NDg4NX0sIk
FLVXBxcHF1YWM0VmoxbnAiOnsiZGlzY3Vzc2lvbklkIjoiWTdt
MTlyZWt0enF4ZHVCZCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkNvcnJlY3QgZm9yIFFHSVMgYW5kIGZpeCBzdHJ1Y3R1
cmUiLCJjcmVhdGVkIjoxNjg3MTcxMDcyNjU0fSwidDVqOVNvTF
hDVmRiMjdENSI6eyJkaXNjdXNzaW9uSWQiOiJXTlFRTTFSTGdy
ZmtacTM5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ2
9ycmVjdCBmb3IgUUdJUyBhbmQgZml4IHN0cnVjdHVyZSIsImNy
ZWF0ZWQiOjE2ODcxNzEwODEyOTZ9LCJ6elV5NUFqUnBWR3NEZ0
pZIjp7ImRpc2N1c3Npb25JZCI6ImlqcXZ0OXBLWHp0dEt6Nlci
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaWd1cmUgb3
V0IHdoYXQgdG8gZG8gd2l0aCB0aGVzZSIsImNyZWF0ZWQiOjE2
ODcxNzExOTY4Mzh9fSwiaGlzdG9yeSI6Wy0xODc1NzY0OTA4LC
04OTE1OTkyMzNdfQ==
-->