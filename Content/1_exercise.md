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

---

### Georeferencing the arena plans 

5. In the downloaded data, there is a file - nokia_areena_plan.tif – that has been saved from a pdf file downloaded off the Tampere City website. It is a raster file, but it doesn’t have any spatial information associated with the grid cells or pixels. That means that QGIS doesn’t know where the raster is – it cannot project it onto a map. Luckily, there are methods for providing this information to QGIS. This process is called Georeferencing. Let’s now **georeference this image**. To open the georeferencer tool:
	- From the main window, choose *Raster* -> *Georeferencer*. This will open up the *Georeferencer* window

	- In the *Georeferencer* window, choose *File* -> *Open Raster*, and choose the nokia_areena_plan.tif from the folder for this exercise. This will load the image into the *Georeferencer* window. Now, we can provide spatial data to ‘reference’ the image!

6. Let’s do at least four reference points. The more locations, the more spread-out, and the more precise the better the georeferencing result will be. To Georeference: 

	- Click an easily identifiable location point on the nokia_areena_plan.tiff in the *Georeferencer* window, such as the corner of an easily recognizable building. You can zoom in and out of the window to get a more precise location.
	
	- After clicking, it will bring up a dialog that says *Enter Map Coordinates*. You can enter them manually if you know what the coordinates of that location should be. But, it is much simpler to select *From Map Canvas*. This makes the *Georeferencer* window disappear (don’t worry).

	- Next, click on the same easily identifiable location on the QGIS map canvas. This tells the *Georeferencer* that the coordinates of this location are the same as those at that location in the nokia_areena_plan.tiff

	- After clicking on the QIS map canvas, you should see the *Georeferencer* reappear with the coordinates from the location where you clicked. Press OK.

	- Repeat this at least three more times in different locations, preferably well distributed across the map (Figure 2).

- Picture

7. When you are finished adding reference points, you can now perform the georeferencing calculation for the image (Figure 3).

	- Press the *Settings* button on the *Georeferencer* menu, and set the *Transformation type* to *Projective*, set the *Target SRS* to the *Project CRS*, and give your *Output Raster* a informative name (e.g. arena_plan_modified). The *Transformation type* describes the type of mathematical algorithm used to modify (like rotate, twist, skew) the raster. Press OK.

	- Press the *Run* arrow in the *Georeferencer* menu, and the georeferencing will start. It will show you the progress on the georeferencing.

- Picture

8. Once the calculation is complete, close the *Georeferencer* window (there is no need to save the GCP Points). There should be a new raster saved that has been georeferenced, but you may need to add it to your QGIS map now. You can drag it below the building, road, and railway layers to see how it fits (Figure 4). Now would be a good time to save your QGIS project again.

- Picture

---

### Editing the buildings layer

9. Let’s now **remove a building from the buildings layer that no longer exists and add the arena and some surrounding buildings**. This involves editing the tampere_buildings layer.

10. You may need to enable the *Digitizing Toolbar*, which enables you to edit the vector files. To do this, choose *View* -> *Toolbars* and make sure *Digitizing Toolbar* is selected. 

11. Click on the tampere_buildings layer in the layers panel to highlight it, then toggle editing on ![](https://docs.qgis.org/3.28/en/_images/mActionToggleEditing.png)  in the *Digitizing Toolbar*.

- Picture

12. First, let’s remove a building that no longer exists. There is one building at the south of the arena that has been demolished (Figure 6).

	- First, choose the *Select* tool (if you don’t see it, you may need to add the Selection Toolbar like you did for the Digitizing Toolbar).

	- Select the building to be removed by clicking it. It will turn yellow when selected.

	- Press *Delete* on your keyboard. The building is now deleted.

- Picture

13. Now, let’s add some new buildings to the layer.
	
	- Select the *Add Polygon Feature* in the *Digitizing Toolbar* (Figure 7).
	
	- Click around the corners of the raster drawing of the new buildings, gradually drawing a new polygon in the tampere_buildings layer. When you are finished, right-click and the polygon will close. You then get the opportunity to add new Attributes. Add attributes if you want (such as the name of the stadium), then press OK.
	
	- When you are finished adding the new buildings, press the *Save* symbol in the Digitizing Toolbar.

---

### Bus stops
14. Now, let’s **create a new layer with bus stops around the arena**. These are marked in red in the arena_plan_modified.tiff. GIS data on bus stops will be available from Tampere City or OSM, but here we will make our own layer to practice how this is done.

	


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJXcmFjeFYwYVZSSlI0SUp5Ijp7In
N0YXJ0Ijo2NzMsImVuZCI6NjgzLCJ0ZXh0IjoiT2JqZWN0aXZl
cyJ9LCJBR0NsRE1hanRLVkZGZ0x6Ijp7InN0YXJ0Ijo2ODUsIm
VuZCI6Njk3LCJ0ZXh0IjoiIyMgRGF0YSB1c2VkIn0sIjB2TE9q
dlFUYVdYVHp2aUgiOnsic3RhcnQiOjY5OSwiZW5kIjo3MTIsIn
RleHQiOiIjIyBDb21wbGV0aW9uIn0sIlc4UDdRWWZXWHJ2T1JG
cmQiOnsic3RhcnQiOjE3OTcsImVuZCI6MTgwNCwidGV4dCI6Il
BpY3R1cmUifSwiaUU3TmdBeFhnMGN6N3JDeSI6eyJzdGFydCI6
NDk1OSwiZW5kIjo0OTY2LCJ0ZXh0IjoiUGljdHVyZSJ9LCJOZH
pwUWZOM3FmOVdVQ0k0Ijp7InN0YXJ0Ijo1NjA2LCJlbmQiOjU2
MTUsInRleHQiOiItIFBpY3R1cmUifSwicGxpQ3VQVkZqaEdTc3
ZuUyI6eyJzdGFydCI6NTExMCwiZW5kIjo1MTE4LCJ0ZXh0Ijoi
U2V0dGluZ3MifSwiU0RzVmZwQkg2SHhHTzdFRyI6eyJzdGFydC
I6NTk5NiwiZW5kIjo2MDAzLCJ0ZXh0IjoiUGljdHVyZSJ9LCJX
SDNXNms3aEs0Rk9LYWJqIjp7InN0YXJ0Ijo2MjI3LCJlbmQiOj
Y0MTEsInRleHQiOiIxMC4gWW91IG1heSBuZWVkIHRvIGVuYWJs
ZSB0aGUgKkRpZ2l0aXppbmcgVG9vbGJhciosIHdoaWNoIGVuYW
JsZXMgeW91IHRvIGVkaXTigKYifSwiRU9zYVZMR3FpWEE2aUdG
VyI6eyJzdGFydCI6NjYxNiwiZW5kIjo2NjIzLCJ0ZXh0IjoiUG
ljdHVyZSJ9LCJMOUNuTGFEWW5VcnE0bERHIjp7InN0YXJ0Ijo2
NzkxLCJlbmQiOjY3OTcsInRleHQiOiJTZWxlY3QifSwiU1Q0Yk
hCdlUzSEkzU05XRyI6eyJzdGFydCI6NzA2OCwiZW5kIjo3MDc1
LCJ0ZXh0IjoiUGljdHVyZSJ9LCJOMENaRkU0VlllNnowZ0FQIj
p7InN0YXJ0Ijo3NjAxLCJlbmQiOjc2MDUsInRleHQiOiJTYXZl
In19LCJjb21tZW50cyI6eyJoNzY0bVdIYjNKWTd1MU5NIjp7Im
Rpc2N1c3Npb25JZCI6IldyYWN4VjBhVlJKUjRJSnkiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb21lIGJhY2sgdG8gdG
hpcyBhZnRlciBmaW5pc2hpbmcgdGhlIGV4ZXJjaXNlIHBoYXNl
IiwiY3JlYXRlZCI6MTY4NjIwMjMwMDA5MH0sIkFRaTZ1UFRJb1
QyRzlDNVIiOnsiZGlzY3Vzc2lvbklkIjoiQUdDbERNYWp0S1ZG
RmdMeiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlNhbW
UgYXMgYWJvdmUiLCJjcmVhdGVkIjoxNjg2MjAyMzIxNDEwfSwi
TjlBNjZHMGkyUVFVRUc2biI6eyJkaXNjdXNzaW9uSWQiOiIwdk
xPanZRVGFXWFR6dmlIIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiU2FtZSBhcyBhYm92ZSIsImNyZWF0ZWQiOjE2ODYyMD
IzMjk0ODJ9LCJqWVRoRHNLZldMQXBUcFZaIjp7ImRpc2N1c3Np
b25JZCI6Ilc4UDdRWWZXWHJ2T1JGcmQiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJHaXRodWIiLCJjcmVhdGVkIjoxNjg2
MjA0NzUxNzc3fSwiZXNBbWd0cEdVWjFVRkZsTSI6eyJkaXNjdX
NzaW9uSWQiOiJpRTdOZ0F4WGcwY3o3ckN5Iiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiR2l0aHViIiwiY3JlYXRlZCI6MT
Y4NjIwNDc2NTU3OX0sInZwRXpKajl1YnltRkxEY3AiOnsiZGlz
Y3Vzc2lvbklkIjoiTmR6cFFmTjNxZjlXVUNJNCIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkdpdGh1YiIsImNyZWF0ZWQi
OjE2ODYyMDQ4NTYzMzd9LCJYcEFuSkhhYTBwOFRYaFhPIjp7Im
Rpc2N1c3Npb25JZCI6InBsaUN1UFZGamhHU3N2blMiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJQaWN0dXJlIiwiY3JlYX
RlZCI6MTY4NjIwNDkxNjc3MH0sIk5tWkk2Q296Wnc4NWdzQzMi
OnsiZGlzY3Vzc2lvbklkIjoiU0RzVmZwQkg2SHhHTzdFRyIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkdpdGh1YiIsImNy
ZWF0ZWQiOjE2ODYyMDUyNzUyNDF9LCJoQmQ4dm9VQWJZb2FLRW
xBIjp7ImRpc2N1c3Npb25JZCI6IldIM1c2azdoSzRGT0thYmoi
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW50cm
9kdWN0aW9uIHRvIHRoaXMgaW4gdGhlb3J5IiwiY3JlYXRlZCI6
MTY4NjIwNTM5OTQwOX0sImxCWUJ5a2tOalVENkl6aEoiOnsiZG
lzY3Vzc2lvbklkIjoiRU9zYVZMR3FpWEE2aUdGVyIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkdpdGh1YiIsImNyZWF0ZW
QiOjE2ODYyMDU2MDM1MTR9LCJzclpIYms5S1psZHBBU3QwIjp7
ImRpc2N1c3Npb25JZCI6Ikw5Q25MYURZblVycTRsREciLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIs
ImNyZWF0ZWQiOjE2ODYyMDU3NDQ2NzR9LCJkWVBSUHR0ajJSNT
hmbmpCIjp7ImRpc2N1c3Npb25JZCI6IlNUNGJIQnZVM0hJM1NO
V0ciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJHaXRodW
IiLCJjcmVhdGVkIjoxNjg2MjA1NzcyMTE0fSwiSmM3MWhkQk5x
ZnU4VUVHUSI6eyJkaXNjdXNzaW9uSWQiOiJOMENaRkU0VlllNn
owZ0FQIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoicGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODYyMDU4NzQ2NDJ9fSwiaGlzdG
9yeSI6WzE1ODg3MDA1OTUsLTE1OTU0ODY1NzZdfQ==
-->