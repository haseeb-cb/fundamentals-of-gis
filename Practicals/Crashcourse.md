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
    2.  Apart from the color fill and a few ready-made styles, the main view does not offer very sophisticated visualizing options, so it is suggested to click on the *Simple fill*
    3.  Press the *Fill color* button and change the color of the layer to blue
    4.  If you want a transparent fill, press on the arrow on the right of the *Fill* button and select Transparent fill
    5.  One you are satisfied with the layer styles, press *Apply* and *OK*
4.  It is also possible to **visualize the layers based on the information stored in the attribute table**. This can be done by selecting Categorized or Graduated instead of Single Symbol from the dropdown menu on the top of the page.	
	
	1. Open the HSL_Helsinki_stops layer symbology
	2. Choose *Graduated* from the dropdown menu
	3. Choose "Boardings)" as the value from which the data is gathered
	4. Set the *Mode* to *Natural breaks (Jenks)* and press *Classify*
	5. Select a fitting *Color ramp* from the drop-down menu
	6. Press *Apply* and *OK*
- Symbology example picture

**Now, using the previous tips and tricks as your support, change the styles of all the layers in the project.**

5. Next, we shall move the focus from visualization to the **actual data**. Start by examining what data is included in the project and what information is stored in the layers by right clicking on the layer name and selecting *Open Attribute Table*.
	
	1. Open the *attribute table* of the layer called Helsinki_small_areas. Take a moment to examine the table, what can you see?
	 
		As you can see, the file consists of a list of the small-sized areas within the city of Helsinki with their corresponding codes and creation dates but little else. Next, we are going to calculate the area for each small area of Helsinki.   
	2.  In the *attribute table*, toggle *Editing mode* and then click on the *Field Calculator* button
- Field calculator picture
6. Now we’ll **write an expression that calculates the area of each small area of Helsinki in square kilometers**. On the right side of the Expression window is a list of drop-down menus.
	
	1. Set an informative *Output field name* (For example: Area_km2)
	2. Set the *Output field type* to *Decimal number (real)*, and *Output field length* to 10 and 2 (try the other options and look how this
	3. Open the *Geometry* drop-down menu
	4. Double-click the *\$area* expression (you can also type *\$area* in the blank *Expression window*)
	5.  Just the *\$area* expression would calculate the area in square meters, but we want square kilometers. So we will divide it by 1 000 000. Click or type the division symbol (/), and type 1000000 after the division and click OK
	6. Click the *Save Edits* button and disable *Editing* mode
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
MjQzWDdkIjp7InN0YXJ0Ijo4NTY1LCJlbmQiOjg1NzcsInRleH
QiOiJsYXllcnMgcGFuZWwifSwiaGxoa2RDRW0zNGwzVnJUVyI6
eyJzdGFydCI6Nzc3NSwiZW5kIjo3NzgxLCJ0ZXh0Ijoib2JqZW
N0In0sIkZYZlFGZkY5RlpPTnBZRmEiOnsic3RhcnQiOjc4MTYs
ImVuZCI6NzgyNSwidGV4dCI6ImF0dHJpYnV0ZSJ9LCJJOHl4QU
RjNjNTa09nRDN5Ijp7InN0YXJ0IjoxMTA4MywiZW5kIjoxMTEw
NywidGV4dCI6IlN5bWJvbG9neSBleGFtcGxlIHBpY3R1ciJ9LC
I5WUpOdThvOHVvdWJZQ2doIjp7InN0YXJ0IjoxMTg4OSwiZW5k
IjoxMTg5NiwidGV4dCI6IkVkaXRpbmcifSwiTnhKZEZXQ0JsVX
MyNHNjTCI6eyJzdGFydCI6MTE5MjYsImVuZCI6MTE5MzEsInRl
eHQiOiJGaWVsZCJ9LCJzUUVwbkYzNjdzZWF2THNjIjp7InN0YX
J0IjoxMTk1MywiZW5kIjoxMTk3NywidGV4dCI6IkZpZWxkIGNh
bGN1bGF0b3IgcGljdHVyZSJ9LCJBY1dUSmttcjlha253MlFWIj
p7InN0YXJ0IjoxMjc5NCwiZW5kIjoxMjgwMSwidGV4dCI6IkVk
aXRpbmcifSwiM1hVaWhUcmdOVFhubHJwMyI6eyJzdGFydCI6MT
I3NjIsImVuZCI6MTI3NzIsInRleHQiOiJTYXZlIEVkaXRzIn19
LCJjb21tZW50cyI6eyJ3c3BWdlNrSXVtekxtaXVNIjp7ImRpc2
N1c3Npb25JZCI6IjZSNTliY3NydUxIWEgyQTgiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgY292ZXIgcGljdHVyZS
IsImNyZWF0ZWQiOjE2ODU3ODI5NjQ5NTd9LCJTUmZ5Szh6djB5
d3Z3c2ZtIjp7ImRpc2N1c3Npb25JZCI6InBWZTF0NHR5TmJGeF
JwUU4iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
cmVjb21tZW5kYXRpb25zIG9uIG1ha2luZyBhIGZvbGRlciBmb3
IgZWFjaCBwcmFjdGljYWwiLCJjcmVhdGVkIjoxNjg1NzgzMDM5
MzU3fSwidVBLdERKWlk1Q0FVa3dOQSI6eyJkaXNjdXNzaW9uSW
QiOiJLMjRpODd1c0ttRlpVUklKIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNj
g1NzgzMDQ4Mzg5fSwicnljUnRteWdJcnlaU2VkNiI6eyJkaXNj
dXNzaW9uSWQiOiJ1U1ZsOW12cTBRMm43VExHIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRHVtYiB0aGlzIGRvd24gb3Ig
ZXhwbGFpbiBpdCBtb3JlIHRob3JvdWdobHkiLCJjcmVhdGVkIj
oxNjg1NzgzMDcxNzQwfSwiOVJaT0J0VGlDUk9uNk01ciI6eyJk
aXNjdXNzaW9uSWQiOiJXalFnU21WQ1ZPMFl2VjlCIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIG1lbWUiLCJjcmVh
dGVkIjoxNjg1NzgzMDgzOTUxfSwiR1BId1JhUEhDOWZKclJFUS
I6eyJkaXNjdXNzaW9uSWQiOiI1TVVNUEdhVzV0OHdPekRnIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIi
wiY3JlYXRlZCI6MTY4NTc4MzE5MzYzN30sImRWTWEzZVRYMjZQ
T0Zla00iOnsiZGlzY3Vzc2lvbklkIjoiU0R5bDhRVTB0RXBJc0
1OcSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBp
bWFnZSIsImNyZWF0ZWQiOjE2ODU3ODMyMDIxNTB9LCJOaGVSMF
NlN3hZVnR5bzBnIjp7ImRpc2N1c3Npb25JZCI6IkluSTR6WnJS
TjRNVFJhQjMiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1NzgzMjE0NDcwfSwi
S0hDVnAzczRNREN2MldpdCI6eyJkaXNjdXNzaW9uSWQiOiJOOG
NoUGR6ZEhMcXB3S0tOIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQ29tZSBiYWNrIHRvIGNoZWNrIGlmIGFjY3VyYXRlIi
wiY3JlYXRlZCI6MTY4NTc4MzIyODYzN30sImdNOVdqeXNuQzk1
R2tEOXUiOnsiZGlzY3Vzc2lvbklkIjoiOFJBNmRlbElZbXkxUX
BtUiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBp
bWFnZSIsImNyZWF0ZWQiOjE2ODU3ODMyNDI1NTh9LCJZZDRvZm
1xZ1N1cXBqYlFSIjp7ImRpc2N1c3Npb25JZCI6InBjaU9nZ3V3
RmlCNnNVVUYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1NzgzMjQ4MzI2fSwi
aU52YUhod0MyWFFTZElTbyI6eyJkaXNjdXNzaW9uSWQiOiJxRT
NDWHgwbEg0STd1a0E0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQWRkIGltYWdlIGFuZCBjb3JyZWN0IHRleHQiLCJjcm
VhdGVkIjoxNjg1NzgzMjYyMzMzfSwiQlVXWURLOWhKc2RUVkpL
eiI6eyJkaXNjdXNzaW9uSWQiOiJ4ME42SXlMa2dwY1FpSjk5Ii
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCBs
YXlvdXQiLCJjcmVhdGVkIjoxNjg1NzgzMjk0NjIxfSwib3FTZU
1oTXM2dUNGOTF5diI6eyJkaXNjdXNzaW9uSWQiOiJvVDl4ZTZx
d3ZVVXJmN0JvIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIGltYWdlIGFuZCBjb3JyZWN0IHRleHQiLCJjcmVhdGVk
IjoxNjg1NzgzMzA5MjIxfSwiVE5iUTJ0RmtjdXJOZ3kzQyI6ey
JkaXNjdXNzaW9uSWQiOiJqdFhtUndxZFl5Q2c4NmZhIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3
JlYXRlZCI6MTY4NTc4MzM1OTU3NH0sIjdSRU9lSEFvWk9ZdVJD
YlkiOnsiZGlzY3Vzc2lvbklkIjoiemlvU2RVZDhwY0tGRUNuUi
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik1ha2Ugc3R1
ZGVudHMgZ2F0aGVyIHRoZSBkYXRhIHRoZW1zZWx2ZXMiLCJjcm
VhdGVkIjoxNjg1NzgzNDkwNTMzfSwiQk14WEdJMlhCRG9pQlY1
VCI6eyJkaXNjdXNzaW9uSWQiOiJ6aW9TZFVkOHBjS0ZFQ25SIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoib3IgYWRkIGxp
bmtzIiwiY3JlYXRlZCI6MTY4NTc4MzUwNjExN30sIkc1SWUxUE
ZoVlIxaXowSmYiOnsiZGlzY3Vzc2lvbklkIjoiTXc5QWd4cGdl
TzdnMVBvUCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODM1NTc5MzV9LCJB
aUhPM2JYbE0zYks5RTh6Ijp7ImRpc2N1c3Npb25JZCI6IjU4eE
xrd2UwcHJQODE1VlQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1NzgzNTYyOT
E3fSwiN1RoN1pZSkh1N0dnbDdhcCI6eyJkaXNjdXNzaW9uSWQi
OiJhYkRBMEVIazdPMjQzWDdkIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc4
MzU5MjczNH0sIkNIZlJWU3luSkJMdlpKRVEiOnsiZGlzY3Vzc2
lvbklkIjoiaGxoa2RDRW0zNGwzVnJUVyIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IldoYXQgYXJlIG9iamVjdHM/IiwiY3
JlYXRlZCI6MTY4NTc4MzYwNTAyMX0sIm0wR0RKRlpBeEJqTHFz
VUUiOnsiZGlzY3Vzc2lvbklkIjoiRlhmUUZmRjlGWk9OcFlGYS
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IldoYXQgaXMg
YXR0cmlidXRlIGRhdGE/IiwiY3JlYXRlZCI6MTY4NTc4MzYxND
AzN30sInJ5WUZJRWU5eTJsRUV4NUoiOnsiZGlzY3Vzc2lvbklk
IjoiSTh5eEFEYzYzU2tPZ0QzeSIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3
ODUyNDU3MDl9LCJhdzZzQWNFVU81RGE0c0dKIjp7ImRpc2N1c3
Npb25JZCI6IjlZSk51OG84dW91YllDZ2giLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIj
oxNjg1Nzg1NzQzNDIwfSwieDF0MDZtNzZFQWdYS1lLNSI6eyJk
aXNjdXNzaW9uSWQiOiJOeEpkRldDQmxVczI0c2NMIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3Jl
YXRlZCI6MTY4NTc4NTc3Mzk5Nn0sIkU2TEQ4ODJIamdHMzlock
UiOnsiZGlzY3Vzc2lvbklkIjoic1FFcG5GMzY3c2VhdkxzYyIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZS
IsImNyZWF0ZWQiOjE2ODU3ODU4NDI5NzF9LCI0VFNqVjR5cHRZ
ZU1iRWlRIjp7ImRpc2N1c3Npb25JZCI6IkFjV1RKa21yOWFrbn
cyUVYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
aW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg2Mjg4NDM1fSwiYlQ4ZT
Qwb2lXUGRmcXBwOSI6eyJkaXNjdXNzaW9uSWQiOiIzWFVpaFRy
Z05UWG5scnAzIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc4NjI5NTc1MX19
LCJoaXN0b3J5IjpbMjEyNDQ2ODI5NiwtMTY0NzU2NzM3MiwtMT
Y2Mzc0MDQxMl19
-->