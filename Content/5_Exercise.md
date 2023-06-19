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
IlRpcCJ9fSwiY29tbWVudHMiOnsiR2JMb3BWNGI1UFdwRE9pVC
I6eyJkaXNjdXNzaW9uSWQiOiI3NlpVMUtCVkY1M0JPNDN0Iiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmV3cml0ZSIsIm
NyZWF0ZWQiOjE2ODcxNzA3ODE4NDd9LCJtdjlpMmZIb0xXWWFJ
VThhIjp7ImRpc2N1c3Npb25JZCI6Ikg2enk5NlFKWHk2TUxwUm
0iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODcxNzA4MzUyNzB9LCJxVWl3U2
pFTFRoN3RpSzU1Ijp7ImRpc2N1c3Npb25JZCI6IjJySkZTQVFK
VXZZcjBGd1ciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JGaXggcmVmZXJlbmNlIiwiY3JlYXRlZCI6MTY4NzE3MDg4ODc3
NH0sIlA5ZXhtWEtQazZJVE5pTHciOnsiZGlzY3Vzc2lvbklkIj
oiUnRrMHJOUUJCdUZod0I1RSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IldyaXRlIG91dCBpbnN0cnVjdGlvbnMiLCJjcm
VhdGVkIjoxNjg3MTcwOTUzNTQzfSwiUFR0WGJOaG83MFFEMng4
eCI6eyJkaXNjdXNzaW9uSWQiOiJaZTJRT2VZYmVncDNBdWp4Ii
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBm
b3IgUUdJUyIsImNyZWF0ZWQiOjE2ODcxNzA5NzczMTl9LCJBN3
MwUng3Sm1XWXlrVzg2Ijp7ImRpc2N1c3Npb25JZCI6IkhocDBa
eENrR255NXlFdEEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDb3JyZWN0IGZvciBRR0lTIiwiY3JlYXRlZCI6MTY4NzE3
MDk5NDg4NX19LCJoaXN0b3J5IjpbMTc2MTUwMjA1MCwtODkxNT
k5MjMzXX0=
-->