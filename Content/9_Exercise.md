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
		- 
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
VyZSJ9fSwiY29tbWVudHMiOnsiMXJneWlGY1dnNjI2NDY0bSI6
eyJkaXNjdXNzaW9uSWQiOiJhdGNRU1NlSXNOV3JrUEhRIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg3ODUzODg3MzkwfSwiS3lDNkY1VVZGbW
dyR0pOciI6eyJkaXNjdXNzaW9uSWQiOiJ5TElpSGN2OUJOZVhP
dlM5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVG9vIG
11Y2g/IiwiY3JlYXRlZCI6MTY4Nzg1NDQ2ODY2NH0sInVvekIw
WWxLdG5KVlE2NEQiOnsiZGlzY3Vzc2lvbklkIjoiWkROQlFFNF
VyRDRkdnNCSSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Nzg1NDc1NzY3OH
0sIlRUcXRzaG1FV0lvM1I2NFUiOnsiZGlzY3Vzc2lvbklkIjoi
N0xwVXpKcm5MRENvdHFaaCIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Nzg1
NDg0NDU5N30sInFhbWNTd0pTSERkSDZ4TFIiOnsiZGlzY3Vzc2
lvbklkIjoielBiTDNxRjhiUlVUVjZ5cCIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZC
I6MTY4Nzg1NDg4MjY1NH19LCJoaXN0b3J5IjpbMTY5MDc4OTEw
XX0=
-->