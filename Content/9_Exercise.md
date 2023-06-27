### Fundamentals of Geographic Information Systems (GIS)

# Exercise 9: PPGIS/SoftGIS

## OVERVIEW & PURPOSE

Participatory sensing for GIS has become a useful tool to extract quantitative and qualitative information about the environment. Using map questionnaires is an easy way to collect experiential or other types of information from the inhabitants about the everyday environment. Tools like Maptionnaire have enabled urban planners, researchers and activist groups to gain insight about areas and phenomena. These tools have been used to find places/areas that feel safe, insecure, noisy, quiet and so on. Directing the map questionnaires towards a certain population group (children, the elderly, immigrants etc.) can yield valuable data for planning and research purposes. Commonly, this way of obtaining spatial data through the public is known as Public Participation GIS (PPGIS), SoftGIS and Social/Participatory Sensing. With the increasing presence of social media services and location services of smart technology, mining of social media data has become a frontier of “socially sensed” data.

Today we’re using an online map questionnaire from 2015 about possible wind power sites to study the NIMBY (Not in my backyard) phenomenon in Helsinki (if you’re interested in the phenomenon, see Veikko Eranti’s (2017) article “Re-visiting NIMBY: From conflicting interests to conflicting valuations” in Moodle or here: http://urn.fi/URN:NBN:fi:uta-201804051508). This time you’ll have to download the data as it is from an open data portal (www.hri.fi). You’ll get familiar with some of the common difficulties of working with open data and especially open GIS data. You’ll also learn to use a new and helpful tool in QGIS.

### Directional Distribution (Standard Deviational Ellipse, SDE)

We’ll create standard deviational ellipses to summarize the spatial characteristics of geographic features: central tendency, dispersion, and directional trends. Standard Deviation Ellipse shows the area where the majority of the features (here, possible wind power sites)are located:When the underlying spatial pattern of features is concentrated in the center with fewer features toward the periphery (a spatial normal distribution), a standard deviational ellipse polygon will cover approximately 68 percent of the features.

![](https://geol260.academic.wlu.edu/files/lecture_notes/standardellipse_stat.gif)
(Hungry for more? 
- http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-statistics-toolbox/directional-distribution.htm
- http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-statistics-toolbox/h-how-directional-distribution-standard-deviationa.htm)

## OBJECTIVES

1. Getting familiar with SoftGIS/PPGIS (public participation GIS) data from a wind power
questionnaire
2. Examining the directional distribution of answers
3. Studying NIMBY attitudes from two locations

## DATA USED/NEEDED

1. “Helsingin tuulivoimakysely 2015” (“Wind power survey for Helsinki 2015”)
	-  Find and download this Excel data from http://www.hri.fi/en/
2. Zip code areas of Helsinki
	- Download this data from Helsinki Region Environmental Authority’sWFS (HSYWFS): 
	Title: pks_postinumeroalueet_2022
	- Or from the WFS of the city of Helsinki: Postinumeroalue

## COMPLETION

Work individually or in pairs. Complete the exercise and write a short reflection. Include at the following: 

1. Downloading the two datasets described above and importing the spreadsheet data as point layers
2. Finding where the respondents from Töölö and Vuosaari (neighbourhoods in Helsinki) prefer and don’t prefer to have windmills
	- Discovering the standard deviational ellipses of the preferences of respondents from Töölö and Vuosaari.
3. Visualizing and composing at least 3 maps of the NIMBY attitudes, including:
	- Maps depicting Töölö and Vuosaari respondents’ preferred and unpreferred wind power plant locations and personally important places, and
	- Map of the directional distribution of unpreferred locations.
4. Analyzing in writing the NIMBY attitudes between the two respondent areas:
	- Are the preferred locations for wind power turbines located near or far away from the respondents’ own neighbourhood? How about unpreferred locations? Pay special attention to the sea and coastal areas.
	- Are the places that are important to the respondents located in the same areas as the locations where they prefer not to have wind power turbines? Can you think of why/why not?
	- What do the standard deviational ellipses reveal of the respondents’ preferences? Are there any overlaps between the two groups of respondents?
	- Are there any potential conflict areas?

## EXERCISE PHASES

### Getting familiar with the data

1. **Head over to Helsinki Region Infoshare** (http://www.hri.fi/en/), search for “Helsingin tuulivoimakysely 2015” or “Wind power survey for Helsinki 2015”, and **download the wind power survey data** (the data are in Excel format)
	
	1. Unzip the files into a folder for this exercise, and open the files in Libra Office, Excel, or something similar. 
	2. There are three files that contain latitudinal and longitudinal coordinates (WGS84):
		-	Tuulivoimakysely_**soveltuvat**_paikat (**preferred** places for wind turbines)
		-	Tuulivoimakysely_**kielletyt**_paikat (**unpreferred** places for wind turbines)
		-	Tuulivoimakysely_**omat**_paikat (coastal/maritime places that are **important to
the residents**)

2. Since it’s difficult to import Excel’s native file format (.xlsx) spreadsheet data into QGIS, you should **save those three files in csv-format (in Libre Office: csv, in Excel:Windows -csv/CSV (comma delimited)**. On Mac, you may have to use Libre Office.

3. **Import the csv -files into QGIS using Add Delimited Text Layer**
	1. By default, as you are importing the text file, you will probably run into a cramped mass of text in the Sample Data display, like in the picture below. Instead, the Sample Data should look like something you would find in an Attribute table.
- Figure
	2. Change File Format to Regular expression delimiter. As we can see in the Sample Data box, the semicolon ; is being used in the text. Type ; into Expression.
- Figure
	3. If the names of the columns in the sample data are not ID, postinumero, and so on, but field_1, field_2, etc. (compare pictures above and below): make sure to tick the First record has field values checkbox.
- Figure
	4.  To transform the geographic information of your text file into a visual map, we have to tell QGIS where in the text locations are specified. Therefore, under Geometry Definition, choose the right **X field** (= Lng) and **Y field** (= Lat) from the menu. Also set the correct **Geometry CRS** (= EPSG:4326 - WGS 84). Then Add.
		- The coordinate systemused for the points is a global coordinate system WGS84 (also used by e.g. Google Maps/Earth). What do you think might be the reason that the coordinates are inWGS84 instead of a Finnish coordinate system?
	5. Once you have imported all three text files into QGIS, save each of the layers on your computer in shapefile format. Name these layers informatively (e.g., preferred (‘soveltuvat’), unpreferred (‘kielletyt’), and important (‘omat’)). Fromhere on, continue with the exercise working on these new layers.

4. **Explore the attribute tables for the three layers**
	
	1. The field Postinumero has the zip codes, which will be important for us
		- (General notion, no need for action: as you can see, there is the prefix “ZIP_”, which could make joining difficult. Open data or any kind of data can have things like these that make interoperability difficult. However, this not an issue for now, since we are not joining data today.)
	2. The field Ikä has the age of the respondent, and the field Sukupuoli has the gender of the respondent (m=male, n=female)
	3. Fun fact: the field Perustelut contains the respondents’ open answers (if any) about why the area would or wouldn’t be suitable for wind turbines
		- For the important places layer, this field instead has the reasons why the particular place is important to the respondent
		- Some of the given reasons are quite opinionated and funny. You can read them mostly in Finnish, but there are some in English and Swedish, too.
	4. *Optional*: Using the Group Stats plugin is very usefulwhen dealing with large datasets, because one can examine the attribute data by grouping it by variables.
		- For instance, in this case Group Stats can be used to easily decipher how many women and men answered the survey, or which zip code area had the most respondents. (See also: https://gis.stackexchange.com/questions/229007/whydoes-calculate-button-remain-gray-in-group-stats-plugin-for-qgis)

---

### Classification of the data

5. To discover possible NIMBY attitudes of the respondents, we’re going to **extract the answers based on the residential areas of the respondents**.
	-  Doing this is easy, since one of the fields in attribute data has the zip code of the area where each respondent lives in.

6. We’re interested in the respondents that live in **Töölö** and **Vuosaari** city districts. Both districts have three zip code areas, the names of which are:
	- Vuosaari
		- Pohjois-Vuosaari (00960)
		- Etelä-Vuosaari (00980)
		- Aurinkolahti (00990)
	- Töölö
		- Etu-Töölö (00100)
		- Keski-Töölö (00260)
		- Taka-Töölö (00250)

7. For each of the three layers (preferred/unpreferred/important places layers), **select the entries by respondents from Vuosaari, employing *Select features using an expression*** and the zip code information provided above.
	1. Save the selections as new shapefile layers.
	2. Then create layers containing the preferred, unpreferred, and important locations of Töölö respondents only (select the right features using the zip code-based expression on the three layers; save the selections as new layers).

- Figure 

8. **Visualize the point feature layers with different colors in Symbology.**
	- For example: Unpreferred wind park sites as red, preferred as green, etc.

9. To help with later analysis and map composition, **add a WFS layer showing the zip code areas.** Do this by connecting to either: 
	1.  Helsinki Region EnvironmentalServices’WFS, https://kartta.hsy.fi/geoserver/wfs – the title of the right zip code layer is pks_postinumeroalueet_2022, and in the attribute table of this layer, the field name for zip codes is posno – or
	2. City of HelsinkiWFS, http://kartta.hel.fi/ws/geoserver/avoindata/wfs – the title of the right layer is Postinumeroalue, and the right field is named tunnus
	3. Select the zip code areas of Vuosaari and Töölö, and save them as separate layers you can use for your visualization.

---

### Creating the directional distribution analysis for the region 

10. **Download the plugin *Standard Deviational Ellipse***
	- After the download and installation is complete, it should be found under the Vector
drop-down menu.

11. **Use the plugin to create the default Yuill ellipses for the unpreferred locations of the Töölö
and Vuosaari respondents**
	1. Save the resulting ellipses as shapefiles (Make permanent)
	2. To make the interpretation easier, you can make the ellipses transparent or have them have outlines only and no fill
	3. If you wish, you can calculate standard deviational ellipses for other kinds of places, too – e.g., preferred locations, or
		- If you want to calculate an ellipse that takes into consideration the unpreferred locations of both Töölö and Vuosaari residents, but not those of respondents from other parts: first create a new shapefile layer containing the Töölö and Vuosaari residents using the Merge vector layers tool (found in Processing toolbox), for example.

---

### Optional: Hexa-grid analysis for wind park locations

12. UsingMMQGIS plugin, create a hexagonal grid that covers the municipal borders of Helsinki
	1. A good size for the hexagons could be approximately 500m x ~500m or 750m x ~750m.
	2. Make sure that the grid has a same coordinate system as your point features. (To change it: Save features as → select the correct coordinate system.)

13. Calculate the number of preferred and unpreferred points within each grid.
	1. Hint: Count points in polygon -tool might be helpful here
	2. Create a new field to represent whether the grid has more preferred locations or unpreferred points.

14. Compose a map of the outcome, include it in your report and analysis.
	- Visualize to highlight the most preferred and most unpreferred areas for wind turbines
	- What kind of spatial patterns do the preferred and unpreferred places for wind turbines show?
	- Can you identify any potential conflict areas?


---

### Map visualization  

12. **Compose maps about the possible NIMBY attitudes of Töölö and Vuosaari regarding windmills.**
	1. You decide the number of maps and what exactly eachmap contains.
		- But the map should support your analysis and its conclusion
		- Thinking about what to include and how included features are visualized on the map is always important, but increasingly so when there’s high numbers of features on the map.
	2. Remember to include a north arrow, a legend, and a scale bar into each map!
	3. Hint: You can reproject the data on-the-fly to EPSG:3067 for visual purposes – this ought to look better than the global projection. Select current project CRS from the bottom right corner.


	

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJhdGNRU1NlSXNOV3JrUEhRIjp7In
N0YXJ0Ijo4NywiZW5kIjoxMDgsInRleHQiOiIjIyBPVkVSVklF
VyAmIFBVUlBPU0UifSwieUxJaUhjdjlCTmVYT3ZTOSI6eyJzdG
FydCI6MzI2NCwiZW5kIjozMjc0LCJ0ZXh0IjoiQ09NUExFVElP
TiJ9LCJaRE5CUUU0VXJENGR2c0JJIjp7InN0YXJ0Ijo2MDExLC
JlbmQiOjYwMTksInRleHQiOiItIEZpZ3VyZSJ9LCI3THBVekpy
bkxEQ290cVpoIjp7InN0YXJ0Ijo2MTgxLCJlbmQiOjYxODksIn
RleHQiOiItIEZpZ3VyZSJ9LCJ6UGJMM3FGOGJSVVRWNnlwIjp7
InN0YXJ0Ijo2NDAyLCJlbmQiOjY0MTAsInRleHQiOiItIEZpZ3
VyZSJ9LCJKejFPbld2REs2M2VYRkc1Ijp7InN0YXJ0Ijo5ODc0
LCJlbmQiOjk4ODIsInRleHQiOiItIEZpZ3VyZSJ9fSwiY29tbW
VudHMiOnsiMXJneWlGY1dnNjI2NDY0bSI6eyJkaXNjdXNzaW9u
SWQiOiJhdGNRU1NlSXNOV3JrUEhRIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjox
Njg3ODUzODg3MzkwfSwiS3lDNkY1VVZGbWdyR0pOciI6eyJkaX
NjdXNzaW9uSWQiOiJ5TElpSGN2OUJOZVhPdlM5Iiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVG9vIG11Y2g/IiwiY3JlYX
RlZCI6MTY4Nzg1NDQ2ODY2NH0sInVvekIwWWxLdG5KVlE2NEQi
OnsiZGlzY3Vzc2lvbklkIjoiWkROQlFFNFVyRDRkdnNCSSIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJl
IiwiY3JlYXRlZCI6MTY4Nzg1NDc1NzY3OH0sIlRUcXRzaG1FV0
lvM1I2NFUiOnsiZGlzY3Vzc2lvbklkIjoiN0xwVXpKcm5MRENv
dHFaaCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Nzg1NDg0NDU5N30sInFh
bWNTd0pTSERkSDZ4TFIiOnsiZGlzY3Vzc2lvbklkIjoielBiTD
NxRjhiUlVUVjZ5cCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Nzg1NDg4Mj
Y1NH0sIjVHVFRmVndqSXhPdFhEdzgiOnsiZGlzY3Vzc2lvbklk
IjoiSnoxT25XdkRLNjNlWEZHNSIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBmaWd1cmUiLCJjcmVhdGVkIjoxNjg3
ODU1NDMwNjI5fX0sImhpc3RvcnkiOlstMzE3MDI2NTQ1LDI2Mj
g0OTE4M119
-->