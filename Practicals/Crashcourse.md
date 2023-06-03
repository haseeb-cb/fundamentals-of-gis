### Fundamentals of Geographic Information Systems (GIS)

# Crash Course

-   Cover image[^1]

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

**Saving in QGIS**: You can save your project by clicking either the *save* or the *save as* icon. You can also use the keyboard shortcut *Ctrl + S* (or *Command + S*) or go to *Project* \> *Save*. The file format of a project file is \*.qgs

**Creating and opening a project in QGIS:** If you want to start a new project, you can click on the *New* icon with a blank page, or alternatively go to *Project* \> *New* or use the keyboard shortcut *Ctrl + N* (or Command + N). To open an already existing project, click on the folder-like *Open* icon to pick up where you left off.

**Changing the coordinate system of a project in QGIS:** You can see the current coordinate system of the project in the status bar in the lower right corner. You can change the coordinate system by clicking on the sign and selecting a new coordinate system from the list in the project properties window that pops open. You can access the same window also by going to *Project* \> *Properties* \> *CRS*. The default coordinate system in QGIS is set automatically to EPSG:4326 (WGS 84). You can change the default if you wish by going to *Settings* \> *Options* \> *CRS*. The data used in this course will mostly be in EPSG 3067 (ETRS-TM35FIN), which is the standard for nationwide data in Finland.

(QGIS supports ‘**on the fly**’ (**OTF**) coordinate system transformation for both vector and raster layers. This means that the program will automatically draw the layers to match the coordinate system defined for the map canvas, if a transformation formula is available.)

### 1.2 Tools, toolbars and panels

Here is a brief introduction to the **basic toolbars** in QGIS. The toolbars can be toggled in *View* \> *Toolbars* by ticking the boxes. If you can’t find a toolbar mentioned below – the toolbar might be deselected!

The **Map Navigation toolbar** lets you zoom and pan the map view.

-   Picture of map navigation toolbar

The **Attributes toolbar** includes some of the most common tools that enable for example **selecting** and **deselecting** features, **measuring lines** and getting access to the **attribute table** and **field calculator**.

-   Picture of attributes toolbar

**Adding data in QGIS:** The **Data Source Manager** offers a handy way to add a vector or raster layer. There are also special buttons for different kinds of database layers and interface services. The figure on the right offers a closer look at the tool. Similar functionality can be found in *Layer* \> *Add Layer*.

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
eyJkaXNjdXNzaW9ucyI6eyI2UjU5YmNzcnVMSFhIMkE4Ijp7In
N0YXJ0Ijo3OCwiZW5kIjo4OSwidGV4dCI6IkNvdmVyIGltYWdl
In0sInBWZTF0NHR5TmJGeFJwUU4iOnsic3RhcnQiOjExMDQsIm
VuZCI6MTI2NCwidGV4dCI6IioqRmlyc3QgbWFrZSBzdXJlIHlv
dSBoYXZlIGRvd25sb2FkZWQgdGhlIGRhdGEgemlwIGNvbnRhaW
5pbmcgdGhlIGNyYXNoIGNvdXJzZeKApiJ9LCJLMjRpODd1c0tt
RlpVUklKIjp7InN0YXJ0IjoxMzQ1LCJlbmQiOjEzNTcsInRleH
QiOiItICAgRmlndXJlIDEifSwidVNWbDltdnEwUTJuN1RMRyI6
eyJzdGFydCI6MTc5NywiZW5kIjoyMjA4LCJ0ZXh0IjoiU2ltaW
xhcmx5LCB0byBhIGUuZy4sIGEgd29ya3NwYWNlIGluIEFyY0dJ
UywgYSBwcm9qZWN0IGlzIGNvbnNpZGVyZWQgdGhlIGVuc2VtYu
KApiJ9LCJXalFnU21WQ1ZPMFl2VjlCIjp7InN0YXJ0IjoxOTky
LCJlbmQiOjIwODAsInRleHQiOiJSZW1lbWJlciB0byBzYXZlIH
lvdXIgcHJvamVjdHMgb2Z0ZW4gdG8gcHJldmVudCB3b3JrIGZy
b20gYmVpbmcgbG9zdCBpbiBjYXNlIG9m4oCmIn0sIjVNVU1QR2
FXNXQ4d096RGciOnsic3RhcnQiOjIzMTYsImVuZCI6MjMzNCwi
dGV4dCI6IioqU2F2aW5nIGluIFFHSVMqKiJ9LCJTRHlsOFFVMH
RFcElzTU5xIjp7InN0YXJ0IjoyNTU5LCJlbmQiOjI2MDIsInRl
eHQiOiIqKkNyZWF0aW5nIGFuZCBvcGVuaW5nIGEgcHJvamVjdC
BpbiBRR0lTOioqIn0sIkluSTR6WnJSTjRNVFJhQjMiOnsic3Rh
cnQiOjI4OTYsImVuZCI6Mjk1MiwidGV4dCI6IioqQ2hhbmdpbm
cgdGhlIGNvb3JkaW5hdGUgc3lzdGVtIG9mIGEgcHJvamVjdCBp
biBRR0lTOioqIn0sIk44Y2hQZHpkSExxcHdLS04iOnsic3Rhcn
QiOjM0NjgsImVuZCI6MzU5NCwidGV4dCI6IlRoZSBkYXRhIHVz
ZWQgaW4gdGhpcyBjb3Vyc2Ugd2lsbCBtb3N0bHkgYmUgaW4gRV
BTRyAzMDY3IChFVFJTLVRNMzVGSU4pLCB3aGljaOKApiJ9LCI4
UkE2ZGVsSVlteTFRcG1SIjp7InN0YXJ0Ijo0MTk4LCJlbmQiOj
QyMzEsInRleHQiOiJQaWN0dXJlIG9mIG1hcCBuYXZpZ2F0aW9u
IHRvb2xiYXIifSwicGNpT2dndXdGaUI2c1VVRiI6eyJzdGFydC
I6NDQ2NCwiZW5kIjo0NDkzLCJ0ZXh0IjoiUGljdHVyZSBvZiBh
dHRyaWJ1dGVzIHRvb2xiYXIifSwicUUzQ1h4MGxINEk3dWtBNC
I6eyJzdGFydCI6NDY5OCwiZW5kIjo0NzA0LCJ0ZXh0IjoiZmln
dXJlIn0sIngwTjZJeUxrZ3BjUWlKOTkiOnsic3RhcnQiOjQ5ND
AsImVuZCI6NDk4MywidGV4dCI6IkxheWVycyBhbmQgQnJvd3Nl
ciBwYW5lbHMgaW50cm9kdWNlZCBhYm92ZS4ifSwib1Q5eGU2cX
d2VVVyZjdCbyI6eyJzdGFydCI6NTA1MywiZW5kIjo1MTUwLCJ0
ZXh0IjoiT24gdGhlIGxlZnQgaXMgYW4gZXhhbXBsZSBvZiB0aH
JlZSBwYW5lbHMgKEJyb3dzZXIsIExheWVyIFN0eWxlIGFuZCBM
YXllcnMpIG9u4oCmIn0sImp0WG1Sd3FkWXlDZzg2ZmEiOnsic3
RhcnQiOjU1NDYsImVuZCI6NTU2OSwidGV4dCI6IkV4YW1wbGUg
aW1hZ2Ugb2YgcGx1Z2luIn0sInppb1NkVWQ4cGNLRkVDblIiOn
sic3RhcnQiOjY3MzMsImVuZCI6NzA0MCwidGV4dCI6IlRoZXNl
IGRhdGEgc2V0cyBhcmUgYWxsIGRvd25sb2FkZWQgZnJvbSBQYU
lUdWxpIGFuZCBIZWxzaW5raSBSZWdpb24gSW5mb3NoYXJlIGTi
gKYifSwiTXc5QWd4cGdlTzdnMVBvUCI6eyJzdGFydCI6NzcwMi
wiZW5kIjo3NzE5LCJ0ZXh0IjoiSWRlbnRpZnkgRmVhdHVyZXMi
fSwiNTh4TGt3ZTBwclA4MTVWVCI6eyJzdGFydCI6ODAyNCwiZW
5kIjo4MDMxLCJ0ZXh0IjoibWVhc3VyZSJ9LCJhYkRBMEVIazdP
MjQzWDdkIjp7InN0YXJ0Ijo4NTY2LCJlbmQiOjg1NzgsInRleH
QiOiJsYXllcnMgcGFuZWwifSwiaGxoa2RDRW0zNGwzVnJUVyI6
eyJzdGFydCI6Nzc3NSwiZW5kIjo3NzgxLCJ0ZXh0Ijoib2JqZW
N0In0sIkZYZlFGZkY5RlpPTnBZRmEiOnsic3RhcnQiOjc4MTYs
ImVuZCI6NzgyNSwidGV4dCI6ImF0dHJpYnV0ZSJ9LCJJOHl4QU
RjNjNTa09nRDN5Ijp7InN0YXJ0IjoxMTA2NCwiZW5kIjoxMTA4
OCwidGV4dCI6IlN5bWJvbG9neSBleGFtcGxlIHBpY3R1ciJ9LC
I5WUpOdThvOHVvdWJZQ2doIjp7InN0YXJ0IjoxMTg2NywiZW5k
IjoxMTg3NCwidGV4dCI6IkVkaXRpbmcifSwiTnhKZEZXQ0JsVX
MyNHNjTCI6eyJzdGFydCI6MTE5MDQsImVuZCI6MTE5MDksInRl
eHQiOiJGaWVsZCJ9LCJzUUVwbkYzNjdzZWF2THNjIjp7InN0YX
J0IjoxMTkzMiwiZW5kIjoxMTk1NiwidGV4dCI6IkZpZWxkIGNh
bGN1bGF0b3IgcGljdHVyZSJ9LCJBY1dUSmttcjlha253MlFWIj
p7InN0YXJ0IjoxMjgxMSwiZW5kIjoxMjgxOCwidGV4dCI6IkVk
aXRpbmcifSwiM1hVaWhUcmdOVFhubHJwMyI6eyJzdGFydCI6MT
I3NzksImVuZCI6MTI3ODksInRleHQiOiJTYXZlIEVkaXRzIn0s
ImV2TFdZb0FHWDB5dXVJWHMiOnsic3RhcnQiOjEzMjYyLCJlbm
QiOjEzMjgwLCJ0ZXh0IjoiUHJvY2Vzc2luZyBUb29sYm94In0s
IlFnanFjSGsxV2VidmRRZFUiOnsic3RhcnQiOjEzMTg3LCJlbm
QiOjEzMjE2LCJ0ZXh0IjoiU2VsZWN0IGZlYXR1cmVzIGJ5IGV4
cHJlc3Npb24ifSwiSFRCajVOQWlqamlQSG5kdiI6eyJzdGFydC
I6MTQwMjYsImVuZCI6MTQwMzgsInRleHQiOiJEZXNlbGVjdCBh
bGwifSwiSEtYc0Njb0ZLRmY0ZXhQUyI6eyJzdGFydCI6MTQwND
IsImVuZCI6MTQwODEsInRleHQiOiItIFNlbGVjdCBmZWF0dXJl
cyBieSBleHByZXNzaW9uIHBpY3R1cmUifSwiY1U3UVhUVUJrWm
lvNmd6TSI6eyJzdGFydCI6MTUyNTIsImVuZCI6MTUyOTAsInRl
eHQiOiItIEpvaW4gYXR0cmlidXRlcyBieSBMb2NhdGlvbiBwaW
N0dXJlcyJ9LCJJY2RGdGdKUWJQQk1HTmpDIjp7InN0YXJ0Ijox
NjgyOCwiZW5kIjoxNjg3NiwidGV4dCI6ImN0dXJlIG9mIGN1cn
JlbnQgYXR0cmlidXRlIHRhYmxlIHdpdGggbmV3IGZpZWxkcyJ9
LCJQUVhKa1N0WTJnc3V2ejVEIjp7InN0YXJ0IjoxNzg2NiwiZW
5kIjoxNzg5MCwidGV4dCI6Ii0gTGF5b3V0IG1hbmFnZXIgcGlj
dHVyZSJ9LCJMRUdUbE01UTNXaHRnYVBYIjp7InN0YXJ0IjoxNz
k4OSwiZW5kIjoxODAwNSwidGV4dCI6Ik5ldyBQcmludCBsYXlv
dXQifSwiT3Y3ZFNhd3Q3aUxoQWZFciI6eyJzdGFydCI6MTgyND
ksImVuZCI6MTgyNjcsInRleHQiOiJBZGQgbmV3IG1hcCBidXR0
b24ifSwibFNXamU3Z1A2cmxJbmdheSI6eyJzdGFydCI6MTg2MT
YsImVuZCI6MTg2MjUsInRleHQiOiJNb3ZlIGl0ZW0ifSwiWXla
VGFkUnBwS3JlMTJQVCI6eyJzdGFydCI6MTg3MjcsImVuZCI6MT
g3NDQsInRleHQiOiJNb3ZlIGl0ZW0gY29udGVudCJ9LCJKeENB
VGNid20yUDAyNDgwIjp7InN0YXJ0IjoxOTI3NiwiZW5kIjoyMD
cxMywidGV4dCI6IioqQWRkaW5nIGEgbGFiZWwqKjogWW91IGNh
biBjaGFuZ2UgdGhlIGRlZmF1bHQgdGV4dCBhcyB3ZWxsIGFzIH
RoZSBmb250IGFuZCBjb2zigKYifX0sImNvbW1lbnRzIjp7Indz
cFZ2U2tJdW16TG1pdU0iOnsiZGlzY3Vzc2lvbklkIjoiNlI1OW
Jjc3J1TEhYSDJBOCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBjb3ZlciBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NT
c4Mjk2NDk1N30sIlNSZnlLOHp2MHl3dndzZm0iOnsiZGlzY3Vz
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
NTF9LCJHUEh3UmFQSEM5ZkpyUkVRIjp7ImRpc2N1c3Npb25JZC
I6IjVNVU1QR2FXNXQ4d096RGciLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nz
gzMTkzNjM3fSwiZFZNYTNlVFgyNlBPRmVrTSI6eyJkaXNjdXNz
aW9uSWQiOiJTRHlsOFFVMHRFcElzTU5xIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6
MTY4NTc4MzIwMjE1MH0sIk5oZVIwU2U3eFlWdHlvMGciOnsiZG
lzY3Vzc2lvbklkIjoiSW5JNHpaclJONE1UUmFCMyIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZW
F0ZWQiOjE2ODU3ODMyMTQ0NzB9LCJLSENWcDNzNE1EQ3YyV2l0
Ijp7ImRpc2N1c3Npb25JZCI6Ik44Y2hQZHpkSExxcHdLS04iLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDb21lIGJhY2sg
dG8gY2hlY2sgaWYgYWNjdXJhdGUiLCJjcmVhdGVkIjoxNjg1Nz
gzMjI4NjM3fSwiZ005V2p5c25DOTVHa0Q5dSI6eyJkaXNjdXNz
aW9uSWQiOiI4UkE2ZGVsSVlteTFRcG1SIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6
MTY4NTc4MzI0MjU1OH0sIllkNG9mbXFnU3VxcGpiUVIiOnsiZG
lzY3Vzc2lvbklkIjoicGNpT2dndXdGaUI2c1VVRiIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZW
F0ZWQiOjE2ODU3ODMyNDgzMjZ9LCJpTnZhSGh3QzJYUVNkSVNv
Ijp7ImRpc2N1c3Npb25JZCI6InFFM0NYeDBsSDRJN3VrQTQiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2Ug
YW5kIGNvcnJlY3QgdGV4dCIsImNyZWF0ZWQiOjE2ODU3ODMyNj
IzMzN9LCJCVVdZREs5aEpzZFRWSkt6Ijp7ImRpc2N1c3Npb25J
ZCI6IngwTjZJeUxrZ3BjUWlKOTkiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJDb3JyZWN0IGxheW91dCIsImNyZWF0ZWQi
OjE2ODU3ODMyOTQ2MjF9LCJvcVNlTWhNczZ1Q0Y5MXl2Ijp7Im
Rpc2N1c3Npb25JZCI6Im9UOXhlNnF3dlVVcmY3Qm8iLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UgYW5kIG
NvcnJlY3QgdGV4dCIsImNyZWF0ZWQiOjE2ODU3ODMzMDkyMjF9
LCJUTmJRMnRGa2N1ck5neTNDIjp7ImRpc2N1c3Npb25JZCI6Im
p0WG1Sd3FkWXlDZzg2ZmEiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1NzgzMz
U5NTc0fSwiN1JFT2VIQW9aT1l1UkNiWSI6eyJkaXNjdXNzaW9u
SWQiOiJ6aW9TZFVkOHBjS0ZFQ25SIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiTWFrZSBzdHVkZW50cyBnYXRoZXIgdGhl
IGRhdGEgdGhlbXNlbHZlcyIsImNyZWF0ZWQiOjE2ODU3ODM0OT
A1MzN9LCJCTXhYR0kyWEJEb2lCVjVUIjp7ImRpc2N1c3Npb25J
ZCI6Inppb1NkVWQ4cGNLRkVDblIiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJvciBhZGQgbGlua3MiLCJjcmVhdGVkIjox
Njg1NzgzNTA2MTE3fSwiRzVJZTFQRmhWUjFpejBKZiI6eyJkaX
NjdXNzaW9uSWQiOiJNdzlBZ3hwZ2VPN2cxUG9QIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYX
RlZCI6MTY4NTc4MzU1NzkzNX0sIkFpSE8zYlhsTTNiSzlFOHoi
OnsiZGlzY3Vzc2lvbklkIjoiNTh4TGt3ZTBwclA4MTVWVCIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIs
ImNyZWF0ZWQiOjE2ODU3ODM1NjI5MTd9LCI3VGg3WllKSHU3R2
dsN2FwIjp7ImRpc2N1c3Npb25JZCI6ImFiREEwRUhrN08yNDNY
N2QiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW
1hZ2UiLCJjcmVhdGVkIjoxNjg1NzgzNTkyNzM0fSwiQ0hmUlZT
eW5KQkx2WkpFUSI6eyJkaXNjdXNzaW9uSWQiOiJobGhrZENFbT
M0bDNWclRXIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
V2hhdCBhcmUgb2JqZWN0cz8iLCJjcmVhdGVkIjoxNjg1NzgzNj
A1MDIxfSwibTBHREpGWkF4QmpMcXNVRSI6eyJkaXNjdXNzaW9u
SWQiOiJGWGZRRmZGOUZaT05wWUZhIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiV2hhdCBpcyBhdHRyaWJ1dGUgZGF0YT8i
LCJjcmVhdGVkIjoxNjg1NzgzNjE0MDM3fSwicnlZRklFZTl5Mm
xFRXg1SiI6eyJkaXNjdXNzaW9uSWQiOiJJOHl4QURjNjNTa09n
RDN5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIG
ltYWdlIiwiY3JlYXRlZCI6MTY4NTc4NTI0NTcwOX0sImF3NnNB
Y0VVTzVEYTRzR0oiOnsiZGlzY3Vzc2lvbklkIjoiOVlKTnU4bz
h1b3ViWUNnaCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODU3NDM0MjB9LC
J4MXQwNm03NkVBZ1hLWUs1Ijp7ImRpc2N1c3Npb25JZCI6Ik54
SmRGV0NCbFVzMjRzY0wiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg1Nzcz
OTk2fSwiRTZMRDg4MkhqZ0czOWhyRSI6eyJkaXNjdXNzaW9uSW
QiOiJzUUVwbkYzNjdzZWF2THNjIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NT
c4NTg0Mjk3MX0sIjRUU2pWNHlwdFllTWJFaVEiOnsiZGlzY3Vz
c2lvbklkIjoiQWNXVEprbXI5YWtudzJRViIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQi
OjE2ODU3ODYyODg0MzV9LCJiVDhlNDBvaVdQZGZxcHA5Ijp7Im
Rpc2N1c3Npb25JZCI6IjNYVWloVHJnTlRYbmxycDMiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcm
VhdGVkIjoxNjg1Nzg2Mjk1NzUxfSwia2dKRVlENlp2WnI0MzBH
dSI6eyJkaXNjdXNzaW9uSWQiOiJldkxXWW9BR1gweXV1SVhzIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGludHJv
ZHVjdGlvbiB0byB0aGlzPyIsImNyZWF0ZWQiOjE2ODU3ODY2Mj
gwNzZ9LCJjVVBhcFRsOWNIcUNjZFNrIjp7ImRpc2N1c3Npb25J
ZCI6IlFnanFjSGsxV2VidmRRZFUiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1
Nzg2NjM3NDY4fSwiSEJDdFF1dnZPVjh1Ukg2WSI6eyJkaXNjdX
NzaW9uSWQiOiJIVEJqNU5BaWpqaVBIbmR2Iiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZC
I6MTY4NTc4NzI0MzQ2MH0sIkFYY2JVV3h0NzdHRE95WEYiOnsi
ZGlzY3Vzc2lvbklkIjoiZXZMV1lvQUdYMHl1dUlYcyIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkVhcmxpZXIgaW4gY3Jh
c2ggY291cnNlLCBhZGQgZXhhbXBsZXMgb2YgdG9vbHMgYW5kIG
hvdyB0aGV5IHdvcmsiLCJjcmVhdGVkIjoxNjg1Nzg3ODk5MDU5
fSwibEdzUklINlNnaUVlVGRHRyI6eyJkaXNjdXNzaW9uSWQiOi
JIS1hzQ2NvRktGZjRleFBTIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc4OD
Y1NzQ1Mn0sInVOaktzMnV3UlVhNkFnS04iOnsiZGlzY3Vzc2lv
bklkIjoiY1U3UVhUVUJrWmlvNmd6TSIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZXMiLCJjcmVhdGVkIjox
Njg1Nzg4Njk3NDM2fSwibjROTGN4em1TMDNPdHZOUSI6eyJkaX
NjdXNzaW9uSWQiOiJJY2RGdGdKUWJQQk1HTmpDIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYX
RlZCI6MTY4NTc4OTQzNDI5M30sIjAxQ2lGOGlHOG90M2FiMW4i
OnsiZGlzY3Vzc2lvbklkIjoiUFFYSmtTdFkyZ3N1dno1RCIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSIs
ImNyZWF0ZWQiOjE2ODU3OTAzMjM4MDl9LCJNNkVTbmJ6TVpHT3
FZbnR5Ijp7ImRpc2N1c3Npb25JZCI6IkxFR1RsTTVRM1dodGdh
UFgiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW
1hZ2UiLCJjcmVhdGVkIjoxNjg1NzkwNDA4NDM0fSwiR05pS1lr
eDV5RFB4UGNWSyI6eyJkaXNjdXNzaW9uSWQiOiJPdjdkU2F3dD
dpTGhBZkVyIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc5MDQ0ODYyNX0sIm
5DRDRHdW1vMTdMWWtjd2QiOnsiZGlzY3Vzc2lvbklkIjoibFNX
amU3Z1A2cmxJbmdheSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3OTA1NjU2
NTl9LCJxZEZFdm5iZUY1Y1VSNUFvIjp7ImRpc2N1c3Npb25JZC
I6Ill5WlRhZFJwcEtyZTEyUFQiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nz
kwNTg3MDkwfSwiaURFa0drRGRxdjRORzBtWiI6eyJkaXNjdXNz
aW9uSWQiOiJKeENBVGNid20yUDAyNDgwIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlcyIsImNyZWF0ZWQi
OjE2ODU3OTA4NTQ1Nzh9fSwiaGlzdG9yeSI6WzEyNDU0NTcyOT
ksMTIxNzQzNjc2Miw2ODExODQ4NzQsLTE4MTkwMDE4NzEsLTQ3
NzAwMjIzNCwtMTY0NzU2NzM3MiwtMTY2Mzc0MDQxMl19
-->