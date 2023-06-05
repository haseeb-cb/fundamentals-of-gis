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

 7.  **Using the field we just created in the attribute table, explore the small areas of Helsinki**, which is the tiniest? How about the largest? By clicking on the attribute table on a certain row, for instance Viikki, you select that area and highlight in the map view. You can also select features with expression. Click open *Select features by expression*. 
 ![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_select_by_expression1.png)
 Alternatively you can find tools from the *Processing Toolbox*.
	 1. Open the *Field and Values* drop-down menu, which will show all the attribute fields
	 2. Double-click on the area field you made earlier (Area_km2)
	 3. Type "< 5" to the right of the field in the text field
	 4. Click *Select features*
	![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_select_by_expression.png)
Your selection now includes all the areas under 5 square kilometers in this layer, with selected objects shown in **yellow in on the map** and **blue on the attribute table**.
	Alternative expressions include:
 -  "Area_km2" = 5, select the features the area of which is exactly 5 square meters
 - "Area_km2" > 2 AND "Area_km2" < 5, select the features the area of which is between 2 and 5 square kilometers  

	5. Close the *Select by expression* window and deselect all the features by clicking *Deselect all* ![](https://docs.qgis.org/3.28/en/_images/mActionDeselectAll.png)

- Select features by expression picture 

 8. **Next, we’re going to create and calculate another field into the Helsinki_small_areas attribute table using the HSL_Helsinki_stops point data.** First open the *attribute table* of HSL_Helsinki_stops to familiarize yourself with its contents. The Boardings column depicts the amount of boardings on stops in Helsinki on average per day. We will calculate and visualize the public transit passenger numbers per area for every Helsinki small area.
	
	1. Check if the *Processing Toolbox* is active in the top right of the main QGIS window, if not open it by selecting *Processing* > *Toolbox* from the top of the window
	2. Type “Join attributes by location” into the search bar. Select the one that has (Summary) after it.
![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_join_attributes_by_location.png)
	3. The parameter window for the algorithm opens and here you have to specify what the algorithm does and with what data
	4. Set the follow values:
	- *Base layer*: Helsinki_small_areas
	- *Join layer*: HSL_Helsinki_stops
	- *Geometric predicate*: contains (What do you think the other options mean?)
	-  *Field to summarise*: Boardings
	- *Summaries to calculate*: *Sum*
	- *Discard records which could not be joined*: Yes
![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_join_attributes_by_location1.png)
	5. Click *Run*
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
dXRlIn0sImV2TFdZb0FHWDB5dXVJWHMiOnsic3RhcnQiOjE1MD
MwLCJlbmQiOjE1MDQ4LCJ0ZXh0IjoiUHJvY2Vzc2luZyBUb29s
Ym94In0sIkljZEZ0Z0pRYlBCTUdOakMiOnsic3RhcnQiOjE4OT
k2LCJlbmQiOjE5MDQ0LCJ0ZXh0IjoiY3R1cmUgb2YgY3VycmVu
dCBhdHRyaWJ1dGUgdGFibGUgd2l0aCBuZXcgZmllbGRzIn0sIl
BRWEprU3RZMmdzdXZ6NUQiOnsic3RhcnQiOjIwMDM0LCJlbmQi
OjIwMDU4LCJ0ZXh0IjoiLSBMYXlvdXQgbWFuYWdlciBwaWN0dX
JlIn0sImxTV2plN2dQNnJsSW5nYXkiOnsic3RhcnQiOjIwOTA3
LCJlbmQiOjIwOTE2LCJ0ZXh0IjoiTW92ZSBpdGVtIn0sIll5Wl
RhZFJwcEtyZTEyUFQiOnsic3RhcnQiOjIxMDE4LCJlbmQiOjIx
MDM1LCJ0ZXh0IjoiTW92ZSBpdGVtIGNvbnRlbnQifSwieW5oNW
JvUWlPTVRpbFpNVyI6eyJzdGFydCI6NzYsImVuZCI6MTk0LCJ0
ZXh0IjoiIVtDb3ZlciBwaWN0dXJlXShodHRwczovL3Jhdy5naX
RodWJ1c2VyY29udGVudC5jb20vcm93YW44ay9mdW5kYW1lbnRh
bHMtb2YtZ2lzL+KApiJ9LCIwT1lHek5lcDJhOW8xSEpZIjp7In
N0YXJ0Ijo1MzI5LCJlbmQiOjUzMjksInRleHQiOiJpY29uIHBp
Y3R1cmUifX0sImNvbW1lbnRzIjp7IlNSZnlLOHp2MHl3dndzZm
0iOnsiZGlzY3Vzc2lvbklkIjoicFZlMXQ0dHlOYkZ4UnBRTiIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCByZWNvbW
1lbmRhdGlvbnMgb24gbWFraW5nIGEgZm9sZGVyIGZvciBlYWNo
IHByYWN0aWNhbCIsImNyZWF0ZWQiOjE2ODU3ODMwMzkzNTd9LC
J1UEt0REpaWTVDQVVrd05BIjp7ImRpc2N1c3Npb25JZCI6Iksy
NGk4N3VzS21GWlVSSUoiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODU3ODMw
NDgzODl9LCJyeWNSdG15Z0lyeVpTZWQ2Ijp7ImRpc2N1c3Npb2
5JZCI6InVTVmw5bXZxMFEybjdUTEciLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJEdW1iIHRoaXMgZG93biBvciBleHBsYW
luIGl0IG1vcmUgdGhvcm91Z2hseSIsImNyZWF0ZWQiOjE2ODU3
ODMwNzE3NDB9LCI5UlpPQnRUaUNST242TTVyIjp7ImRpc2N1c3
Npb25JZCI6IldqUWdTbVZDVk8wWXZWOUIiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgbWVtZSIsImNyZWF0ZWQiOj
E2ODU3ODMwODM5NTF9LCJLSENWcDNzNE1EQ3YyV2l0Ijp7ImRp
c2N1c3Npb25JZCI6Ik44Y2hQZHpkSExxcHdLS04iLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJDb21lIGJhY2sgdG8gY2hl
Y2sgaWYgYWNjdXJhdGUiLCJjcmVhdGVkIjoxNjg1NzgzMjI4Nj
M3fSwiQlVXWURLOWhKc2RUVkpLeiI6eyJkaXNjdXNzaW9uSWQi
OiJ4ME42SXlMa2dwY1FpSjk5Iiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQ29ycmVjdCBsYXlvdXQiLCJjcmVhdGVkIjox
Njg1NzgzMjk0NjIxfSwiN1JFT2VIQW9aT1l1UkNiWSI6eyJkaX
NjdXNzaW9uSWQiOiJ6aW9TZFVkOHBjS0ZFQ25SIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiTWFrZSBzdHVkZW50cyBnYX
RoZXIgdGhlIGRhdGEgdGhlbXNlbHZlcyIsImNyZWF0ZWQiOjE2
ODU3ODM0OTA1MzN9LCJCTXhYR0kyWEJEb2lCVjVUIjp7ImRpc2
N1c3Npb25JZCI6Inppb1NkVWQ4cGNLRkVDblIiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJvciBhZGQgbGlua3MiLCJjcm
VhdGVkIjoxNjg1NzgzNTA2MTE3fSwiN1RoN1pZSkh1N0dnbDdh
cCI6eyJkaXNjdXNzaW9uSWQiOiJhYkRBMEVIazdPMjQzWDdkIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdl
IiwiY3JlYXRlZCI6MTY4NTc4MzU5MjczNH0sIkNIZlJWU3luSk
JMdlpKRVEiOnsiZGlzY3Vzc2lvbklkIjoiaGxoa2RDRW0zNGwz
VnJUVyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IldoYX
QgYXJlIG9iamVjdHM/IiwiY3JlYXRlZCI6MTY4NTc4MzYwNTAy
MX0sIm0wR0RKRlpBeEJqTHFzVUUiOnsiZGlzY3Vzc2lvbklkIj
oiRlhmUUZmRjlGWk9OcFlGYSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IldoYXQgaXMgYXR0cmlidXRlIGRhdGE/IiwiY3
JlYXRlZCI6MTY4NTc4MzYxNDAzN30sImtnSkVZRDZadlpyNDMw
R3UiOnsiZGlzY3Vzc2lvbklkIjoiZXZMV1lvQUdYMHl1dUlYcy
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbnRy
b2R1Y3Rpb24gdG8gdGhpcz8iLCJjcmVhdGVkIjoxNjg1Nzg2Nj
I4MDc2fSwiQVhjYlVXeHQ3N0dET3lYRiI6eyJkaXNjdXNzaW9u
SWQiOiJldkxXWW9BR1gweXV1SVhzIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiRWFybGllciBpbiBjcmFzaCBjb3Vyc2Us
IGFkZCBleGFtcGxlcyBvZiB0b29scyBhbmQgaG93IHRoZXkgd2
9yayIsImNyZWF0ZWQiOjE2ODU3ODc4OTkwNTl9LCJuNE5MY3h6
bVMwM090dk5RIjp7ImRpc2N1c3Npb25JZCI6IkljZEZ0Z0pRYl
BCTUdOakMiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg5NDM0MjkzfSwiMD
FDaUY4aUc4b3QzYWIxbiI6eyJkaXNjdXNzaW9uSWQiOiJQUVhK
a1N0WTJnc3V2ejVEIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc5MDMyMzgw
OX0sIm5DRDRHdW1vMTdMWWtjd2QiOnsiZGlzY3Vzc2lvbklkIj
oibFNXamU3Z1A2cmxJbmdheSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3OT
A1NjU2NTl9LCJxZEZFdm5iZUY1Y1VSNUFvIjp7ImRpc2N1c3Np
b25JZCI6Ill5WlRhZFJwcEtyZTEyUFQiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjox
Njg1NzkwNTg3MDkwfSwiNTdMWGpTekhzemFIY2hKVSI6eyJkaX
NjdXNzaW9uSWQiOiJ5bmg1Ym9RaU9NVGlsWk1XIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVXBkYXRlIGNvdmVyIHBpY3
R1cmUiLCJjcmVhdGVkIjoxNjg1OTQzNTg3MzU4fSwiUFZhYTJ5
ZHhUeThFQ3dUaiI6eyJkaXNjdXNzaW9uSWQiOiJXalFnU21WQ1
ZPMFl2VjlCIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
U3RyYWlnaHQgdG8gamFpbCIsImNyZWF0ZWQiOjE2ODU5NDQwNz
Q5NjV9LCJVdGpZSjdHY083RUU2eDdBIjp7ImRpc2N1c3Npb25J
ZCI6IjBPWUd6TmVwMmE5bzFISlkiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJnaXRodWIiLCJjcmVhdGVkIjoxNjg1OTQ0
OTczMzU4fSwiSW14bERrSUI1NFF1c211NSI6eyJkaXNjdXNzaW
9uSWQiOiJhYkRBMEVIazdPMjQzWDdkIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiZ2l0aHViIiwiY3JlYXRlZCI6MTY4NT
k0NTUzNDY2Mn0sIjNYNktIS1FyNzBKYUYyWXIiOnsiZGlzY3Vz
c2lvbklkIjoiSWNkRnRnSlFiUEJNR05qQyIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6ImdpdGh1YiIsImNyZWF0ZWQiOjE2
ODU5NDcxODQ4ODN9LCJKTU04aEc1MVMwSHdvS3o5Ijp7ImRpc2
N1c3Npb25JZCI6ImxTV2plN2dQNnJsSW5nYXkiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJnaXRodWIiLCJjcmVhdGVkIj
oxNjg1OTQ3ODM3NjQ3fSwiTDZHWUMzN1hOM3lKb2I1OCI6eyJk
aXNjdXNzaW9uSWQiOiJZeVpUYWRScHBLcmUxMlBUIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiZ2l0aHViIiwiY3JlYXRl
ZCI6MTY4NTk0Nzg0NDUzOX19LCJoaXN0b3J5IjpbMTAxNTQ3Mz
MxMCwyMzg1MzE0NDUsLTExNDY5NTE0MjEsMjAyMTk4ODA1Miwt
MTcyMzg5NDk5NCw4MzcyMzM3NywtMTkzODkxNjYxMiwxMjA4MD
czMDg1LC0yMDk4NzEwODQzLDE1MTQzNDc5MTksMTgzOTc4NjU5
NCwtMTYzNTc1MTYyNCwyNDY3NTAxOTAsMTQ5NzQ3MTAxNywxMj
Q1NDU3Mjk5LDEyMTc0MzY3NjIsNjgxMTg0ODc0LC0xODE5MDAx
ODcxLC00NzcwMDIyMzQsLTE2NDc1NjczNzJdfQ==
-->