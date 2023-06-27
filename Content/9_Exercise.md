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

1. **Head over to Helsinki Region Infoshare** (http://www.hri.fi/en/), search for “Helsingin
tuulivoimakysely 2015” or “Wind power survey for Helsinki 2015”, and download the wind
power survey data (the data are in Excel format)

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJhdGNRU1NlSXNOV3JrUEhRIjp7In
N0YXJ0Ijo4NywiZW5kIjoxMDgsInRleHQiOiIjIyBPVkVSVklF
VyAmIFBVUlBPU0UifSwieUxJaUhjdjlCTmVYT3ZTOSI6eyJzdG
FydCI6MzI2NCwiZW5kIjozMjc0LCJ0ZXh0IjoiQ09NUExFVElP
TiJ9fSwiY29tbWVudHMiOnsiMXJneWlGY1dnNjI2NDY0bSI6ey
JkaXNjdXNzaW9uSWQiOiJhdGNRU1NlSXNOV3JrUEhRIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLC
JjcmVhdGVkIjoxNjg3ODUzODg3MzkwfSwiS3lDNkY1VVZGbWdy
R0pOciI6eyJkaXNjdXNzaW9uSWQiOiJ5TElpSGN2OUJOZVhPdl
M5Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVG9vIG11
Y2g/IiwiY3JlYXRlZCI6MTY4Nzg1NDQ2ODY2NH19LCJoaXN0b3
J5IjpbLTU2NzM4NjAzOV19
-->