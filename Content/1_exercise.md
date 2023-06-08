### Fundamentals of Geographic Information Systems (GIS)

# Exercise 1: Introduction continuation



## Overview & purpose
Urban areas undergo continuous development, and maps need to be updated regularly to account for new construction, demolition, and land use changes for example. In this tutorial, the objective is to **edit a GIS layer to show urban development**. In this case, we will be looking at the development of the Nokia Arena in the city centre of Tampere, Finland. 

The learning objectives are:
- Understand vector data
- How to create and edit vector data
- How to georeference a picture
- How to project data in the right Coordinate Reference System

## Objectives

## Data used

## Completion

## Exercise phases
### Getting familiar with the data
It is good to be familiar with the area you will be working with in this exercise:
- https://en.wikipedia.org/wiki/Nokia_Arena_(Tampere)
- https://goo.gl/maps/MifgU6b51S6QKacf7

1. Save the downloaded GIS data in an empty folder for this exercise.

2. Open QGIS and load the tampere_buildings.shp, tampere_roads.shp, and tampere_railway.shp into QGIS (See Crash Course exercise 2.1), the project CRS will change to the CRS of these layers (ETS89/TM35FIN).

3. Add Google Satellite imagery: Navigate to your browser panel > expand XYZ Tiles > drag "Google Satellite" to you the layers panel (See Crash Course exercise 1.2).

4. Take a moment to examine the data you added now, what is it about? What kind of attributes does the data have?
	- Can you find the location of where the Nokia Arena is constructed? (hint: the coordinates are 328300 east, 6822050 north in the ETS89 / TM35FIN(E,N) coordinate system. Does the arena and new development exist in the tampere_buildings layer? What about in the Google satellite imagery?

- Picture

We have a vector layer with the buildings in central Tampere, and a vector layer showing the roads – both of which originally came from OpenStreetMap. This data is old – it shows the area before the development of the arena. In addition, we have a raster image file that shows the designs for the Arena, taken from a planning document. Unfortunately, this raster is not spatially referenced – there is no spatial information associated with each raster cell.

So, the tampere_buildings data is old and we need to update it – there are now new buildings, and an old building has been demolished. City mappers have various ways of updating the spatial databases. Some-times, maps are updated by new aerial imagery. Sometimes, they are updated based on building plans submitted to the city. And, sometimes they might be updated based on measurements carried out by surveyors. In this case, we are going to use an image from the city planning department and add it to our buildings layer, as well as remove some buildings that no longer exist.

### Georeferencing the arena plans 

5. In the downloaded data, there is a file - nokia_areena_plan.tif – that has been saved from a pdf file downloaded off the Tampere City website. It is a raster file, but it doesn’t have any spatial information associated with the grid cells or pixels. That means that QGIS doesn’t know where the raster is – it cannot project it onto a map. Luckily, there are methods for providing this information to QGIS. This process is called Georeferencing. Let’s now georeference this image. To open the georeferencer tool:
	- From the main window, choose *Raster* -> *Georeferencer*. This will open up the *Georeferencer* window

	- In the *Georeferencer* window, choose *File* -> *Open Raster*, and choose the nokia_areena_plan.tif from the folder for this exercise. This will load the image into the *Georeferencer* window. Now, we can provide spatial data to ‘reference’ the image!

6. Let’s do at least four reference points. The more locations, the more spread-out, and the more precise the better the georeferencing result will be. To Georeference: 

	- Click an easily identifiable location point on the nokia_areena_plan.tiff in the *Georeferencer* window, such as the corner of an easily recognizable building. You can zoom in and out of the window to get a more precise location.
	
	- After clicking, it will bring up a dialog that says *Enter Map Coordinates*. You can enter them manually if you know what the coordinates of that location should be. But, it is much simpler to select *From Map Canvas*. This makes the *Georeferencer* window disappear (don’t worry).

	- Next, click on the same easily identifiable location on the QGIS map canvas. This tells the *Georeferencer* that the coordinates of this location are the same as those at that location in the nokia_areena_plan.tiff

	- After clicking on the QIS map canvas, you should see the *Georeferencer* reappear with the coordinates from the location where you clicked. Press OK.

	- Repeat this at least three more times in different locations, preferably well distributed across the map (Figure 2).

- Picture

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJXcmFjeFYwYVZSSlI0SUp5Ijp7In
N0YXJ0Ijo2NzMsImVuZCI6NjgzLCJ0ZXh0IjoiT2JqZWN0aXZl
cyJ9LCJBR0NsRE1hanRLVkZGZ0x6Ijp7InN0YXJ0Ijo2ODUsIm
VuZCI6Njk3LCJ0ZXh0IjoiIyMgRGF0YSB1c2VkIn0sIjB2TE9q
dlFUYVdYVHp2aUgiOnsic3RhcnQiOjY5OSwiZW5kIjo3MTIsIn
RleHQiOiIjIyBDb21wbGV0aW9uIn0sIlc4UDdRWWZXWHJ2T1JG
cmQiOnsic3RhcnQiOjE3OTcsImVuZCI6MTgwNCwidGV4dCI6Il
BpY3R1cmUifSwiaUU3TmdBeFhnMGN6N3JDeSI6eyJzdGFydCI6
NDk1MCwiZW5kIjo0OTU3LCJ0ZXh0IjoiUGljdHVyZSJ9fSwiY2
9tbWVudHMiOnsiaDc2NG1XSGIzSlk3dTFOTSI6eyJkaXNjdXNz
aW9uSWQiOiJXcmFjeFYwYVZSSlI0SUp5Iiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQ29tZSBiYWNrIHRvIHRoaXMgYWZ0
ZXIgZmluaXNoaW5nIHRoZSBleGVyY2lzZSBwaGFzZSIsImNyZW
F0ZWQiOjE2ODYyMDIzMDAwOTB9LCJBUWk2dVBUSW9UMkc5QzVS
Ijp7ImRpc2N1c3Npb25JZCI6IkFHQ2xETWFqdEtWRkZnTHoiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJTYW1lIGFzIGFi
b3ZlIiwiY3JlYXRlZCI6MTY4NjIwMjMyMTQxMH0sIk45QTY2Rz
BpMlFRVUVHNm4iOnsiZGlzY3Vzc2lvbklkIjoiMHZMT2p2UVRh
V1hUenZpSCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Il
NhbWUgYXMgYWJvdmUiLCJjcmVhdGVkIjoxNjg2MjAyMzI5NDgy
fSwiallUaERzS2ZXTEFwVHBWWiI6eyJkaXNjdXNzaW9uSWQiOi
JXOFA3UVlmV1hydk9SRnJkIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiR2l0aHViIiwiY3JlYXRlZCI6MTY4NjIwNDc1MT
c3N30sImVzQW1ndHBHVVoxVUZGbE0iOnsiZGlzY3Vzc2lvbklk
IjoiaUU3TmdBeFhnMGN6N3JDeSIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkdpdGh1YiIsImNyZWF0ZWQiOjE2ODYyMDQ3
NjU1Nzl9fSwiaGlzdG9yeSI6WzEwMTY5NTQ0NzQsLTE1OTU0OD
Y1NzZdfQ==
-->