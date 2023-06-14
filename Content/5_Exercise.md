### Fundamentals of Geographic Information Systems (GIS)

# Exercise 5: 

## OVERVIEW & PURPOSE
This tutorial uses data from a historical event in London, which many people consider to be the original use of map-ping to understand disease transmission. In the 1800’s, London was a rapidly growing city, with huge amounts of migration from rural England to the city. However, the city lacked modern infrastructure, and disease and over-crowding was rife.

In 1854, there was a large cholera outbreak in London, with 120 deaths within three days in the Soho area of the city. Public health officials in the city were convinced that many diseases – including cholera – were spread by ‘mi-asma’, or toxic air and poor hygiene. However, a doctor and scientist in London, John Snow, was convinced that it was spread through contaminated water, but needed to find evidence to support his theory and convince city offi-cials to close contaminated water pumps. To do this, he surveyed households in the area, plotted the locations of households with deaths, and used this to quantitative data to develop a theory about the contaminated water source.

Henry Whitehead – the local priest – knew the area and residents in Soho well, and initially did not agree with John Snow’s theory about the contaminated water pump because he knew of residents who drank from the well and did not get sick. He began his own study, interviewing residents using a qualitative social science approach, and eventu-ally came to agree with the theory about the contaminated pump. Crucially, it was Whitehead’s interviews that al-lowed the source of the contamination to be identified.

## OBJECTIVES

In this tutorial, we will learn about importing survey data and using QGIS to create a heatmap using this data, thus re-creating one of the most famous epidemiological studies using modern GIS tools. The research question we want to ask ourselves is:
- What water pump was the source of the 1854 cholera outbreak in London?

## DATA USED/NEEDED

## COMPLETION

## EXERCISE PHASES

### Getting familiar with the data

1. Save the downloaded GIS data from Moodle in a folder for this exercise and extract it. The data includes:
	- deathAddresses.csv, a file with the locations of households with cholera deaths and the number of deaths 
	- Study_Area.shp – A shapefile that describes our area of interest.
	- Snow-cholera-map-1_modified - this is a georeferenced image of the map from John Snow’s original report on the cholera outbreak of 1854 
	- Water_Pumps.geojson. This shows the location of water pumps. The file type – a geojson – is an-other standard for representing geographical features, commonly used to transmit data in web applications. 
	- Snow-cholera-map-1_modified.tif, a raster showing a map of the area in 1854.

3. Open QGIS on your computer and start a new project. Save it with a new name under the folder for this exercise.

4. Import the Study_Area.shp file, to add it to your map project. Change the symbology to make the study area hollow by right-clicking the layer, choosing Properties, and then changing the Symbology.

5. Let’s bring in some Google Earth data into our map using XYZ tiles to give the map some more context (Figure 1).
	- If you haven’t connected to Google Earth, right-click XYZ tiles and choose New Connection
	- Give it a name (like Google Satellite), and enter the URL for the data: https://mt1.google.com/vt/lyrs=s&x={x}&y={y}&z={z}
	- Press OK and then double-click the Google Satellite in the browser window. The layer will then show up in the layer panel and in your map.
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJ4MTV3V05CSzZKRHc3Vml2Ijp7In
N0YXJ0IjoxOTk1LCJlbmQiOjIwMTQsInRleHQiOiIjIyBEQVRB
IFVTRUQvTkVFREVEIn0sIjZ1RXQxNkV3VXNNSTFGc0QiOnsic3
RhcnQiOjIwMTYsImVuZCI6MjAyOSwidGV4dCI6IiMjIENPTVBM
RVRJT04ifSwid1BiRHU5QUlWN2kyemt1dyI6eyJzdGFydCI6Mj
QxNywiZW5kIjoyNDMwLCJ0ZXh0IjoiZ2VvcmVmZXJlbmNlZCJ9
fSwiY29tbWVudHMiOnsiR25kUjNoeGhkcXY5bkhyMSI6eyJkaX
NjdXNzaW9uSWQiOiJ4MTV3V05CSzZKRHc3Vml2Iiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHNlY3Rpb24iLCJjcm
VhdGVkIjoxNjg2NzI3MzczMzgwfSwidFl3R3hidEdadjhHRFNl
aSI6eyJkaXNjdXNzaW9uSWQiOiI2dUV0MTZFd1VzTUkxRnNEIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHNlY3Rp
b24iLCJjcmVhdGVkIjoxNjg2NzI3Mzc4Nzk2fSwiZkJqazNsV2
ZPMXpPUWxwdSI6eyJkaXNjdXNzaW9uSWQiOiJ3UGJEdTlBSVY3
aTJ6a3V3Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiTG
V0IHN0dWRlbnRzIGRvIHRoaXM/IiwiY3JlYXRlZCI6MTY4Njcy
NzU2NzEwOH19LCJoaXN0b3J5IjpbLTIwNjE5MjA1NTksMTI3OT
EyNTQ5OV19
-->