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
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI3NlpVMUtCVkY1M0JPNDN0Ijp7In
N0YXJ0Ijo5OCwiZW5kIjoxMTEsInRleHQiOiIjIyBPQkpFQ1RJ
VkVTIn0sIkg2enk5NlFKWHk2TUxwUm0iOnsic3RhcnQiOjEwMz
IsImVuZCI6MTA0NywidGV4dCI6Ii0gRmlndXJlIG9mIERFTSJ9
LCIyckpGU0FRSlV2WXIwRndXIjp7InN0YXJ0IjoxMTM3LCJlbm
QiOjExNDMsInRleHQiOiJNb29kbGUifSwiRFJaY2xwRWx0NFFs
aXFnWiI6eyJzdGFydCI6MTE5MCwiZW5kIjoxNDM0LCJ0ZXh0Ij
oiMi4gWW91IGhhdmUgdG8gZG93bmxvYWQgdGhlIERpZ2l0YWwg
RWxldmF0aW9uIE1vZGVsIChERU0pIGZyb20gUGFJVHVsaS4gU2
VsZWN04oCmIn19LCJjb21tZW50cyI6eyJHYkxvcFY0YjVQV3BE
T2lUIjp7ImRpc2N1c3Npb25JZCI6Ijc2WlUxS0JWRjUzQk80M3
QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJSZXdyaXRl
IiwiY3JlYXRlZCI6MTY4NzE3MDc4MTg0N30sIm12OWkyZkhvTF
dZYUlVOGEiOnsiZGlzY3Vzc2lvbklkIjoiSDZ6eTk2UUpYeTZN
THBSbSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NzE3MDgzNTI3MH0sInFV
aXdTakVMVGg3dGlLNTUiOnsiZGlzY3Vzc2lvbklkIjoiMnJKRl
NBUUpVdllyMEZ3VyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkZpeCByZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3MTcwOD
g4Nzc0fSwiS3ZlajNmMWlaY1NuS0lOZSI6eyJkaXNjdXNzaW9u
SWQiOiJEUlpjbHBFbHQ0UWxpcWdaIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiV3JpdGUgb3V0IGluc3RydWN0aW9ucyIs
ImNyZWF0ZWQiOjE2ODcxNzA5MDg3OTF9fSwiaGlzdG9yeSI6Wz
gwMjcwMzAyMiwtODkxNTk5MjMzXX0=
-->