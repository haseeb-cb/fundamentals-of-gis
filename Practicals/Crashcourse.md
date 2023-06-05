### Fundamentals of Geographic Information Systems (GIS)

# Crash Course



![Cover picture](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/CC-cover-placeholder.png)

[^1]: Image note

Rowan van der Kaaden

## Introduction to QGIS

### The contents of this exercise in a nutshell:

**The aim of this practical is to** get familiar with the QGIS software. The first practical exercises will introduce the QGIS graphical user interface (GUI) and its basic tools and features to create a foundation for the later practicals. After some basic introduction, you will create a choropleth map[^2].

[^2]: What is a choropleth map?

If you have time after that, try out the second part! They will introduce joining spreadsheet data with spatial data and vector clipping.

**By the end of today’s crash course, you will:**

-   **Be familiar with QGIS’s user interface and basic functions**
-   **Have an idea what kind of data types GIS can process**

**Note:** If you have not yet downloaded QGIS, do so now from this link: <https://www.qgis.org/en/site/forusers/download.html> See QGIS installation instructions for details.



## The basics of QGIS

### Getting started with QGIS

**First make sure you have downloaded the data zip containing the crash course data.** If you have not, download it using the link in Moodle and unzip the data.

**Launch QGIS** and the QGIS graphical user interface (GUI) opens (Figure 1).

-   Figure 1

Start by setting the **default language** in QGIS to English (if it isn’t already) by navigating to the language settings: *Settings menu* \> *Options* \> *General* \> *User Interface Translation*. Tick the “*Override system locale*” box and choose English from the dropdown menu and close the window by pressing OK. For the change to take effect, restart the application.

The state of a working session in QGIS is called a **project**. Similarly, to a e.g., a workspace in ArcGIS, a project is considered the ensemble of layers, projections, table relations and other properties, such as symbols and styles, of a specific session. Remember to save your projects often to prevent work from being lost in case of a crash. Also note that project files do not contain geospatial data, they merely contain information on where the program will find it.

*Here a few basic functions that are worth knowing before starting to play around with data and layers:*

![Save icon](https://docs.qgis.org/3.28/en/_images/mActionFileSave.png) **Saving in QGIS**: You can save your project by clicking either the *save* ![](https://docs.qgis.org/3.28/en/_images/mActionFileSave.png) or the *save as* icon. You can also use the keyboard shortcut *Ctrl + S* (or *Command + S*) or go to *Project* \> *Save*. The file format of a project file is \*.qgs

![](https://docs.qgis.org/3.28/en/_images/mActionFileNew.png) ![enter image description here](https://docs.qgis.org/3.28/en/_images/mActionFileOpen.png) **Creating and opening a project in QGIS:** If you want to start a new project, you can click on the *New* icon ![](https://docs.qgis.org/3.28/en/_images/mActionFileNew.png) with a blank page, or alternatively go to *Project* \> *New* or use the keyboard shortcut *Ctrl + N* (or Command + N). To open an already existing project, click on the folder-like *Open* icon ![enter image description here](https://docs.qgis.org/3.28/en/_images/mActionFileOpen.png) to pick up where you left off.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_project_CRS.PNG) **Changing the coordinate system of a project in QGIS:** You can see the current coordinate system of the project in the status bar in the lower right corner. You can change the coordinate system by clicking on the sign and selecting a new coordinate system from the list in the project properties window that pops open. You can access the same window also by going to *Project* \> *Properties* \> *CRS*. The default coordinate system in QGIS is set automatically to EPSG:4326 (WGS 84). You can change the default if you wish by going to *Settings* \> *Options* \> *CRS*. The data used in this course will mostly be in EPSG 3067 (ETRS-TM35FIN), which is the standard for nationwide data in Finland.

(QGIS supports ‘**on the fly**’ (**OTF**) coordinate system transformation for both vector and raster layers. This means that the program will automatically draw the layers to match the coordinate system defined for the map canvas, if a transformation formula is available.)

### 1.2 Tools, toolbars and panels

Here is a brief introduction to the **basic toolbars** in QGIS. The toolbars can be toggled in *View* \> *Toolbars* by ticking the boxes. If you can’t find a toolbar mentioned below – the toolbar might be deselected!

The **Map Navigation toolbar** lets you zoom and pan the map view.

![Map navigation toolbar](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_map_navigation_toolbar.PNG)

The **Attributes toolbar** includes some of the most common tools that enable for example **selecting** and **deselecting** features, **measuring lines** and getting access to the **attribute table** and **field calculator**.

![Attributes toolbar](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_attributes_toolbar.PNG)

 **Adding data in QGIS:** The **Data Source Manager** offers a handy way to add a vector or raster layer. There are also special buttons for different kinds of database layers and interface services. The figure on the below offers a closer look at the tool. Similar functionality can be found in *Layer* \> *Add Layer*.

![Data Source Manager](https://docs.qgis.org/3.28/en/_images/datasource_manager.png)

If you want to create new empty layers, go to *Layer* \> *Create Layer*.

**Panels** offer a single major function, like the Layers and Browser panels introduced above. Similarly, to toolbars, they can be toggled from *View* \> *Panels*. Below is an example of three panels (Browser, Layer Style and Statistics) on top of each other.

![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_panels.png)

### 1.3 Plugins

Only a fraction of all the possible tools and functions are visible in the default view of QGIS as a lot of functionality is done via **plugins**. You can manage plugins in the QGIS plugin manager: select *Plugins* \> *Manage* and install plugins. Here you can see what plugins are already installed to your repository and install new or update/uninstall current plugins.

![Plugins](https://docs.qgis.org/3.28/en/_images/plugin_details.png)

Let’s download a very handy plugin called **QuickMapServices**, which gives access to a wide selection of background maps.

1.  Select *Plugins* \> *Manage*
2.  Select *All* on the left menu and type “QuickMapServices” in the search bar
3.  Select the QuickMapServices plugin and *Install the plugin*
4.  You can find the newly installed plugin in the main QGIS window under *Web* \> *QuickMapServices*

(Hungry for more? Further reading on plugins in the QGIS manual: <https://docs.qgis.org/3.22/en/docs/user_manual/plugins/index.html>)

## 2 Warm-up exercise

### 2.1 Add and explore data

In order to get a proper touch of QGIS and how the different tools work, we will of course need data.

1.  Open the Data Source Manager (see 1.2)
2.  Select *Vector* from the menu
3.  Press the “…” button next to the *Vector Dataset(s)* field
4.  Navigate to the folder where you saved the data for this practical and select the following files from the folder (Click + Ctrl to select multiple items):
    
    1.  Helsinki_small_areas.shp
    2.  Helsinki_Municipality.shp
    3.  Helsinki_buildings.shp
    4.  HSL_helsinki_stops.shp
5.  Press *Open*
6.  Press *Add*

These data sets are all downloaded from PaITuli and Helsinki Region Infoshare data and map services, the data itself is produced by numerous entities (National Land Survey, Helsinki Regional Transport and the City of Helsinki). You can also add the Helsinki_roads.shp layer later for visualization purposes.

The shapefiles should now appear on the map canvas. Once you add the layers, the program should automatically change the project’s coordinate system to EPSG:3067, or more commonly, the ETRS89-TM35FIN (Transverse-Mercator) coordinate reference system, which is the proposed system for spatial data in Finland.

For a start, take your time to move around and get acquainted with the basic tools in QGIS. Try panning around and zooming in and out in the map view. If your layers “get lost” by mistake when zooming, simply right click on the layer you want to retrieve and select *Zoom to layer*.

**Whilst moving around, try out the following two tools:**

![](https://docs.qgis.org/3.28/en/_images/mActionIdentify.png) The **Identify Features** tool is essentially an info-tool that identifies the object(s) selected with it and lists the attribute data available for all the layers in that particular location. If you only want to look at information from a specific layer, use the drop-down menu to specify the layer you want to examine.

![](https://docs.qgis.org/3.28/en/_images/mActionMeasure.png) The **measure** tool can be used to make simple distance and area calculations on the map, as well as for measuring angles. The tool can calculate both the length of single line segments and the sum of all drawn lines. The measurement unit can be changed from the tool options.

Managing the **layers** is key in GIS. Right now, the added layers are arbitrarily symbolized and ordered, and do not come out very useful or informative. Thus, we need to get our hands dirty.

 1.  Start by **changing the order of the layers** by dragging them in the layers panel on the left side of the map view. A good order, for example, can be as follows from top to bottom: HSL_Helsinki_stops, Helsinki_buildings, Waterbodies, Helsinki_small_areas and Helsinki_Municipality.

 2.  You can also **change the visibility of the layers** by checking or unchecking the tick boxes next to the layer name or by adjusting **transparency**. The latter can be done under the *Style* tab in the *Layer properties* window, which can be accessed by right-clicking on the layer name and selecting *Properties*. This is also where you can change other style properties such as **symbol size and color**, **layer rendering** or create e.g. **choropleth maps**, but we will look into these in more detail later on.

 In addition to editing a layer’s style properties, the Layer properties window can also be used for e.g. examining the **layer’s general information** such as its coordinate system and source, adding **labels** to the map as well as managing **joins** and layer **metadata**.

 3.  Next, we want to **change the styles and the symbology of the layers**. You can navigate back to the *Symbology* tab in the *Layer Properties* window. The window looks slightly different depending on whether we have a raster or vector file, and what feature type is in question. You can see this for instance by comparing the style tabs of the HSL Stops (point feature) and Waterbodies (polygon feature) layers.
	 1.  Open the *symbology* properties for the Waterbodies layer
	 2. Apart from the color fill and a few ready-made styles, the main view does not offer very sophisticated visualizing options, so it is suggested to click on the *Simple fill*
![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_symbology1.png)
	 3. Press the *Fill color* button and change the color of the layer to blue
	 4. If you want a transparent fill, press on the arrow on the right of the *Fill* button and select Transparent fill
	 5. One you are satisfied with the layer styles, press *Apply* and *OK*
4. It is also possible to **visualize the layers based on the information stored in the attribute table**. This can be done by selecting Categorized or Graduated instead of Single Symbol from the dropdown menu on the top of the page.	
	
	1. Open the HSL_Helsinki_stops layer symbology
	2. Choose *Graduated* from the dropdown menu
	3. Choose "Boardings)" as the value from which the data is gathered
	4. Set the *Mode* to *Natural breaks (Jenks)* and press *Classify*
	5. Select a fitting *Color ramp* from the drop-down menu
	6. Press *Apply* and *OK*
![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_symbology2.png)

**Now, using the previous tips and tricks as your support, change the styles of all the layers in the project.**

 5.  Next, we shall move the focus from visualization to the **actual data**. Start by examining what data is included in the project and what information is stored in the layers by right clicking on the layer name and selecting *Open Attribute Table*.
	 1. Open the *attribute table* of the layer called Helsinki_small_areas. Take a moment to examine the table, what can you see?
	 As you can see, the file consists of a list of the small-sized areas within the city of Helsinki with their corresponding codes and creation dates but little else. Next, we are going to calculate the area for each small area of Helsinki. 
	 2.  In the *attribute table*, toggle *Editing mode* ![](https://docs.qgis.org/3.28/en/_images/mActionToggleEditing.png) and then click on the *Field Calculator* button ![](https://docs.qgis.org/3.28/en/_images/mActionCalculateField.png)
 - Field calculator picture
 6.  Now we’ll **write an expression that calculates the area of each small area of Helsinki in square kilometers**. On the right side of the Expression window is a list of drop-down menus.
	 1. Open the *Geometry* drop-down menu
	 2. Double-click the *\$area* expression (you can also type *\$area* in the blank *Expression window*)
	 3. Just the *\$area* expression would calculate the area in square meters, but we want square kilometers. So we will divide it by 1 000 000. Click or type the division symbol (/), and type 1000000 after the division
	 4. Set an informative *Output field name* (For example: Area_km2)
	 5. Set the *Output field type* to *Decimal number (real)*, and *Output field length* to 10 and 2 (try the other options and look how this changes the preview value)Click *OK*
	 6. Finally, click the *Save Edits* button ![](https://docs.qgis.org/3.28/en/_images/mActionSaveEdits.png) and disable *Editing* mode ![](https://docs.qgis.org/3.28/en/_images/mActionToggleEditing.png) to make the changes permanent

 7.  **Using the field we just created in the attribute table, explore the small areas of Helsinki**, which is the tiniest? How about the largest? By clicking on the attribute table on a certain row, for instance Viikki, you select that area and highlight in the map view. You can also select features with expression. Click open *Select features by expression*. Alternatively you can find tools from the *Processing Toolbox*.
	 1. Open the *Field and Values* drop-down menu, which will show all the attribute fields
	 2. Double-click on the area field you made earlier (Area_km2)
	 3. Type "< 5" to the right of the field in the text field
	 4. Click *Select features*
	
Your selection now includes all the areas under 5 square kilometers in this layer, with selected objects shown in **yellow in on the map** and **blue on the attribute table**.
	Alternative expressions include:
 -  "Area_km2" = 5, select the features the area of which is exactly 5 square meters
 - "Area_km2" > 2 AND "Area_km2" < 5, select the features the area of which is between 2 and 5 square kilometers  

	5. Close the *Select by expression* window and deselect all the features by clicking *Deselect all* ![](https://docs.qgis.org/3.28/en/_images/mActionDeselectAll.png)

- Select features by expression picture 

 8. **Next, we’re going to create and calculate another field into the Helsinki_small_areas attribute table using the HSL_Helsinki_stops point data.** First open the *attribute table* of HSL_Helsinki_stops to familiarize yourself with its contents. The Boardings column depicts the amount of boardings on stops in Helsinki on average per day. We will calculate and visualize the public transit passenger numbers per area for every Helsinki small area.
	
	1. Check if the *Processing Toolbox* is active in the top right of the main QGIS window, if not open it by selecting *Processing* > *Toolbox* from the top of the window
	2. Type “Join attributes by location” into the search bar. Select the one that has (Summary) after it.
	3. The parameter window for the algorithm opens and here you have to specify what the algorithm does and with what data
	4. Set the follow values:
	- *Base layer*: Helsinki_small_areas
	- *Join layer*: HSL_Helsinki_stops
	- *Geometric predicate*: contains (What do you think the other options mean?)
	-  *Field to summarise*: Boardings
	- *Summaries to calculate*: *Sum*
	- *Discard records which could not be joined*: Yes
	5. Click *Run*
- Join attributes by Location pictures

	6. A new temporary layer, Joined Layer, was created in the *Layers Panel* and by opening its *attribute table* you should see it’s similar to the Helsinki_small_areas attribute table, but with a new field, "Boardings_sum", which is the sum of all the passengers from every bus and train stop within that particular small area of Helsinki.
	7. Right-click the Joined Layer and select *Make permanent* to save the temporary scratch layer for further processing
	- Temporary layers will be lost when closing QGIS and are best not used for further processing
	8. Save the joined layer as ESRI Shapefile, with a sensible name (for example "Helsinki_small_areas_HSL.shp"), and within the folder for your project you made earlier
	9. Delete the temporary Joined Layer from the Layers window

9.   **Now we’ll calculate yet another field** using the *field calculator* by dividing the number of passengers by the square kilometer area of the Helsinki small areas.
		1.  Calculate this field using the *Field calculator* (don’t forget to toggle editing mode): output field name should be informative e.g. “PassArea”, set Output field type to decimal
		2. Set output *field length* to 10 and *precision* to 2
		3. Then you must enter the calculation into the Expression field, you can either use the drop-down menus (Fields and values) or simply type it in. The calculation should be similar to this (change if your fields are named differently): "Boardings_" / "Area_km2"
		4. Click OK. Remember to *Save edits* and *Disable editing mode*.
- Picture of current attribute table with new fields

10.  Head to the layer’s *symbology* tab and select **Graduated** from the drop-down menu. **Select the PassArea column as the data source and press Classify**. Choose a suitable classification method and visualize the data as desired. You can edit the class bounds and the legend values manually by double clicking on them. Which areas are the most passenger heavy and which are not? Why?

11. Now it is time for the finishing touches. To make the map easier to interpret, we are going to **add labels** to it.
		1. Right-click the layer we just visualized and go to *Layer properties* > *Labels*
		2. Select *Single labels* form the drop-down menu to enable labeling
		3. Choose the column from the list that contains the area names (name_fi)
		4. You can edit the lable placement and appearance, for example add a halo around it by selecting buffer in the lower section

### 2.2 Creating a map output in QGIS
The last phase of this practical will concentrate on creating a map output.
- Layout manager picture

1. In QGIS, the map layout is done in a separate window called a **Print layout**. Press on the *New Print layout* button ![](https://docs.qgis.org/3.28/en/_images/mActionNewLayout.png) in the *File toolbar* or go to *Project* > *New print layout*. Give a name for the composer in the opening window, and an empty map window should appear on the screen.

2. The next step is to add the content to the screen. Press the *Add new map* button ![](https://docs.qgis.org/3.28/en/_images/mActionNewMap.png) in the left side panel and drag from the corners to match the paper orientation. Now, you should see the same view as in the working view. If you want, you can change the paper orientation in the right-side *Composition panel* under the section *Paper and quality*.

	You can orientate in two ways in the composer: 
- To move the window, select *Move item* or press the keyboard shortcut **V** and drag as desired 
- To move the content on the map, select *Move item content* or press the keyboard shortcut C and drag as desired 

	NB! Remember, that **if you make changes in your working view, you need to press ***Refresh view*** ![](https://docs.qgis.org/3.28/en/_images/mActionRefresh.png) in order to see the changes in the print composer view!

3. A proper map should always have at least these three elements: a **north arrow**, a **scale bar** and a **legend**. All of these can be found in QGIS under the Layout-tab or the left hand-side toolbar in the Print layout. Add the mentioned elements to your map and visualize them as desired.
		
	1. ![](https://docs.qgis.org/3.28/en/_images/mActionLabel.png) **Adding a label**: You can change the default text as well as the font and colors of the label from the Item properties window in the lower right corner.
	2. ![](https://docs.qgis.org/3.28/en/_images/mActionScaleBar.png) **Adding a scale bar**: Click where you want to add it and customize it as desired. The size and the colors can be modified from the right-side Item properties panel.
	3. ![](https://docs.qgis.org/3.28/en/_images/mActionAddLegend.png) **Adding a legend**: You probably have to modify the legend a bit so that it looks informative on the map. The modification can be done from the Item properties. For example, delete the unnecessary items from your legend by clicking the minus symbol (tick the Auto update box off first).
	4. ![enter image description here](https://docs.qgis.org/3.28/en/_images/north_arrow.png) **Adding a North arrow or an image**: To do this, press Add North Arrow and click on the layout. If you want to modify the look of the arrow, go to Item properties and open the Search directories tab (see the picture on the right). Click on the desired arrow.

4. Once you are satisfied with your map, **save the project** and go to *Layout* > *Export as image* to **save your layout as an image file**. If you want to adjust the export resolution (default is 300 dpi, higher value = higher resolution image and larger file size), you can do that prior to exporting from the Layout panel. **Save your map under your course folder and submit the finished map on Moodle.**

(Hungry for more? furhter reading on the print composer in the QGIS manual: https://docs.qgis.org/3.22/en/docs/user_manual/print_composer/index.html

# Congratulations! You are now done with the first part of this Crash Course. How are you liking (Q)GIS so far?

## 3. Optional exercise
 
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJwVmUxdDR0eU5iRnhScFFOIjp7In
N0YXJ0IjoxMjA1LCJlbmQiOjEzNjUsInRleHQiOiIqKkZpcnN0
IG1ha2Ugc3VyZSB5b3UgaGF2ZSBkb3dubG9hZGVkIHRoZSBkYX
RhIHppcCBjb250YWluaW5nIHRoZSBjcmFzaCBjb3Vyc2XigKYi
fSwiSzI0aTg3dXNLbUZaVVJJSiI6eyJzdGFydCI6MTQ0NiwiZW
5kIjoxNDU4LCJ0ZXh0IjoiLSAgIEZpZ3VyZSAxIn0sInVTVmw5
bXZxMFEybjdUTEciOnsic3RhcnQiOjE4OTgsImVuZCI6MjMwOS
widGV4dCI6IlNpbWlsYXJseSwgdG8gYSBlLmcuLCBhIHdvcmtz
cGFjZSBpbiBBcmNHSVMsIGEgcHJvamVjdCBpcyBjb25zaWRlcm
VkIHRoZSBlbnNlbWLigKYifSwiV2pRZ1NtVkNWTzBZdlY5QiI6
eyJzdGFydCI6MjA5MywiZW5kIjoyMTgxLCJ0ZXh0IjoiUmVtZW
1iZXIgdG8gc2F2ZSB5b3VyIHByb2plY3RzIG9mdGVuIHRvIHBy
ZXZlbnQgd29yayBmcm9tIGJlaW5nIGxvc3QgaW4gY2FzZSBvZu
KApiJ9LCJOOGNoUGR6ZEhMcXB3S0tOIjp7InN0YXJ0Ijo0MTEy
LCJlbmQiOjQyMzgsInRleHQiOiJUaGUgZGF0YSB1c2VkIGluIH
RoaXMgY291cnNlIHdpbGwgbW9zdGx5IGJlIGluIEVQU0cgMzA2
NyAoRVRSUy1UTTM1RklOKSwgd2hpY2jigKYifSwieDBONkl5TG
tncGNRaUo5OSI6eyJzdGFydCI6NTg2MSwiZW5kIjo1OTA0LCJ0
ZXh0IjoiTGF5ZXJzIGFuZCBCcm93c2VyIHBhbmVscyBpbnRyb2
R1Y2VkIGFib3ZlLiJ9LCJ6aW9TZFVkOHBjS0ZFQ25SIjp7InN0
YXJ0Ijo3ODE5LCJlbmQiOjgxMjYsInRleHQiOiJUaGVzZSBkYX
RhIHNldHMgYXJlIGFsbCBkb3dubG9hZGVkIGZyb20gUGFJVHVs
aSBhbmQgSGVsc2lua2kgUmVnaW9uIEluZm9zaGFyZSBk4oCmIn
0sImFiREEwRUhrN08yNDNYN2QiOnsic3RhcnQiOjk3NzcsImVu
ZCI6OTc4OSwidGV4dCI6ImxheWVycyBwYW5lbCJ9LCJobGhrZE
NFbTM0bDNWclRXIjp7InN0YXJ0Ijo4OTI0LCJlbmQiOjg5MzAs
InRleHQiOiJvYmplY3QifSwiRlhmUUZmRjlGWk9OcFlGYSI6ey
JzdGFydCI6ODk2NSwiZW5kIjo4OTc0LCJ0ZXh0IjoiYXR0cmli
dXRlIn0sInNRRXBuRjM2N3NlYXZMc2MiOnsic3RhcnQiOjEzND
UzLCJlbmQiOjEzNDc3LCJ0ZXh0IjoiRmllbGQgY2FsY3VsYXRv
ciBwaWN0dXJlIn0sImV2TFdZb0FHWDB5dXVJWHMiOnsic3Rhcn
QiOjE0OTE1LCJlbmQiOjE0OTMzLCJ0ZXh0IjoiUHJvY2Vzc2lu
ZyBUb29sYm94In0sIlFnanFjSGsxV2VidmRRZFUiOnsic3Rhcn
QiOjE0ODQwLCJlbmQiOjE0ODY5LCJ0ZXh0IjoiU2VsZWN0IGZl
YXR1cmVzIGJ5IGV4cHJlc3Npb24ifSwiSEtYc0Njb0ZLRmY0ZX
hQUyI6eyJzdGFydCI6MTU3NjAsImVuZCI6MTU3OTksInRleHQi
OiItIFNlbGVjdCBmZWF0dXJlcyBieSBleHByZXNzaW9uIHBpY3
R1cmUifSwiY1U3UVhUVUJrWmlvNmd6TSI6eyJzdGFydCI6MTY5
NzAsImVuZCI6MTcwMDgsInRleHQiOiItIEpvaW4gYXR0cmlidX
RlcyBieSBMb2NhdGlvbiBwaWN0dXJlcyJ9LCJJY2RGdGdKUWJQ
Qk1HTmpDIjp7InN0YXJ0IjoxODU0NiwiZW5kIjoxODU5NCwidG
V4dCI6ImN0dXJlIG9mIGN1cnJlbnQgYXR0cmlidXRlIHRhYmxl
IHdpdGggbmV3IGZpZWxkcyJ9LCJQUVhKa1N0WTJnc3V2ejVEIj
p7InN0YXJ0IjoxOTU4NCwiZW5kIjoxOTYwOCwidGV4dCI6Ii0g
TGF5b3V0IG1hbmFnZXIgcGljdHVyZSJ9LCJsU1dqZTdnUDZybE
luZ2F5Ijp7InN0YXJ0IjoyMDQ1NywiZW5kIjoyMDQ2NiwidGV4
dCI6Ik1vdmUgaXRlbSJ9LCJZeVpUYWRScHBLcmUxMlBUIjp7In
N0YXJ0IjoyMDU2OCwiZW5kIjoyMDU4NSwidGV4dCI6Ik1vdmUg
aXRlbSBjb250ZW50In0sInluaDVib1FpT01UaWxaTVciOnsic3
RhcnQiOjc2LCJlbmQiOjE5NCwidGV4dCI6IiFbQ292ZXIgcGlj
dHVyZV0oaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY2
9tL3Jvd2FuOGsvZnVuZGFtZW50YWxzLW9mLWdpcy/igKYifSwi
ME9ZR3pOZXAyYTlvMUhKWSI6eyJzdGFydCI6NTMyOSwiZW5kIj
o1MzI5LCJ0ZXh0IjoiaWNvbiBwaWN0dXJlIn19LCJjb21tZW50
cyI6eyJTUmZ5Szh6djB5d3Z3c2ZtIjp7ImRpc2N1c3Npb25JZC
I6InBWZTF0NHR5TmJGeFJwUU4iLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgcmVjb21tZW5kYXRpb25zIG9uIG1ha2
luZyBhIGZvbGRlciBmb3IgZWFjaCBwcmFjdGljYWwiLCJjcmVh
dGVkIjoxNjg1NzgzMDM5MzU3fSwidVBLdERKWlk1Q0FVa3dOQS
I6eyJkaXNjdXNzaW9uSWQiOiJLMjRpODd1c0ttRlpVUklKIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cm
UiLCJjcmVhdGVkIjoxNjg1NzgzMDQ4Mzg5fSwicnljUnRteWdJ
cnlaU2VkNiI6eyJkaXNjdXNzaW9uSWQiOiJ1U1ZsOW12cTBRMm
43VExHIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRHVt
YiB0aGlzIGRvd24gb3IgZXhwbGFpbiBpdCBtb3JlIHRob3JvdW
dobHkiLCJjcmVhdGVkIjoxNjg1NzgzMDcxNzQwfSwiOVJaT0J0
VGlDUk9uNk01ciI6eyJkaXNjdXNzaW9uSWQiOiJXalFnU21WQ1
ZPMFl2VjlCIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIG1lbWUiLCJjcmVhdGVkIjoxNjg1NzgzMDgzOTUxfSwiS0
hDVnAzczRNREN2MldpdCI6eyJkaXNjdXNzaW9uSWQiOiJOOGNo
UGR6ZEhMcXB3S0tOIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQ29tZSBiYWNrIHRvIGNoZWNrIGlmIGFjY3VyYXRlIiwi
Y3JlYXRlZCI6MTY4NTc4MzIyODYzN30sIkJVV1lESzloSnNkVF
ZKS3oiOnsiZGlzY3Vzc2lvbklkIjoieDBONkl5TGtncGNRaUo5
OSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3
QgbGF5b3V0IiwiY3JlYXRlZCI6MTY4NTc4MzI5NDYyMX0sIjdS
RU9lSEFvWk9ZdVJDYlkiOnsiZGlzY3Vzc2lvbklkIjoiemlvU2
RVZDhwY0tGRUNuUiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6Ik1ha2Ugc3R1ZGVudHMgZ2F0aGVyIHRoZSBkYXRhIHRoZW
1zZWx2ZXMiLCJjcmVhdGVkIjoxNjg1NzgzNDkwNTMzfSwiQk14
WEdJMlhCRG9pQlY1VCI6eyJkaXNjdXNzaW9uSWQiOiJ6aW9TZF
VkOHBjS0ZFQ25SIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
Ijoib3IgYWRkIGxpbmtzIiwiY3JlYXRlZCI6MTY4NTc4MzUwNj
ExN30sIjdUaDdaWUpIdTdHZ2w3YXAiOnsiZGlzY3Vzc2lvbklk
IjoiYWJEQTBFSGs3TzI0M1g3ZCIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3
ODM1OTI3MzR9LCJDSGZSVlN5bkpCTHZaSkVRIjp7ImRpc2N1c3
Npb25JZCI6ImhsaGtkQ0VtMzRsM1ZyVFciLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJXaGF0IGFyZSBvYmplY3RzPyIsIm
NyZWF0ZWQiOjE2ODU3ODM2MDUwMjF9LCJtMEdESkZaQXhCakxx
c1VFIjp7ImRpc2N1c3Npb25JZCI6IkZYZlFGZkY5RlpPTnBZRm
EiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXaGF0IGlz
IGF0dHJpYnV0ZSBkYXRhPyIsImNyZWF0ZWQiOjE2ODU3ODM2MT
QwMzd9LCJFNkxEODgySGpnRzM5aHJFIjp7ImRpc2N1c3Npb25J
ZCI6InNRRXBuRjM2N3NlYXZMc2MiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1
Nzg1ODQyOTcxfSwia2dKRVlENlp2WnI0MzBHdSI6eyJkaXNjdX
NzaW9uSWQiOiJldkxXWW9BR1gweXV1SVhzIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGludHJvZHVjdGlvbiB0by
B0aGlzPyIsImNyZWF0ZWQiOjE2ODU3ODY2MjgwNzZ9LCJjVVBh
cFRsOWNIcUNjZFNrIjp7ImRpc2N1c3Npb25JZCI6IlFnanFjSG
sxV2VidmRRZFUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg2NjM3NDY4fS
wiQVhjYlVXeHQ3N0dET3lYRiI6eyJkaXNjdXNzaW9uSWQiOiJl
dkxXWW9BR1gweXV1SVhzIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiRWFybGllciBpbiBjcmFzaCBjb3Vyc2UsIGFkZCBl
eGFtcGxlcyBvZiB0b29scyBhbmQgaG93IHRoZXkgd29yayIsIm
NyZWF0ZWQiOjE2ODU3ODc4OTkwNTl9LCJsR3NSSUg2U2dpRWVU
ZEdHIjp7ImRpc2N1c3Npb25JZCI6IkhLWHNDY29GS0ZmNGV4UF
MiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1h
Z2UiLCJjcmVhdGVkIjoxNjg1Nzg4NjU3NDUyfSwidU5qS3MydX
dSVWE2QWdLTiI6eyJkaXNjdXNzaW9uSWQiOiJjVTdRWFRVQmta
aW82Z3pNIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIGltYWdlcyIsImNyZWF0ZWQiOjE2ODU3ODg2OTc0MzZ9LCJu
NE5MY3h6bVMwM090dk5RIjp7ImRpc2N1c3Npb25JZCI6IkljZE
Z0Z0pRYlBCTUdOakMiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg5NDM0Mj
kzfSwiMDFDaUY4aUc4b3QzYWIxbiI6eyJkaXNjdXNzaW9uSWQi
OiJQUVhKa1N0WTJnc3V2ejVEIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc5
MDMyMzgwOX0sIm5DRDRHdW1vMTdMWWtjd2QiOnsiZGlzY3Vzc2
lvbklkIjoibFNXamU3Z1A2cmxJbmdheSIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOj
E2ODU3OTA1NjU2NTl9LCJxZEZFdm5iZUY1Y1VSNUFvIjp7ImRp
c2N1c3Npb25JZCI6Ill5WlRhZFJwcEtyZTEyUFQiLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVh
dGVkIjoxNjg1NzkwNTg3MDkwfSwiNTdMWGpTekhzemFIY2hKVS
I6eyJkaXNjdXNzaW9uSWQiOiJ5bmg1Ym9RaU9NVGlsWk1XIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVXBkYXRlIGNvdm
VyIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg1OTQzNTg3MzU4fSwi
UFZhYTJ5ZHhUeThFQ3dUaiI6eyJkaXNjdXNzaW9uSWQiOiJXal
FnU21WQ1ZPMFl2VjlCIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiU3RyYWlnaHQgdG8gamFpbCIsImNyZWF0ZWQiOjE2OD
U5NDQwNzQ5NjV9LCJVdGpZSjdHY083RUU2eDdBIjp7ImRpc2N1
c3Npb25JZCI6IjBPWUd6TmVwMmE5bzFISlkiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJnaXRodWIiLCJjcmVhdGVkIjox
Njg1OTQ0OTczMzU4fSwiSW14bERrSUI1NFF1c211NSI6eyJkaX
NjdXNzaW9uSWQiOiJhYkRBMEVIazdPMjQzWDdkIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiZ2l0aHViIiwiY3JlYXRlZC
I6MTY4NTk0NTUzNDY2Mn0sIkdZb2VYT3FnV1Zvc1IzSVYiOnsi
ZGlzY3Vzc2lvbklkIjoic1FFcG5GMzY3c2VhdkxzYyIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6ImdpdGh1YiIsImNyZWF0
ZWQiOjE2ODU5NDYxMjA0MjB9LCJDR2tjcFFGYTJRTXZzYUlaIj
p7ImRpc2N1c3Npb25JZCI6IlFnanFjSGsxV2VidmRRZFUiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJnaXRodWIiLCJjcm
VhdGVkIjoxNjg1OTQ2NTIyNTAxfSwiYXBNUkhIYXRwNHdMT3BC
ciI6eyJkaXNjdXNzaW9uSWQiOiJIS1hzQ2NvRktGZjRleFBTIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiR2l0aHViIiwi
Y3JlYXRlZCI6MTY4NTk0NjY3Mzc3M30sIjJHS0Y0YXVUak5FU1
EydjAiOnsiZGlzY3Vzc2lvbklkIjoiY1U3UVhUVUJrWmlvNmd6
TSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6ImdpdGh1Yi
IsImNyZWF0ZWQiOjE2ODU5NDcxMDE1Mzl9LCIzWDZLSEtRcjcw
SmFGMllyIjp7ImRpc2N1c3Npb25JZCI6IkljZEZ0Z0pRYlBCTU
dOakMiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJnaXRo
dWIiLCJjcmVhdGVkIjoxNjg1OTQ3MTg0ODgzfSwiSk1NOGhHNT
FTMEh3b0t6OSI6eyJkaXNjdXNzaW9uSWQiOiJsU1dqZTdnUDZy
bEluZ2F5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiZ2
l0aHViIiwiY3JlYXRlZCI6MTY4NTk0NzgzNzY0N30sIkw2R1lD
MzdYTjN5Sm9iNTgiOnsiZGlzY3Vzc2lvbklkIjoiWXlaVGFkUn
BwS3JlMTJQVCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
ImdpdGh1YiIsImNyZWF0ZWQiOjE2ODU5NDc4NDQ1Mzl9fSwiaG
lzdG9yeSI6WzIwNjcyMzkzMDksMjM4NTMxNDQ1LC0xMTQ2OTUx
NDIxLDIwMjE5ODgwNTIsLTE3MjM4OTQ5OTQsODM3MjMzNzcsLT
E5Mzg5MTY2MTIsMTIwODA3MzA4NSwtMjA5ODcxMDg0MywxNTE0
MzQ3OTE5LDE4Mzk3ODY1OTQsLTE2MzU3NTE2MjQsMjQ2NzUwMT
kwLDE0OTc0NzEwMTcsMTI0NTQ1NzI5OSwxMjE3NDM2NzYyLDY4
MTE4NDg3NCwtMTgxOTAwMTg3MSwtNDc3MDAyMjM0LC0xNjQ3NT
Y3MzcyXX0=
-->