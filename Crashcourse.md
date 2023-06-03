---


---

<h3 id="fundamentals-of-geographic-information-systems-gis">Fundamentals of Geographic Information Systems (GIS)</h3>
<h1 id="crash-course">Crash Course</h1>
<ul>
<li>Cover image<sup class="footnote-ref"><a href="#fn1" id="fnref1">1</a></sup></li>
</ul>
<p>Rowan van der Kaaden</p>
<h2 id="introduction-to-qgis">Introduction to QGIS</h2>
<h3 id="the-contents-of-this-exercise-in-a-nutshell">The contents of this exercise in a nutshell:</h3>
<p><strong>The aim of this practical is to</strong> get familiar with the QGIS software. The first practical exercises will introduce the QGIS graphical user interface (GUI) and its basic tools and features to create a foundation for the later practicals. After some basic introduction, you will create a choropleth map<sup class="footnote-ref"><a href="#fn2" id="fnref2">2</a></sup>.</p>
<p>If you have time after that, try out the second part! They will introduce joining spreadsheet data with spatial data and vector clipping.</p>
<p><strong>By the end of today’s crash course, you will:</strong></p>
<ul>
<li><strong>Be familiar with QGIS’s user interface and basic functions</strong></li>
<li><strong>Have an idea what kind of data types GIS can process</strong></li>
</ul>
<p><strong>Note:</strong> If you have not yet downloaded QGIS, do so now from this link: <a href="https://www.qgis.org/en/site/forusers/download.html">https://www.qgis.org/en/site/forusers/download.html</a> See QGIS installation instructions for details.</p>
<h2 id="the-basics-of-qgis">The basics of QGIS</h2>
<h3 id="getting-started-with-qgis">Getting started with QGIS</h3>
<p><strong>First make sure you have downloaded the data zip containing the crash course data.</strong> If you have not, download it using the link in Moodle and unzip the data.</p>
<p><strong>Launch QGIS</strong> and the QGIS graphical user interface (GUI) opens (Figure 1).</p>
<ul>
<li>Figure 1</li>
</ul>
<p>Start by setting the <strong>default language</strong> in QGIS to English (if it isn’t already) by navigating to the language settings: <em>Settings menu</em> &gt; <em>Options</em> &gt; <em>General</em> &gt; <em>User Interface Translation</em>. Tick the “<em>Override system locale</em>” box and choose English from the dropdown menu and close the window by pressing OK. For the change to take effect, restart the application.</p>
<p>The state of a working session in QGIS is called a <strong>project</strong>. Similarly, to a e.g., a workspace in ArcGIS, a project is considered the ensemble of layers, projections, table relations and other properties, such as symbols and styles, of a specific session. Remember to save your projects often to prevent work from being lost in case of a crash. Also note that project files do not contain geospatial data, they merely contain information on where the program will find it.</p>
<p><em>Here a few basic functions that are worth knowing before starting to play around with data and layers:</em></p>
<p><strong>Saving in QGIS</strong>: You can save your project by clicking either the <em>save</em> or the <em>save as</em> icon. You can also use the keyboard shortcut <em>Ctrl + S</em> (or <em>Command + S</em>) or go to <em>Project</em> &gt; <em>Save</em>. The file format of a project file is *.qgs</p>
<p><strong>Creating and opening a project in QGIS:</strong> If you want to start a new project, you can click on the <em>New</em> icon with a blank page, or alternatively go to <em>Project</em> &gt; <em>New</em> or use the keyboard shortcut <em>Ctrl + N</em> (or Command + N). To open an already existing project, click on the folder-like <em>Open</em> icon to pick up where you left off.</p>
<p><strong>Changing the coordinate system of a project in QGIS:</strong> You can see the current coordinate system of the project in the status bar in the lower right corner. You can change the coordinate system by clicking on the sign and selecting a new coordinate system from the list in the project properties window that pops open. You can access the same window also by going to <em>Project</em> &gt; <em>Properties</em> &gt; <em>CRS</em>. The default coordinate system in QGIS is set automatically to EPSG:4326 (WGS 84). You can change the default if you wish by going to <em>Settings</em> &gt; <em>Options</em> &gt; <em>CRS</em>. The data used in this course will mostly be in EPSG 3067 (ETRS-TM35FIN), which is the standard for nationwide data in Finland.</p>
<p>(QGIS supports ‘<strong>on the fly</strong>’ (<strong>OTF</strong>) coordinate system transformation for both vector and raster layers. This means that the program will automatically draw the layers to match the coordinate system defined for the map canvas, if a transformation formula is available.)</p>
<h3 id="tools-toolbars-and-panels">1.2 Tools, toolbars and panels</h3>
<p>Here is a brief introduction to the <strong>basic toolbars</strong> in QGIS. The toolbars can be toggled in <em>View</em> &gt; <em>Toolbars</em> by ticking the boxes. If you can’t find a toolbar mentioned below – the toolbar might be deselected!</p>
<p>The <strong>Map Navigation toolbar</strong> lets you zoom and pan the map view.</p>
<ul>
<li>Picture of map navigation toolbar</li>
</ul>
<p>The <strong>Attributes toolbar</strong> includes some of the most common tools that enable for example <strong>selecting</strong> and <strong>deselecting</strong> features, <strong>measuring lines</strong> and getting access to the <strong>attribute table</strong> and <strong>field calculator</strong>.</p>
<ul>
<li>Picture of attributes toolbar</li>
</ul>
<p><strong>Adding data in QGIS:</strong> The <strong>Data Source Manager</strong> offers a handy way to add a vector or raster layer. There are also special buttons for different kinds of database layers and interface services. The figure on the right offers a closer look at the tool. Similar functionality can be found in <em>Layer</em> &gt; <em>Add Layer</em>.</p>
<p>If you want to create new empty layers, go to <em>Layer</em> &gt; <em>Create Layer</em>.</p>
<p><strong>Panels</strong> offer a single major function, like the Layers and Browser panels introduced above. Similarly, to toolbars, they can be toggled from <em>View</em> &gt; <em>Panels</em>. On the left is an example of three panels (Browser, Layer Style and Layers) on top of each other.</p>
<h3 id="plugins">1.3 Plugins</h3>
<p>Only a fraction of all the possible tools and functions are visible in the default view of QGIS as a lot of functionality is done via <strong>plugins</strong>. You can manage plugins in the QGIS plugin manager: select <em>Plugins</em> &gt; <em>Manage</em> and install plugins. Here you can see what plugins are already installed to your repository and install new or update/uninstall current plugins.</p>
<ul>
<li>Example image of plugin</li>
</ul>
<p>Let’s download a very handy plugin called <strong>QuickMapServices</strong>, which gives access to a wide selection of background maps.</p>
<ol>
<li>Select <em>Plugins</em> &gt; <em>Manage</em></li>
<li>Select <em>All</em> on the left menu and type “QuickMapServices” in the search bar</li>
<li>Select the QuickMapServices plugin and <em>Install the plugin</em></li>
<li>You can find the newly installed plugin in the main QGIS window under <em>Web</em> &gt; <em>QuickMapServices</em></li>
</ol>
<p>(Hungry for more? Further reading on plugins in the QGIS manual: <a href="https://docs.qgis.org/3.22/en/docs/user_manual/plugins/index.html">https://docs.qgis.org/3.22/en/docs/user_manual/plugins/index.html</a>)</p>
<h2 id="warm-up-exercise">2 Warm-up exercise</h2>
<h3 id="add-and-explore-data">2.1 Add and explore data</h3>
<p>In order to get a proper touch of QGIS and how the different tools work, we will of course need data.</p>
<ol>
<li>Open the Data Source Manager (see 1.2)</li>
<li>Select <em>Vector</em> from the menu</li>
<li>Press the “…” button next to the <em>Vector Dataset(s)</em> field</li>
<li>Navigate to the folder where you saved the data for this practical and select the following files from the folder (Click + Ctrl to select multiple items):
<ol>
<li>Helsinki_small_areas.shp</li>
<li>Helsinki_Municipality.shp</li>
<li>Helsinki_buildings.shp</li>
<li>HSL_helsinki_stops.shp</li>
</ol>
</li>
<li>Press <em>Open</em></li>
<li>Press <em>Add</em></li>
</ol>
<p>These data sets are all downloaded from PaITuli and Helsinki Region Infoshare data and map services, the data itself is produced by numerous entities (National Land Survey, Helsinki Regional Transport and the City of Helsinki). You can also add the Helsinki_roads.shp layer later for visualization purposes.</p>
<p>The shapefiles should now appear on the map canvas. Once you add the layers, the program should automatically change the project’s coordinate system to EPSG:3067, or more commonly, the ETRS89-TM35FIN (Transverse-Mercator) coordinate reference system, which is the proposed system for spatial data in Finland.</p>
<p>For a start, take your time to move around and get acquainted with the basic tools in QGIS. Try panning around and zooming in and out in the map view. If your layers “get lost” by mistake when zooming, simply right click on the layer you want to retrieve and select <em>Zoom to layer</em>.</p>
<p><strong>Whilst moving around, try out the following two tools:</strong></p>
<p>The <strong>Identify Features</strong> tool is essentially an info-tool that identifies the object(s) selected with it and lists the attribute data available for all the layers in that particular location. If you only want to look at information from a specific layer, use the drop-down menu to specify the layer you want to examine.</p>
<p>The <strong>measure</strong> tool can be used to make simple distance and area calculations on the map, as well as for measuring angles. The tool can calculate both the length of single line segments and the sum of all drawn lines. The measurement unit can be changed from the tool options.</p>
<p>Managing the <strong>layers</strong> is key in GIS. Right now, the added layers are arbitrarily symbolized and ordered, and do not come out very useful or informative. Thus, we need to get our hands dirty.</p>
<ol>
<li>
<p>Start by <strong>changing the order of the layers</strong> by dragging them in the layers panel on the left side of the map view. A good order, for example, can be as follows from top to bottom: HSL_Helsinki_stops, Helsinki_buildings, Waterbodies, Helsinki_small_areas and Helsinki_Municipality.</p>
</li>
<li>
<p>You can also <strong>change the visibility of the layers</strong> by checking or unchecking the tick boxes next to the layer name or by adjusting <strong>transparency</strong>. The latter can be done under the <em>Style</em> tab in the <em>Layer properties</em> window, which can be accessed by right-clicking on the layer name and selecting <em>Properties</em>. This is also where you can change other style properties such as <strong>symbol size and color</strong>, <strong>layer rendering</strong> or create e.g. <strong>choropleth maps</strong>, but we will look into these in more detail later on.</p>
<p>In addition to editing a layer’s style properties, the Layer properties window can also be used for e.g. examining the <strong>layer’s general information</strong> such as its coordinate system and source, adding <strong>labels</strong> to the map as well as managing <strong>joins</strong> and layer <strong>metadata</strong>.</p>
</li>
<li>
<p>Next, we want to <strong>change the styles and the symbology of the layers</strong>. You can navigate back to the <em>Symbology</em> tab in the <em>Layer Properties</em> window. The window looks slightly different depending on whether we have a raster or vector file, and what feature type is in question. You can see this for instance by comparing the style tabs of the HSL Stops (point feature) and Waterbodies (polygon feature) layers.</p>
<ol>
<li>Open the <em>symbology</em> properties for the Waterbodies layer</li>
<li>Apart from the color fill and a few ready-made styles, the main view does not offer very sophisticated visualizing options, so it is suggested to click on the <em>Simple fill</em></li>
<li>Press the <em>Fill color</em> button and change the color of the layer to blue</li>
<li>If you want a transparent fill, press on the arrow on the right of the <em>Fill</em> button and select Transparent fill</li>
<li>One you are satisfied with the layer styles, press <em>Apply</em> and <em>OK</em></li>
</ol>
</li>
<li>
<p>It is also possible to <strong>visualize the layers based on the information stored in the attribute table</strong>. This can be done by selecting Categorized or Graduated instead of Single Symbol from the dropdown menu on the top of the page.</p>
</li>
</ol>
<hr class="footnotes-sep">
<section class="footnotes">
<ol class="footnotes-list">
<li id="fn1" class="footnote-item"><p>Image note <a href="#fnref1" class="footnote-backref">↩︎</a></p>
</li>
<li id="fn2" class="footnote-item"><p>What is a choropleth map? <a href="#fnref2" class="footnote-backref">↩︎</a></p>
</li>
</ol>
</section>

