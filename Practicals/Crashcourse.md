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

**Changing the coordinate system of a project in QGIS:** You can see the current coordinate system of the project in the status bar in the lower right corner. You can change the coordinate system by clicking on the sign and selecting a new coordinate system from the list in the project properties window that pops open. You can access the same window also by going to *Project* \> *Properties* \> *CRS*. The default coordinate system in QGIS is set automatically to EPSG:4326 (WGS 84). You can change the default if you wish by going to *Settings* \> *Options* \> *CRS*. The data used in this course will mostly be in EPSG 3067 (ETRS-TM35FIN), which is the standard for nationwide data in Finland.

(QGIS supports ‘**on the fly**’ (**OTF**) coordinate system transformation for both vector and raster layers. This means that the program will automatically draw the layers to match the coordinate system defined for the map canvas, if a transformation formula is available.)

### 1.2 Tools, toolbars and panels

Here is a brief introduction to the **basic toolbars** in QGIS. The toolbars can be toggled in *View* \> *Toolbars* by ticking the boxes. If you can’t find a toolbar mentioned below – the toolbar might be deselected!

The **Map Navigation toolbar** lets you zoom and pan the map view.

-   Picture of map navigation toolbar

The **Attributes toolbar** includes some of the most common tools that enable for example **selecting** and **deselecting** features, **measuring lines** and getting access to the **attribute table** and **field calculator**.

-   Picture of attributes toolbar

(picture **Adding data in QGIS:** The **Data Source Manager** offers a handy way to add a vector or raster layer. There are also special buttons for different kinds of database layers and interface services. The figure on the right offers a closer look at the tool. Similar functionality can be found in *Layer* \> *Add Layer*.

If you want to create new empty layers, go to *Layer* \> *Create Layer*.

**Panels** offer a single major function, like the Layers and Browser panels introduced above. Similarly, to toolbars, they can be toggled from *View* \> *Panels*. On the left is an example of three panels (Browser, Layer Style and Layers) on top of each other.

### 1.3 Plugins

Only a fraction of all the possible tools and functions are visible in the default view of QGIS as a lot of functionality is done via **plugins**. You can manage plugins in the QGIS plugin manager: select *Plugins* \> *Manage* and install plugins. Here you can see what plugins are already installed to your repository and install new or update/uninstall current plugins.

-   Example image of plugin

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

The **Identify Features** tool is essentially an info-tool that identifies the object(s) selected with it and lists the attribute data available for all the layers in that particular location. If you only want to look at information from a specific layer, use the drop-down menu to specify the layer you want to examine.

The **measure** tool can be used to make simple distance and area calculations on the map, as well as for measuring angles. The tool can calculate both the length of single line segments and the sum of all drawn lines. The measurement unit can be changed from the tool options.

Managing the **layers** is key in GIS. Right now, the added layers are arbitrarily symbolized and ordered, and do not come out very useful or informative. Thus, we need to get our hands dirty.

 1.  Start by **changing the order of the layers** by dragging them in the layers panel on the left side of the map view. A good order, for example, can be as follows from top to bottom: HSL_Helsinki_stops, Helsinki_buildings, Waterbodies, Helsinki_small_areas and Helsinki_Municipality.

 2.  You can also **change the visibility of the layers** by checking or unchecking the tick boxes next to the layer name or by adjusting **transparency**. The latter can be done under the *Style* tab in the *Layer properties* window, which can be accessed by right-clicking on the layer name and selecting *Properties*. This is also where you can change other style properties such as **symbol size and color**, **layer rendering** or create e.g. **choropleth maps**, but we will look into these in more detail later on.

 In addition to editing a layer’s style properties, the Layer properties window can also be used for e.g. examining the **layer’s general information** such as its coordinate system and source, adding **labels** to the map as well as managing **joins** and layer **metadata**.

 3.  Next, we want to **change the styles and the symbology of the layers**. You can navigate back to the *Symbology* tab in the *Layer Properties* window. The window looks slightly different depending on whether we have a raster or vector file, and what feature type is in question. You can see this for instance by comparing the style tabs of the HSL Stops (point feature) and Waterbodies (polygon feature) layers.
	 1.  Open the *symbology* properties for the Waterbodies layer
	 2. Apart from the color fill and a few ready-made styles, the main view does not offer very sophisticated visualizing options, so it is suggested to click on the *Simple fill*
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
 - Symbology example picture

**Now, using the previous tips and tricks as your support, change the styles of all the layers in the project.**

 5.  Next, we shall move the focus from visualization to the **actual data**. Start by examining what data is included in the project and what information is stored in the layers by right clicking on the layer name and selecting *Open Attribute Table*.
	 1. Open the *attribute table* of the layer called Helsinki_small_areas. Take a moment to examine the table, what can you see?
	 As you can see, the file consists of a list of the small-sized areas within the city of Helsinki with their corresponding codes and creation dates but little else. Next, we are going to calculate the area for each small area of Helsinki. 
	 2.  In the *attribute table*, toggle *Editing mode* and then click on the *Field Calculator* button
 - Field calculator picture
 6.  Now we’ll **write an expression that calculates the area of each small area of Helsinki in square kilometers**. On the right side of the Expression window is a list of drop-down menus.
	 1. Open the *Geometry* drop-down menu
	 2. Double-click the *\$area* expression (you can also type *\$area* in the blank *Expression window*)
	 3. Just the *\$area* expression would calculate the area in square meters, but we want square kilometers. So we will divide it by 1 000 000. Click or type the division symbol (/), and type 1000000 after the division
	 4. Set an informative *Output field name* (For example: Area_km2)
	 5. Set the *Output field type* to *Decimal number (real)*, and *Output field length* to 10 and 2 (try the other options and look how this changes the preview value)Click *OK*
	 6. Finally, click the *Save Edits* button and disable *Editing* mode to make the changes permanent

 7.  **Using the field we just created in the attribute table, explore the small areas of Helsinki**, which is the tiniest? How about the largest? By clicking on the attribute table on a certain row, for instance Viikki, you select that area and highlight in the map view. You can also select features with expression. Click open *Select features by expression*. Alternatively you can find tools from the *Processing Toolbox*.
	 1. Open the *Field and Values* drop-down menu, which will show all the attribute fields
	 2. Double-click on the area field you made earlier (Area_km2)
	 3. Type "< 5" to the right of the field in the text field
	 4. Click *Select features*
	
Your selection now includes all the areas under 5 square kilometers in this layer, with selected objects shown in **yellow in on the map** and **blue on the attribute table**.
	Alternative expressions include:
 -  "Area_km2" = 5, select the features the area of which is exactly 5 square meters
 - "Area_km2" > 2 AND "Area_km2" < 5, select the features the area of which is between 2 and 5 square kilometers  

	5. Close the *Select by expression* window and deselect all the features by clicking *Deselect all* 

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

1. In QGIS, the map layout is done in a separate window called a **Print layout**. Press on the *New Print layout* button in the *File toolbar* or go to *Project* > *New print layout*. Give a name for the composer in the opening window, and an empty map window should appear on the screen.

2. The next step is to add the content to the screen. Press the **Add new map button** in the left side panel and drag from the corners to match the paper orientation. Now, you should see the same view as in the working view. If you want, you can change the paper orientation in the right-side *Composition panel* under the section *Paper and quality*.

	You can orientate in two ways in the composer: 
- To move the window, select *Move item* or press the keyboard shortcut **V** and drag as desired 
- To move the content on the map, select *Move item content* or press the keyboard shortcut C and drag as desired 

	NB! Remember, that **if you make changes in your working view, you need to press *Update preview / Refresh view*** in order to see the changes in the print composer view!

3. A proper map should always have at least these three elements: a **north arrow**, a **scale bar** and a **legend**. All of these can be found in QGIS under the Layout-tab or the left hand-side toolbar in the Print layout. Add the mentioned elements to your map and visualize them as desired.
		
	1. **Adding a label**: You can change the default text as well as the font and colors of the label from the Item properties window in the lower right corner.
	2. **Adding a scale bar**: Click where you want to add it and customize it as desired. The size and the colors can be modified from the right-side Item properties panel.
	3. **Adding a legend**: You probably have to modify the legend a bit so that it looks informative on the map. The modification can be done from the Item properties. For example, delete the unnecessary items from your legend by clicking the minus symbol (tick the Auto update box off first).
	4. **Adding a North arrow or an image**: To do this, press Add North Arrow and click on the layout. If you want to modify the look of the arrow, go to Item properties and open the Search directories tab (see the picture on the right). Click on the desired arrow.
	5. **Adding a legend**: You probably have to modify the legend a bit so that it looks informative on the map. The modification can be done from the Item properties. For example, delete the unnecessary items from your legend by clicking the minus symbol (tick the Auto update box off first).
	6. **Adding a North arrow or an image**: To do this, press Add North Arrow and click on the layout.
If you want to modify the look of the arrow, go to Item properties and open the Search directories tab (see the picture on the right). Click on the desired arrow.

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
KApiJ9LCJJbkk0elpyUk40TVRSYUIzIjp7InN0YXJ0IjozNDM4
LCJlbmQiOjM0OTQsInRleHQiOiIqKkNoYW5naW5nIHRoZSBjb2
9yZGluYXRlIHN5c3RlbSBvZiBhIHByb2plY3QgaW4gUUdJUzoq
KiJ9LCJOOGNoUGR6ZEhMcXB3S0tOIjp7InN0YXJ0Ijo0MDEwLC
JlbmQiOjQxMzYsInRleHQiOiJUaGUgZGF0YSB1c2VkIGluIHRo
aXMgY291cnNlIHdpbGwgbW9zdGx5IGJlIGluIEVQU0cgMzA2Ny
AoRVRSUy1UTTM1RklOKSwgd2hpY2jigKYifSwiOFJBNmRlbElZ
bXkxUXBtUiI6eyJzdGFydCI6NDc0MCwiZW5kIjo0NzczLCJ0ZX
h0IjoiUGljdHVyZSBvZiBtYXAgbmF2aWdhdGlvbiB0b29sYmFy
In0sInBjaU9nZ3V3RmlCNnNVVUYiOnsic3RhcnQiOjUwMDYsIm
VuZCI6NTAzNSwidGV4dCI6IlBpY3R1cmUgb2YgYXR0cmlidXRl
cyB0b29sYmFyIn0sInFFM0NYeDBsSDRJN3VrQTQiOnsic3Rhcn
QiOjUyNDksImVuZCI6NTI1NSwidGV4dCI6ImZpZ3VyZSJ9LCJ4
ME42SXlMa2dwY1FpSjk5Ijp7InN0YXJ0Ijo1NDkxLCJlbmQiOj
U1MzQsInRleHQiOiJMYXllcnMgYW5kIEJyb3dzZXIgcGFuZWxz
IGludHJvZHVjZWQgYWJvdmUuIn0sIm9UOXhlNnF3dlVVcmY3Qm
8iOnsic3RhcnQiOjU2MDQsImVuZCI6NTcwMSwidGV4dCI6Ik9u
IHRoZSBsZWZ0IGlzIGFuIGV4YW1wbGUgb2YgdGhyZWUgcGFuZW
xzIChCcm93c2VyLCBMYXllciBTdHlsZSBhbmQgTGF5ZXJzKSBv
buKApiJ9LCJqdFhtUndxZFl5Q2c4NmZhIjp7InN0YXJ0Ijo2MD
k3LCJlbmQiOjYxMjAsInRleHQiOiJFeGFtcGxlIGltYWdlIG9m
IHBsdWdpbiJ9LCJ6aW9TZFVkOHBjS0ZFQ25SIjp7InN0YXJ0Ij
o3Mjg0LCJlbmQiOjc1OTEsInRleHQiOiJUaGVzZSBkYXRhIHNl
dHMgYXJlIGFsbCBkb3dubG9hZGVkIGZyb20gUGFJVHVsaSBhbm
QgSGVsc2lua2kgUmVnaW9uIEluZm9zaGFyZSBk4oCmIn0sIk13
OUFneHBnZU83ZzFQb1AiOnsic3RhcnQiOjgyNTMsImVuZCI6OD
I3MCwidGV4dCI6IklkZW50aWZ5IEZlYXR1cmVzIn0sIjU4eExr
d2UwcHJQODE1VlQiOnsic3RhcnQiOjg1NzUsImVuZCI6ODU4Mi
widGV4dCI6Im1lYXN1cmUifSwiYWJEQTBFSGs3TzI0M1g3ZCI6
eyJzdGFydCI6OTExNywiZW5kIjo5MTI5LCJ0ZXh0IjoibGF5ZX
JzIHBhbmVsIn0sImhsaGtkQ0VtMzRsM1ZyVFciOnsic3RhcnQi
OjgzMjYsImVuZCI6ODMzMiwidGV4dCI6Im9iamVjdCJ9LCJGWG
ZRRmZGOUZaT05wWUZhIjp7InN0YXJ0Ijo4MzY3LCJlbmQiOjgz
NzYsInRleHQiOiJhdHRyaWJ1dGUifSwiSTh5eEFEYzYzU2tPZ0
QzeSI6eyJzdGFydCI6MTE2MTUsImVuZCI6MTE2MzksInRleHQi
OiJTeW1ib2xvZ3kgZXhhbXBsZSBwaWN0dXIifSwiOVlKTnU4bz
h1b3ViWUNnaCI6eyJzdGFydCI6MTI0MTgsImVuZCI6MTI0MjUs
InRleHQiOiJFZGl0aW5nIn0sIk54SmRGV0NCbFVzMjRzY0wiOn
sic3RhcnQiOjEyNDU1LCJlbmQiOjEyNDYwLCJ0ZXh0IjoiRmll
bGQifSwic1FFcG5GMzY3c2VhdkxzYyI6eyJzdGFydCI6MTI0OD
MsImVuZCI6MTI1MDcsInRleHQiOiJGaWVsZCBjYWxjdWxhdG9y
IHBpY3R1cmUifSwiQWNXVEprbXI5YWtudzJRViI6eyJzdGFydC
I6MTMzNjIsImVuZCI6MTMzNjksInRleHQiOiJFZGl0aW5nIn0s
IjNYVWloVHJnTlRYbmxycDMiOnsic3RhcnQiOjEzMzMwLCJlbm
QiOjEzMzQwLCJ0ZXh0IjoiU2F2ZSBFZGl0cyJ9LCJldkxXWW9B
R1gweXV1SVhzIjp7InN0YXJ0IjoxMzgxMywiZW5kIjoxMzgzMS
widGV4dCI6IlByb2Nlc3NpbmcgVG9vbGJveCJ9LCJRZ2pxY0hr
MVdlYnZkUWRVIjp7InN0YXJ0IjoxMzczOCwiZW5kIjoxMzc2Ny
widGV4dCI6IlNlbGVjdCBmZWF0dXJlcyBieSBleHByZXNzaW9u
In0sIkhUQmo1TkFpamppUEhuZHYiOnsic3RhcnQiOjE0NTc3LC
JlbmQiOjE0NTg5LCJ0ZXh0IjoiRGVzZWxlY3QgYWxsIn0sIkhL
WHNDY29GS0ZmNGV4UFMiOnsic3RhcnQiOjE0NTkzLCJlbmQiOj
E0NjMyLCJ0ZXh0IjoiLSBTZWxlY3QgZmVhdHVyZXMgYnkgZXhw
cmVzc2lvbiBwaWN0dXJlIn0sImNVN1FYVFVCa1ppbzZnek0iOn
sic3RhcnQiOjE1ODAzLCJlbmQiOjE1ODQxLCJ0ZXh0IjoiLSBK
b2luIGF0dHJpYnV0ZXMgYnkgTG9jYXRpb24gcGljdHVyZXMifS
wiSWNkRnRnSlFiUEJNR05qQyI6eyJzdGFydCI6MTczNzksImVu
ZCI6MTc0MjcsInRleHQiOiJjdHVyZSBvZiBjdXJyZW50IGF0dH
JpYnV0ZSB0YWJsZSB3aXRoIG5ldyBmaWVsZHMifSwiUFFYSmtT
dFkyZ3N1dno1RCI6eyJzdGFydCI6MTg0MTcsImVuZCI6MTg0ND
EsInRleHQiOiItIExheW91dCBtYW5hZ2VyIHBpY3R1cmUifSwi
TEVHVGxNNVEzV2h0Z2FQWCI6eyJzdGFydCI6MTg1NDAsImVuZC
I6MTg1NTYsInRleHQiOiJOZXcgUHJpbnQgbGF5b3V0In0sIk92
N2RTYXd0N2lMaEFmRXIiOnsic3RhcnQiOjE4ODAwLCJlbmQiOj
E4ODE4LCJ0ZXh0IjoiQWRkIG5ldyBtYXAgYnV0dG9uIn0sImxT
V2plN2dQNnJsSW5nYXkiOnsic3RhcnQiOjE5MTY3LCJlbmQiOj
E5MTc2LCJ0ZXh0IjoiTW92ZSBpdGVtIn0sIll5WlRhZFJwcEty
ZTEyUFQiOnsic3RhcnQiOjE5Mjc4LCJlbmQiOjE5Mjk1LCJ0ZX
h0IjoiTW92ZSBpdGVtIGNvbnRlbnQifSwiSnhDQVRjYndtMlAw
MjQ4MCI6eyJzdGFydCI6MTk4MjcsImVuZCI6MjEyNjQsInRleH
QiOiIqKkFkZGluZyBhIGxhYmVsKio6IFlvdSBjYW4gY2hhbmdl
IHRoZSBkZWZhdWx0IHRleHQgYXMgd2VsbCBhcyB0aGUgZm9udC
BhbmQgY29s4oCmIn0sInluaDVib1FpT01UaWxaTVciOnsic3Rh
cnQiOjc2LCJlbmQiOjE5NCwidGV4dCI6IiFbQ292ZXIgcGljdH
VyZV0oaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29t
L3Jvd2FuOGsvZnVuZGFtZW50YWxzLW9mLWdpcy/igKYifX0sIm
NvbW1lbnRzIjp7IlNSZnlLOHp2MHl3dndzZm0iOnsiZGlzY3Vz
c2lvbklkIjoicFZlMXQ0dHlOYkZ4UnBRTiIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCByZWNvbW1lbmRhdGlvbnMg
b24gbWFraW5nIGEgZm9sZGVyIGZvciBlYWNoIHByYWN0aWNhbC
IsImNyZWF0ZWQiOjE2ODU3ODMwMzkzNTd9LCJ1UEt0REpaWTVD
QVVrd05BIjp7ImRpc2N1c3Npb25JZCI6IksyNGk4N3VzS21GWl
VSSUoiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
cGljdHVyZSIsImNyZWF0ZWQiOjE2ODU3ODMwNDgzODl9LCJyeW
NSdG15Z0lyeVpTZWQ2Ijp7ImRpc2N1c3Npb25JZCI6InVTVmw5
bXZxMFEybjdUTEciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJEdW1iIHRoaXMgZG93biBvciBleHBsYWluIGl0IG1vcmUg
dGhvcm91Z2hseSIsImNyZWF0ZWQiOjE2ODU3ODMwNzE3NDB9LC
I5UlpPQnRUaUNST242TTVyIjp7ImRpc2N1c3Npb25JZCI6Ildq
UWdTbVZDVk8wWXZWOUIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgbWVtZSIsImNyZWF0ZWQiOjE2ODU3ODMwODM5
NTF9LCJOaGVSMFNlN3hZVnR5bzBnIjp7ImRpc2N1c3Npb25JZC
I6IkluSTR6WnJSTjRNVFJhQjMiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nz
gzMjE0NDcwfSwiS0hDVnAzczRNREN2MldpdCI6eyJkaXNjdXNz
aW9uSWQiOiJOOGNoUGR6ZEhMcXB3S0tOIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQ29tZSBiYWNrIHRvIGNoZWNrIGlm
IGFjY3VyYXRlIiwiY3JlYXRlZCI6MTY4NTc4MzIyODYzN30sIm
dNOVdqeXNuQzk1R2tEOXUiOnsiZGlzY3Vzc2lvbklkIjoiOFJB
NmRlbElZbXkxUXBtUiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODMyNDI1
NTh9LCJZZDRvZm1xZ1N1cXBqYlFSIjp7ImRpc2N1c3Npb25JZC
I6InBjaU9nZ3V3RmlCNnNVVUYiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nz
gzMjQ4MzI2fSwiaU52YUhod0MyWFFTZElTbyI6eyJkaXNjdXNz
aW9uSWQiOiJxRTNDWHgwbEg0STd1a0E0Iiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIGFuZCBjb3JyZWN0
IHRleHQiLCJjcmVhdGVkIjoxNjg1NzgzMjYyMzMzfSwiQlVXWU
RLOWhKc2RUVkpLeiI6eyJkaXNjdXNzaW9uSWQiOiJ4ME42SXlM
a2dwY1FpSjk5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQ29ycmVjdCBsYXlvdXQiLCJjcmVhdGVkIjoxNjg1NzgzMjk0
NjIxfSwib3FTZU1oTXM2dUNGOTF5diI6eyJkaXNjdXNzaW9uSW
QiOiJvVDl4ZTZxd3ZVVXJmN0JvIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIGFuZCBjb3JyZWN0IHRleH
QiLCJjcmVhdGVkIjoxNjg1NzgzMzA5MjIxfSwiVE5iUTJ0Rmtj
dXJOZ3kzQyI6eyJkaXNjdXNzaW9uSWQiOiJqdFhtUndxZFl5Q2
c4NmZhIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRk
IGltYWdlIiwiY3JlYXRlZCI6MTY4NTc4MzM1OTU3NH0sIjdSRU
9lSEFvWk9ZdVJDYlkiOnsiZGlzY3Vzc2lvbklkIjoiemlvU2RV
ZDhwY0tGRUNuUiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6Ik1ha2Ugc3R1ZGVudHMgZ2F0aGVyIHRoZSBkYXRhIHRoZW1z
ZWx2ZXMiLCJjcmVhdGVkIjoxNjg1NzgzNDkwNTMzfSwiQk14WE
dJMlhCRG9pQlY1VCI6eyJkaXNjdXNzaW9uSWQiOiJ6aW9TZFVk
OHBjS0ZFQ25SIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oib3IgYWRkIGxpbmtzIiwiY3JlYXRlZCI6MTY4NTc4MzUwNjEx
N30sIkc1SWUxUEZoVlIxaXowSmYiOnsiZGlzY3Vzc2lvbklkIj
oiTXc5QWd4cGdlTzdnMVBvUCIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3OD
M1NTc5MzV9LCJBaUhPM2JYbE0zYks5RTh6Ijp7ImRpc2N1c3Np
b25JZCI6IjU4eExrd2UwcHJQODE1VlQiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjox
Njg1NzgzNTYyOTE3fSwiN1RoN1pZSkh1N0dnbDdhcCI6eyJkaX
NjdXNzaW9uSWQiOiJhYkRBMEVIazdPMjQzWDdkIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYX
RlZCI6MTY4NTc4MzU5MjczNH0sIkNIZlJWU3luSkJMdlpKRVEi
OnsiZGlzY3Vzc2lvbklkIjoiaGxoa2RDRW0zNGwzVnJUVyIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IldoYXQgYXJlIG9i
amVjdHM/IiwiY3JlYXRlZCI6MTY4NTc4MzYwNTAyMX0sIm0wR0
RKRlpBeEJqTHFzVUUiOnsiZGlzY3Vzc2lvbklkIjoiRlhmUUZm
RjlGWk9OcFlGYSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IldoYXQgaXMgYXR0cmlidXRlIGRhdGE/IiwiY3JlYXRlZCI6
MTY4NTc4MzYxNDAzN30sInJ5WUZJRWU5eTJsRUV4NUoiOnsiZG
lzY3Vzc2lvbklkIjoiSTh5eEFEYzYzU2tPZ0QzeSIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZW
F0ZWQiOjE2ODU3ODUyNDU3MDl9LCJhdzZzQWNFVU81RGE0c0dK
Ijp7ImRpc2N1c3Npb25JZCI6IjlZSk51OG84dW91YllDZ2giLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2Ui
LCJjcmVhdGVkIjoxNjg1Nzg1NzQzNDIwfSwieDF0MDZtNzZFQW
dYS1lLNSI6eyJkaXNjdXNzaW9uSWQiOiJOeEpkRldDQmxVczI0
c2NMIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIG
ltYWdlIiwiY3JlYXRlZCI6MTY4NTc4NTc3Mzk5Nn0sIkU2TEQ4
ODJIamdHMzlockUiOnsiZGlzY3Vzc2lvbklkIjoic1FFcG5GMz
Y3c2VhdkxzYyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODU4NDI5NzF9LC
I0VFNqVjR5cHRZZU1iRWlRIjp7ImRpc2N1c3Npb25JZCI6IkFj
V1RKa21yOWFrbncyUVYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg2Mjg4
NDM1fSwiYlQ4ZTQwb2lXUGRmcXBwOSI6eyJkaXNjdXNzaW9uSW
QiOiIzWFVpaFRyZ05UWG5scnAzIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NT
c4NjI5NTc1MX0sImtnSkVZRDZadlpyNDMwR3UiOnsiZGlzY3Vz
c2lvbklkIjoiZXZMV1lvQUdYMHl1dUlYcyIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbnRyb2R1Y3Rpb24gdG8g
dGhpcz8iLCJjcmVhdGVkIjoxNjg1Nzg2NjI4MDc2fSwiY1VQYX
BUbDljSHFDY2RTayI6eyJkaXNjdXNzaW9uSWQiOiJRZ2pxY0hr
MVdlYnZkUWRVIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc4NjYzNzQ2OH0s
IkhCQ3RRdXZ2T1Y4dVJINlkiOnsiZGlzY3Vzc2lvbklkIjoiSF
RCajVOQWlqamlQSG5kdiIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODcyND
M0NjB9LCJBWGNiVVd4dDc3R0RPeVhGIjp7ImRpc2N1c3Npb25J
ZCI6ImV2TFdZb0FHWDB5dXVJWHMiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJFYXJsaWVyIGluIGNyYXNoIGNvdXJzZSwg
YWRkIGV4YW1wbGVzIG9mIHRvb2xzIGFuZCBob3cgdGhleSB3b3
JrIiwiY3JlYXRlZCI6MTY4NTc4Nzg5OTA1OX0sImxHc1JJSDZT
Z2lFZVRkR0ciOnsiZGlzY3Vzc2lvbklkIjoiSEtYc0Njb0ZLRm
Y0ZXhQUyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFk
ZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODg2NTc0NTJ9LCJ1Tm
pLczJ1d1JVYTZBZ0tOIjp7ImRpc2N1c3Npb25JZCI6ImNVN1FY
VFVCa1ppbzZnek0iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJBZGQgaW1hZ2VzIiwiY3JlYXRlZCI6MTY4NTc4ODY5NzQz
Nn0sIm40TkxjeHptUzAzT3R2TlEiOnsiZGlzY3Vzc2lvbklkIj
oiSWNkRnRnSlFiUEJNR05qQyIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3OD
k0MzQyOTN9LCIwMUNpRjhpRzhvdDNhYjFuIjp7ImRpc2N1c3Np
b25JZCI6IlBRWEprU3RZMmdzdXZ6NUQiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjox
Njg1NzkwMzIzODA5fSwiTTZFU25iek1aR09xWW50eSI6eyJkaX
NjdXNzaW9uSWQiOiJMRUdUbE01UTNXaHRnYVBYIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYX
RlZCI6MTY4NTc5MDQwODQzNH0sIkdOaUtZa3g1eURQeFBjVksi
OnsiZGlzY3Vzc2lvbklkIjoiT3Y3ZFNhd3Q3aUxoQWZFciIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIs
ImNyZWF0ZWQiOjE2ODU3OTA0NDg2MjV9LCJuQ0Q0R3VtbzE3TF
lrY3dkIjp7ImRpc2N1c3Npb25JZCI6ImxTV2plN2dQNnJsSW5n
YXkiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW
1hZ2UiLCJjcmVhdGVkIjoxNjg1NzkwNTY1NjU5fSwicWRGRXZu
YmVGNWNVUjVBbyI6eyJkaXNjdXNzaW9uSWQiOiJZeVpUYWRScH
BLcmUxMlBUIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc5MDU4NzA5MH0sIm
lERWtHa0RkcXY0TkcwbVoiOnsiZGlzY3Vzc2lvbklkIjoiSnhD
QVRjYndtMlAwMjQ4MCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBpbWFnZXMiLCJjcmVhdGVkIjoxNjg1NzkwODU0
NTc4fSwiNTdMWGpTekhzemFIY2hKVSI6eyJkaXNjdXNzaW9uSW
QiOiJ5bmg1Ym9RaU9NVGlsWk1XIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiVXBkYXRlIGNvdmVyIHBpY3R1cmUiLCJjcm
VhdGVkIjoxNjg1OTQzNTg3MzU4fSwiUFZhYTJ5ZHhUeThFQ3dU
aiI6eyJkaXNjdXNzaW9uSWQiOiJXalFnU21WQ1ZPMFl2VjlCIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiU3RyYWlnaHQg
dG8gamFpbCIsImNyZWF0ZWQiOjE2ODU5NDQwNzQ5NjV9LCJTcW
toQ1R2cmU0aHFWYXpNIjp7ImRpc2N1c3Npb25JZCI6IkluSTR6
WnJSTjRNVFJhQjMiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJHaXRodWIiLCJjcmVhdGVkIjoxNjg1OTQ0NDUzNTQxfSwi
MUxwM2pta0dKRFJlakhwOSI6eyJkaXNjdXNzaW9uSWQiOiI4Uk
E2ZGVsSVlteTFRcG1SIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiZ2l0aHViIiwiY3JlYXRlZCI6MTY4NTk0NDY5MTgwNX
0sImNLdnBBYVpZNWs0dGZuUFAiOnsiZGlzY3Vzc2lvbklkIjoi
cGNpT2dndXdGaUI2c1VVRiIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6ImdpdGh1YiIsImNyZWF0ZWQiOjE2ODU5NDQ2OTYy
MTV9fSwiaGlzdG9yeSI6WzIxMTk0NTY0NDksMTgzOTc4NjU5NC
wtMTYzNTc1MTYyNCwyNDY3NTAxOTAsMTQ5NzQ3MTAxNywxMjQ1
NDU3Mjk5LDEyMTc0MzY3NjIsNjgxMTg0ODc0LC0xODE5MDAxOD
cxLC00NzcwMDIyMzQsLTE2NDc1NjczNzIsLTE2NjM3NDA0MTJd
fQ==
-->