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

 7.  **Using the field we just created in the attribute table, explore the small areas of Helsinki**, which is the tiniest? How about the largest? By clicking on the attribute table on a certain row, for instance Viikki, you select that area and highlight in the map view. You can also select features with expression. Click open *Select features by expression*.Alternatively you can find tools from the *Processing Toolbox*.
![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_select_by_expression1.png)
 
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

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_attribute_table.png)

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
- To move the window, select *Move item* ![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_move_item.png) or press the keyboard shortcut **V** and drag as desired 
- To move the content on the map, select *Move item content* ![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/QGIS_move_item_content.png) or press the keyboard shortcut C and drag as desired 

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
Q4LCJlbmQiOjE1MDQ4LCJ0ZXh0IjoiUHJvY2Vzc2luZyBUb29s
Ym94In0sIlBRWEprU3RZMmdzdXZ6NUQiOnsic3RhcnQiOjIwMD
g2LCJlbmQiOjIwMTEwLCJ0ZXh0IjoiLSBMYXlvdXQgbWFuYWdl
ciBwaWN0dXJlIn0sInluaDVib1FpT01UaWxaTVciOnsic3Rhcn
QiOjc2LCJlbmQiOjE5NCwidGV4dCI6IiFbQ292ZXIgcGljdHVy
ZV0oaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL3
Jvd2FuOGsvZnVuZGFtZW50YWxzLW9mLWdpcy/igKYifSwiME9Z
R3pOZXAyYTlvMUhKWSI6eyJzdGFydCI6NTMyOSwiZW5kIjo1Mz
I5LCJ0ZXh0IjoiaWNvbiBwaWN0dXJlIn19LCJjb21tZW50cyI6
eyJTUmZ5Szh6djB5d3Z3c2ZtIjp7ImRpc2N1c3Npb25JZCI6In
BWZTF0NHR5TmJGeFJwUU4iLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgcmVjb21tZW5kYXRpb25zIG9uIG1ha2luZy
BhIGZvbGRlciBmb3IgZWFjaCBwcmFjdGljYWwiLCJjcmVhdGVk
IjoxNjg1NzgzMDM5MzU3fSwidVBLdERKWlk1Q0FVa3dOQSI6ey
JkaXNjdXNzaW9uSWQiOiJLMjRpODd1c0ttRlpVUklKIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLC
JjcmVhdGVkIjoxNjg1NzgzMDQ4Mzg5fSwicnljUnRteWdJcnla
U2VkNiI6eyJkaXNjdXNzaW9uSWQiOiJ1U1ZsOW12cTBRMm43VE
xHIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRHVtYiB0
aGlzIGRvd24gb3IgZXhwbGFpbiBpdCBtb3JlIHRob3JvdWdobH
kiLCJjcmVhdGVkIjoxNjg1NzgzMDcxNzQwfSwiOVJaT0J0VGlD
Uk9uNk01ciI6eyJkaXNjdXNzaW9uSWQiOiJXalFnU21WQ1ZPMF
l2VjlCIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRk
IG1lbWUiLCJjcmVhdGVkIjoxNjg1NzgzMDgzOTUxfSwiS0hDVn
AzczRNREN2MldpdCI6eyJkaXNjdXNzaW9uSWQiOiJOOGNoUGR6
ZEhMcXB3S0tOIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQ29tZSBiYWNrIHRvIGNoZWNrIGlmIGFjY3VyYXRlIiwiY3Jl
YXRlZCI6MTY4NTc4MzIyODYzN30sIkJVV1lESzloSnNkVFZKS3
oiOnsiZGlzY3Vzc2lvbklkIjoieDBONkl5TGtncGNRaUo5OSIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QgbG
F5b3V0IiwiY3JlYXRlZCI6MTY4NTc4MzI5NDYyMX0sIjdSRU9l
SEFvWk9ZdVJDYlkiOnsiZGlzY3Vzc2lvbklkIjoiemlvU2RVZD
hwY0tGRUNuUiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
Ik1ha2Ugc3R1ZGVudHMgZ2F0aGVyIHRoZSBkYXRhIHRoZW1zZW
x2ZXMiLCJjcmVhdGVkIjoxNjg1NzgzNDkwNTMzfSwiQk14WEdJ
MlhCRG9pQlY1VCI6eyJkaXNjdXNzaW9uSWQiOiJ6aW9TZFVkOH
BjS0ZFQ25SIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
b3IgYWRkIGxpbmtzIiwiY3JlYXRlZCI6MTY4NTc4MzUwNjExN3
0sIjdUaDdaWUpIdTdHZ2w3YXAiOnsiZGlzY3Vzc2lvbklkIjoi
YWJEQTBFSGs3TzI0M1g3ZCIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODM1
OTI3MzR9LCJDSGZSVlN5bkpCTHZaSkVRIjp7ImRpc2N1c3Npb2
5JZCI6ImhsaGtkQ0VtMzRsM1ZyVFciLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJXaGF0IGFyZSBvYmplY3RzPyIsImNyZW
F0ZWQiOjE2ODU3ODM2MDUwMjF9LCJtMEdESkZaQXhCakxxc1VF
Ijp7ImRpc2N1c3Npb25JZCI6IkZYZlFGZkY5RlpPTnBZRmEiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXaGF0IGlzIGF0
dHJpYnV0ZSBkYXRhPyIsImNyZWF0ZWQiOjE2ODU3ODM2MTQwMz
d9LCJrZ0pFWUQ2WnZacjQzMEd1Ijp7ImRpc2N1c3Npb25JZCI6
ImV2TFdZb0FHWDB5dXVJWHMiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgaW50cm9kdWN0aW9uIHRvIHRoaXM/Iiwi
Y3JlYXRlZCI6MTY4NTc4NjYyODA3Nn0sIkFYY2JVV3h0NzdHRE
95WEYiOnsiZGlzY3Vzc2lvbklkIjoiZXZMV1lvQUdYMHl1dUlY
cyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkVhcmxpZX
IgaW4gY3Jhc2ggY291cnNlLCBhZGQgZXhhbXBsZXMgb2YgdG9v
bHMgYW5kIGhvdyB0aGV5IHdvcmsiLCJjcmVhdGVkIjoxNjg1Nz
g3ODk5MDU5fSwiMDFDaUY4aUc4b3QzYWIxbiI6eyJkaXNjdXNz
aW9uSWQiOiJQUVhKa1N0WTJnc3V2ejVEIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6
MTY4NTc5MDMyMzgwOX0sIjU3TFhqU3pIc3phSGNoSlUiOnsiZG
lzY3Vzc2lvbklkIjoieW5oNWJvUWlPTVRpbFpNVyIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlVwZGF0ZSBjb3ZlciBwaW
N0dXJlIiwiY3JlYXRlZCI6MTY4NTk0MzU4NzM1OH0sIlBWYWEy
eWR4VHk4RUN3VGoiOnsiZGlzY3Vzc2lvbklkIjoiV2pRZ1NtVk
NWTzBZdlY5QiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IlN0cmFpZ2h0IHRvIGphaWwiLCJjcmVhdGVkIjoxNjg1OTQ0MD
c0OTY1fSwiVXRqWUo3R2NPN0VFNng3QSI6eyJkaXNjdXNzaW9u
SWQiOiIwT1lHek5lcDJhOW8xSEpZIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiZ2l0aHViIiwiY3JlYXRlZCI6MTY4NTk0
NDk3MzM1OH0sIklteGxEa0lCNTRRdXNtdTUiOnsiZGlzY3Vzc2
lvbklkIjoiYWJEQTBFSGs3TzI0M1g3ZCIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6ImdpdGh1YiIsImNyZWF0ZWQiOjE2OD
U5NDU1MzQ2NjJ9fSwiaGlzdG9yeSI6Wy0xNDY5MzEyOTQwLDIz
ODUzMTQ0NSwtMTE0Njk1MTQyMSwyMDIxOTg4MDUyLC0xNzIzOD
k0OTk0LDgzNzIzMzc3LC0xOTM4OTE2NjEyLDEyMDgwNzMwODUs
LTIwOTg3MTA4NDMsMTUxNDM0NzkxOSwxODM5Nzg2NTk0LC0xNj
M1NzUxNjI0LDI0Njc1MDE5MCwxNDk3NDcxMDE3LDEyNDU0NTcy
OTksMTIxNzQzNjc2Miw2ODExODQ4NzQsLTE4MTkwMDE4NzEsLT
Q3NzAwMjIzNCwtMTY0NzU2NzM3Ml19
-->