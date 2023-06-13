### Fundamentals of Geographic Information Systems (GIS)

# Exercise 1: Georeferencing & digitizing



## Overview & purpose
Urban areas undergo continuous development, and maps need to be updated regularly to account for new construction, demolition, and land use changes for example. In this tutorial, the objective is to **edit a GIS layer to show urban development**. In this case, we will be looking at the development of the Nokia Arena in the city centre of Tampere, Finland. 

## Objectives

- Georeference the arena plans
- Edit the buildings layer to remove the removed buildings and add new buildings
- Digitize the bus stops from the arena plans

## Data used

## Completion

Work in pairs or individually. Complete the exercise and submit a short report containing at least the following:

1. One map of the outcome of the exercise

	- Remember: all maps should have a legend, a scale bar and a north arrow

	- Use the tips from the Crash Course to improve your map

2. A short reflection (200-300 words) on this exercise and your map

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

![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure1.png)

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

	- Repeat this at least three more times in different locations, preferably well distributed across the map.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure2.png)

7. When you are finished adding reference points, you can now perform the georeferencing calculation for the image.

	- Press the *Settings* button ![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/QGIS_georeferencer_settings.png) on the *Georeferencer* menu, and set the *Transformation type* to *Projective*, set the *Target SRS* to the *Project CRS*, give your *Output Raster* an informative name (e.g. arena_plan_modified), and save it in your folder. The *Transformation type* describes the type of mathematical algorithm used to modify (like rotate, twist, skew) the raster. Press OK.

	- Press the *Run* arrow in the *Georeferencer* menu, and the georeferencing will start. It will show you the progress on the georeferencing.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure3.png)

8. Once the calculation is complete, close the *Georeferencer* window (there is no need to save the GCP Points). The new raster that has been georeferenced is saved and you will need add it to your QGIS map now (Hint: Use the Data Source Manager and add it as a raster instead of a vector) . Once its been added, you can drag it below the building, road, and railway layers to see how it fits. Now would be a good time to save your QGIS project again.
	- Check whether the plans line up with the buildings layer (it doesn't have to be perfect for this exercise)! If it doesn't retry the georeferencing with more points and more spacing between them

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure4.png)

---

### Editing the buildings layer

9. Let’s now **remove a building from the buildings layer that no longer exists and add the arena and some surrounding buildings**. This involves editing the tampere_buildings layer.

10. You may need to enable the *Digitizing Toolbar*, which enables you to edit the vector files. To do this, choose *View* -> *Toolbars* and make sure *Digitizing Toolbar* is selected. 

11. Click on the tampere_buildings layer in the layers panel to highlight it, then toggle editing on ![](https://docs.qgis.org/3.28/en/_images/mActionToggleEditing.png)  in the *Digitizing Toolbar*.

![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure5.png)

12. First, let’s remove a building that no longer exists. There is one building at the south of the arena that has been demolished .

	- First, choose the *Select* tool ![](https://docs.qgis.org/3.28/en/_images/mActionSelect.png) (if you don’t see it, you may need to add the Selection Toolbar like you did for the Digitizing Toolbar).

	- Select the building to be removed by clicking it. It will turn yellow when selected.

	- Press *Delete* on your keyboard. The building is now deleted.

![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure6.png)

13. Now, let’s add some new buildings to the layer.
	
	- Select the *Add Polygon Feature* in the *Digitizing Toolbar*.
	
	- Click around the corners of the raster drawing of the new buildings, gradually drawing a new polygon in the tampere_buildings layer. When you are finished, right-click and the polygon will close. You then get the opportunity to add new Attributes. Add attributes if you want (such as the name of the stadium), then press OK.
	
	- When you are finished adding the new buildings, press the *Save* symbol in the Digitizing Toolbar, and toggle off *editing*.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure8.png)

---

### Bus stops
14. Now, let’s **create a new layer with bus stops around the arena**. These are marked in red in the arena_plan_modified.tiff. GIS data on bus stops will be available from Tampere City or OpenStreetMaps, but here we will make our own layer to practice how this is done.

15. First, let’s create a new layer for the bus stops. In the previous step, we learned how to edit an existing layer, but we can also make a new layer ourselves. In this case, we want points to represent bus stops, so we need to create a new point layer.

	- On the menu, choose *Layer* -> *Create Layer* -> *New Shapefile Layer*

	- Give the new layer an informative filename, like "tampere_bus_stops", and save it in your folder

	- Set the *Geometry type* to be *Point*

	- Under *Additional Dimensions*, set the coordinate system to be ETS89 / TM35FIN(E,N) so that it is in the same coordinate system as the other layers

	- When creating a new layer, you can specify what fields you want to be included in the attributes. There is a default field called ID already. Create a new field. Under *Name* write "road_locat". This will contain the name of the road where the bus stop is located. 

	- Under *Type*, make it *Text Data*

	- Press *Add to Fields List*, and it will appear in the list of fields to be created

	- Press OK

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure9.png)

16. We have now created a new layer, but it is empty – there is nothing in it yet. Now, we can edit the new tam-pere_bus_stops layer we have created to add a location and road name. This happens in a similar way to how we edited the buildings layer, but we are also going to use the identify features tool to find out the name of the roads where each bus stop is located and add it to the tampere_bus_stops attribute table as we add points.

	- Select tampere_bus_stops in the layers panel

	- Toggle *Editing* on in the *Digitization Toolbar*

	- Find a red point on the georeferenced raster and select the tampere_roads layer in the layers panel.

	- Using the *Identify features* tool, click on a line feature in the tampere_roads layers where is the bus stop is located and scroll through the attributes until you find the name of the road

	- Next, select the tampere_bus_stops layer again. Choose *Add Point Feature* from the *Digitization Toolbar*. You don’t need to close the *Identify features* window to do this.

	- Click on the red dot in the georeferenced raster. This will add a point, and prompt you to add attributes for the fields. In ID enter numbers (1 for the first point, 2 for the second…) and the name of the road in road_locat. Press OK.

	- Repeat this for each bus stop.

	- *Save the Edits* in the Digitization Toolbar and toggle off *editing*.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/Exercise1/Exercise1_figure10.png)

---

### Map output

17. You’ve finished your edits. Remove the georeferenced raster (you no longer need it), and make a nice in-formative map. You can choose whether or not to include the Google Satellite data. Insert a scale bar to show the distances in the map, a North Arrow, and a title.
	- Hint: Look at the crash course exercise for instructions on how to make a map
	- Don't forget to change the symbology of your layers to your liking! 
	

# Time to get your hands dirty! Move on to the Crash Course exercise to get started with (Q)GIS. 
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJXSDNXNms3aEs0Rk9LYWJqIjp7In
N0YXJ0Ijo3NDAxLCJlbmQiOjc1ODUsInRleHQiOiIxMC4gWW91
IG1heSBuZWVkIHRvIGVuYWJsZSB0aGUgKkRpZ2l0aXppbmcgVG
9vbGJhciosIHdoaWNoIGVuYWJsZXMgeW91IHRvIGVkaXTigKYi
fSwia2RuODV2UGdsRFRHZVZ1eCI6eyJzdGFydCI6NjYyLCJlbm
QiOjY3MSwidGV4dCI6IkRhdGEgdXNlZCJ9LCJPSFc4dTRXalZj
Wk8wZnA1Ijp7InN0YXJ0Ijo4MDk5LCJlbmQiOjgxNTksInRleH
QiOiIhW10oaHR0cHM6Ly9kb2NzLnFnaXMub3JnLzMuMjgvZW4v
X2ltYWdlcy9tQWN0aW9uU2VsZWN0LnBuZykifSwiVkZQcVE3a2
5QYjZaaGhkWCI6eyJzdGFydCI6ODYzMiwiZW5kIjo4NjUzLCJ0
ZXh0IjoiKkFkZCBQb2x5Z29uIEZlYXR1cmUqIn0sImEzRWllbF
hha2RnY1g4TnkiOnsic3RhcnQiOjExMzQ5LCJlbmQiOjExNTQx
LCJ0ZXh0IjoiLSBVc2luZyB0aGUgKklkZW50aWZ5IGZlYXR1cm
VzKiB0b29sLCBjbGljayBvbiBhIGxpbmUgZmVhdHVyZSBpbiB0
aGUgdGFtcGVyZV9yb+KApiJ9LCJhMTJkS0d5ZVlQM3RMbFhEIj
p7InN0YXJ0Ijo2NzYsImVuZCI6Njg2LCJ0ZXh0IjoiQ29tcGxl
dGlvbiJ9fSwiY29tbWVudHMiOnsiaEJkOHZvVUFiWW9hS0VsQS
I6eyJkaXNjdXNzaW9uSWQiOiJXSDNXNms3aEs0Rk9LYWJqIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGludHJvZH
VjdGlvbiB0byB0aGlzIGluIHRoZW9yeSIsImNyZWF0ZWQiOjE2
ODYyMDUzOTk0MDl9LCJZeVJSZWg5TlJUSmRpbzFEIjp7ImRpc2
N1c3Npb25JZCI6Imtkbjg1dlBnbERUR2VWdXgiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBc2sgSm9uIGZvciB3aGF0IG
RhdGEgaGUgdXNlZCIsImNyZWF0ZWQiOjE2ODYyMDg3MjY2ODJ9
LCJxSWE2M1lPWFViZU5GdjlFIjp7ImRpc2N1c3Npb25JZCI6Ik
9IVzh1NFdqVmNaTzBmcDUiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJGaXggcGljdHVyZSIsImNyZWF0ZWQiOjE2ODYyOD
g2MTc5NjR9LCJ2VkxocHBzRTZTVDlENGsxIjp7ImRpc2N1c3Np
b25JZCI6IlZGUHFRN2tuUGI2WmhoZFgiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJEbyB3ZSB3YW50IHRvIGFkZCBwaWN0
b2dyYW1zIHRvIGFsbCBvZiB0aGVzZSBvciBkbyB3ZSB3YW50IH
RvIGNoYWxsZW5nZSB0aGVtIGEgYml0IGFuZCBsZXQgdGhlbSBz
ZWFyY2ggdGhlbXNlbHZlcz8iLCJjcmVhdGVkIjoxNjg2Mjg4Nz
MzMjUyfSwibFZoeER5SVB6VDVTc1IzRSI6eyJkaXNjdXNzaW9u
SWQiOiJhM0VpZWxYYWtkZ2NYOE55Iiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiUm9hZHMgZGF0YSBpbiBmb2xkZXIgaXMg
bWlzc2luZyBhdHRyaWJ1dGVzIiwiY3JlYXRlZCI6MTY4NjI4OT
E5NTY5OX0sImZZMmRVc212MjJWWnQwMHYiOnsiZGlzY3Vzc2lv
bklkIjoiYTEyZEtHeWVZUDN0TGxYRCIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IldyaXRlIHRoaXMgb3V0IGZ1cnRoZXIi
LCJjcmVhdGVkIjoxNjg2NDc2MzYwOTc2fX0sImhpc3RvcnkiOl
sxMTkyNTE1NTU3LDEzNTIzNzAyNzUsMzUxMTE5MTM3LDY5MDMy
OTE0OCwxMjkwOTg2ODUzLC0xMzE0OTMyNDkyXX0=
-->