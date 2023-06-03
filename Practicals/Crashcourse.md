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
	1. Open the *Geometry* drop-down menu
	2. Double-click the *\$area* expression (you can also type *\$area* in the blank *Expression window*)
	3.  Just the *\$area* expression would calculate the area in square meters, but we want square kilometers. So we will divide it by 1 000 000. Click or type the division symbol (/), and type 
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
sic3RhcnQiOjY3MjgsImVuZCI6NzAzNSwidGV4dCI6IlRoZXNl
IGRhdGEgc2V0cyBhcmUgYWxsIGRvd25sb2FkZWQgZnJvbSBQYU
lUdWxpIGFuZCBIZWxzaW5raSBSZWdpb24gSW5mb3NoYXJlIGTi
gKYifSwiTXc5QWd4cGdlTzdnMVBvUCI6eyJzdGFydCI6NzY5Ny
wiZW5kIjo3NzE0LCJ0ZXh0IjoiSWRlbnRpZnkgRmVhdHVyZXMi
fSwiNTh4TGt3ZTBwclA4MTVWVCI6eyJzdGFydCI6ODAxOSwiZW
5kIjo4MDI2LCJ0ZXh0IjoibWVhc3VyZSJ9LCJhYkRBMEVIazdP
MjQzWDdkIjp7InN0YXJ0Ijo4NTYwLCJlbmQiOjg1NzIsInRleH
QiOiJsYXllcnMgcGFuZWwifSwiaGxoa2RDRW0zNGwzVnJUVyI6
eyJzdGFydCI6Nzc3MCwiZW5kIjo3Nzc2LCJ0ZXh0Ijoib2JqZW
N0In0sIkZYZlFGZkY5RlpPTnBZRmEiOnsic3RhcnQiOjc4MTEs
ImVuZCI6NzgyMCwidGV4dCI6ImF0dHJpYnV0ZSJ9LCJJOHl4QU
RjNjNTa09nRDN5Ijp7InN0YXJ0IjoxMTA3MSwiZW5kIjoxMTA5
NSwidGV4dCI6IlN5bWJvbG9neSBleGFtcGxlIHBpY3R1ciJ9LC
I5WUpOdThvOHVvdWJZQ2doIjp7InN0YXJ0IjoxMTg3NywiZW5k
IjoxMTg4NCwidGV4dCI6IkVkaXRpbmcifSwiTnhKZEZXQ0JsVX
MyNHNjTCI6eyJzdGFydCI6MTE5MTQsImVuZCI6MTE5MTksInRl
eHQiOiJGaWVsZCJ9LCJzUUVwbkYzNjdzZWF2THNjIjp7InN0YX
J0IjoxMTk0MSwiZW5kIjoxMTk2NSwidGV4dCI6IkZpZWxkIGNh
bGN1bGF0b3IgcGljdHVyZSJ9fSwiY29tbWVudHMiOnsid3NwVn
ZTa0l1bXpMbWl1TSI6eyJkaXNjdXNzaW9uSWQiOiI2UjU5YmNz
cnVMSFhIMkE4Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIGNvdmVyIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg1Nzgy
OTY0OTU3fSwiU1JmeUs4enYweXd2d3NmbSI6eyJkaXNjdXNzaW
9uSWQiOiJwVmUxdDR0eU5iRnhScFFOIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQWRkIHJlY29tbWVuZGF0aW9ucyBvbi
BtYWtpbmcgYSBmb2xkZXIgZm9yIGVhY2ggcHJhY3RpY2FsIiwi
Y3JlYXRlZCI6MTY4NTc4MzAzOTM1N30sInVQS3RESlpZNUNBVW
t3TkEiOnsiZGlzY3Vzc2lvbklkIjoiSzI0aTg3dXNLbUZaVVJJ
SiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaW
N0dXJlIiwiY3JlYXRlZCI6MTY4NTc4MzA0ODM4OX0sInJ5Y1J0
bXlnSXJ5WlNlZDYiOnsiZGlzY3Vzc2lvbklkIjoidVNWbDltdn
EwUTJuN1RMRyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkR1bWIgdGhpcyBkb3duIG9yIGV4cGxhaW4gaXQgbW9yZSB0aG
9yb3VnaGx5IiwiY3JlYXRlZCI6MTY4NTc4MzA3MTc0MH0sIjlS
Wk9CdFRpQ1JPbjZNNXIiOnsiZGlzY3Vzc2lvbklkIjoiV2pRZ1
NtVkNWTzBZdlY5QiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBtZW1lIiwiY3JlYXRlZCI6MTY4NTc4MzA4Mzk1MX
0sIkdQSHdSYVBIQzlmSnJSRVEiOnsiZGlzY3Vzc2lvbklkIjoi
NU1VTVBHYVc1dDh3T3pEZyIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODMx
OTM2Mzd9LCJkVk1hM2VUWDI2UE9GZWtNIjp7ImRpc2N1c3Npb2
5JZCI6IlNEeWw4UVUwdEVwSXNNTnEiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNj
g1NzgzMjAyMTUwfSwiTmhlUjBTZTd4WVZ0eW8wZyI6eyJkaXNj
dXNzaW9uSWQiOiJJbkk0elpyUk40TVRSYUIzIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRl
ZCI6MTY4NTc4MzIxNDQ3MH0sIktIQ1ZwM3M0TURDdjJXaXQiOn
siZGlzY3Vzc2lvbklkIjoiTjhjaFBkemRITHFwd0tLTiIsInN1
YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvbWUgYmFjayB0by
BjaGVjayBpZiBhY2N1cmF0ZSIsImNyZWF0ZWQiOjE2ODU3ODMy
Mjg2Mzd9LCJnTTlXanlzbkM5NUdrRDl1Ijp7ImRpc2N1c3Npb2
5JZCI6IjhSQTZkZWxJWW15MVFwbVIiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNj
g1NzgzMjQyNTU4fSwiWWQ0b2ZtcWdTdXFwamJRUiI6eyJkaXNj
dXNzaW9uSWQiOiJwY2lPZ2d1d0ZpQjZzVVVGIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3JlYXRl
ZCI6MTY4NTc4MzI0ODMyNn0sImlOdmFIaHdDMlhRU2RJU28iOn
siZGlzY3Vzc2lvbklkIjoicUUzQ1h4MGxINEk3dWtBNCIsInN1
YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSBhbm
QgY29ycmVjdCB0ZXh0IiwiY3JlYXRlZCI6MTY4NTc4MzI2MjMz
M30sIkJVV1lESzloSnNkVFZKS3oiOnsiZGlzY3Vzc2lvbklkIj
oieDBONkl5TGtncGNRaUo5OSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkNvcnJlY3QgbGF5b3V0IiwiY3JlYXRlZCI6MT
Y4NTc4MzI5NDYyMX0sIm9xU2VNaE1zNnVDRjkxeXYiOnsiZGlz
Y3Vzc2lvbklkIjoib1Q5eGU2cXd2VVVyZjdCbyIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFnZSBhbmQgY29y
cmVjdCB0ZXh0IiwiY3JlYXRlZCI6MTY4NTc4MzMwOTIyMX0sIl
ROYlEydEZrY3VyTmd5M0MiOnsiZGlzY3Vzc2lvbklkIjoianRY
bVJ3cWRZeUNnODZmYSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODMzNTk1
NzR9LCI3UkVPZUhBb1pPWXVSQ2JZIjp7ImRpc2N1c3Npb25JZC
I6Inppb1NkVWQ4cGNLRkVDblIiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJNYWtlIHN0dWRlbnRzIGdhdGhlciB0aGUgZG
F0YSB0aGVtc2VsdmVzIiwiY3JlYXRlZCI6MTY4NTc4MzQ5MDUz
M30sIkJNeFhHSTJYQkRvaUJWNVQiOnsiZGlzY3Vzc2lvbklkIj
oiemlvU2RVZDhwY0tGRUNuUiIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6Im9yIGFkZCBsaW5rcyIsImNyZWF0ZWQiOjE2OD
U3ODM1MDYxMTd9LCJHNUllMVBGaFZSMWl6MEpmIjp7ImRpc2N1
c3Npb25JZCI6Ik13OUFneHBnZU83ZzFQb1AiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVk
IjoxNjg1NzgzNTU3OTM1fSwiQWlITzNiWGxNM2JLOUU4eiI6ey
JkaXNjdXNzaW9uSWQiOiI1OHhMa3dlMHByUDgxNVZUIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGltYWdlIiwiY3
JlYXRlZCI6MTY4NTc4MzU2MjkxN30sIjdUaDdaWUpIdTdHZ2w3
YXAiOnsiZGlzY3Vzc2lvbklkIjoiYWJEQTBFSGs3TzI0M1g3ZC
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbWFn
ZSIsImNyZWF0ZWQiOjE2ODU3ODM1OTI3MzR9LCJDSGZSVlN5bk
pCTHZaSkVRIjp7ImRpc2N1c3Npb25JZCI6ImhsaGtkQ0VtMzRs
M1ZyVFciLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXaG
F0IGFyZSBvYmplY3RzPyIsImNyZWF0ZWQiOjE2ODU3ODM2MDUw
MjF9LCJtMEdESkZaQXhCakxxc1VFIjp7ImRpc2N1c3Npb25JZC
I6IkZYZlFGZkY5RlpPTnBZRmEiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJXaGF0IGlzIGF0dHJpYnV0ZSBkYXRhPyIsIm
NyZWF0ZWQiOjE2ODU3ODM2MTQwMzd9LCJyeVlGSUVlOXkybEVF
eDVKIjp7ImRpc2N1c3Npb25JZCI6Ikk4eXhBRGM2M1NrT2dEM3
kiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaW1h
Z2UiLCJjcmVhdGVkIjoxNjg1Nzg1MjQ1NzA5fSwiYXc2c0FjRV
VPNURhNHNHSiI6eyJkaXNjdXNzaW9uSWQiOiI5WUpOdThvOHVv
dWJZQ2doIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIGltYWdlIiwiY3JlYXRlZCI6MTY4NTc4NTc0MzQyMH0sIngx
dDA2bTc2RUFnWEtZSzUiOnsiZGlzY3Vzc2lvbklkIjoiTnhKZE
ZXQ0JsVXMyNHNjTCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBpbWFnZSIsImNyZWF0ZWQiOjE2ODU3ODU3NzM5OT
Z9LCJFNkxEODgySGpnRzM5aHJFIjp7ImRpc2N1c3Npb25JZCI6
InNRRXBuRjM2N3NlYXZMc2MiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgaW1hZ2UiLCJjcmVhdGVkIjoxNjg1Nzg1
ODQyOTcxfX0sImhpc3RvcnkiOls3NDE4NjIxNDAsLTE2NDc1Nj
czNzIsLTE2NjM3NDA0MTJdfQ==
-->