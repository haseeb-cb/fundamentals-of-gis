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

2. Open QGIS on your computer and start a new project. Save it with a new name under the folder for this exercise.

3. Import the Study_Area.shp file, to add it to your map project. Change the symbology to make the study area hollow (no fill, only borders)

4. Let’s bring in some Google Earth data into our map using XYZ tiles to give the map some more context (Hint: Exercise 2 step 3)

- Figure 1

5. Often the data sets that you want to work with will not come as spatial data sets. They might come, for ex-ample, from observations during field work that you record in a spreadsheet. In this step we will add a table of data that contains fields with the latitude and longitude coordinates of the deaths addresses we want to analyze. In our case, this data comes in a comma-separated values (CSV) file, or a text file that uses a comma to separate values.
	
	- First let’s look at the file with the deaths data in it. If you double-click it in the folder you saved the file in, it should open in Excel or as a text file, and you will see that it has an ID column (OB-JECTID), the number of cases (Num_Cases ), an Address Column (Address), x coordinates (xcoord), and y coordinates (ycoord). These coordinates are helpful, as they let us import the data into GIS.
	- In QGIS, go to Layer -> Add Layer -> Add Delimited Text Layer 
	- Under File name, browse for the deathAddresses.csv file and select Open.
	- QGIS will read in the file, and should automatically recognise some key features of the file (Figure 2), including:
		- That the file format is comma delimited
		- That the first record in the file contains the names of the columns rather than data within the columns
		- That two of the fields in the file include spatial information relating to the x and y coordi-nates. Here, the coordinate reference system (CRS) is EPSG:4326 - WGS 84.
	- If you press Add and Close, you should see that the addresses have been added to the QGIS map.

- Figure 2

6. We have now added the addresses where there were cholera deaths, but it is in a global coordinate system, and this can cause some problems in our analysis because it is in a different coordinate system that the other data that we are going to use. Let’s reproject it to the same as the study area bounding box -EPSG:32630 UTM.
	
	- In the Processing Toolbox, search for Reproject and open the Reproject layer tool b) Choose deathAddresses.csv as the Input layer
	- Set the Target CRS as the Project CRS: EPSG:32630 UTM – WGS 84 / UTM zone 30N d) Save it as a new layer, deaths_locations.shp in your file directory
	- Press Run

- Figure 3

7. Let’s now change the symbology of the deaths_locations layer to identify addresses that had multiple deaths (Figure 3). 
	
	- Remove the original deathsAddresses csv layer by right-clicking it and selecting Remove Layer b) Right-click the new reprojected deaths_locations layer, and choose Properties and go to the Sym-bology tab.
	- Make the Symbol Graduated and the Value Num_Cases
	- Change the Method to Size. Rather than changing the colour of the symbol based on the number of cases, this will change the size of the symbol. Make the Size from 10 to 30 Map Units
	- Make the Classification Mode Natural Breaks with three classes and choose Classify
	- Press Ok.

- Figure 4

8. We now have the locations of the deaths overlaid on top of a Google image of modern London. But, things have changed a little bit in this area of London since the outbreak. Let’s bring in an old map of the area. 
	
	- Import the raster Snow-cholera-map-1_modified.tif, which is an old streetmap of the area.
	- Drag the old streetmap to be on top of the Google map and below the deaths and study area boundary layers. 
	- Right-click Snow-cholera-map-1_modified.tif and choose Properties. Under the Transparency tab, choose 65% and press Ok. This makes the raster slightly transparent, so you can also see the more modern city underneath.

- Figure 5

### Finding the source of the outbreak

9. Now, let’s start trying to identify where the outbreak has come from. First, let’s bring in data on the location of the water pumps. 
	
	- Import the file Water_Pumps.geojson
	- Right-click the layer and look at the Attribute Table. What attributes are associated with each water pump?

10. Now, we want to find out which water pumps is closest to the addresses where there have been deaths rec-orded. Thiessen polygons are a method used to divide a space into regions based on their proximity to fea-tures. That is, within a Thiessen polygon, all the deaths are closer to the point (in this case a pump) that was used to generate that polygon, than to any other point (or pump) in the feature set. Let’s create a set of Thiessen polygons based upon the locations of the Water Pumps in our project (Figure 6).
	
	- In the Processing Toolbox Window, search for Voronoi
	- Double–click the Voronoi polygons tool c) On the Voronoi tool select Water_Pumps as the Input layer
	- Set the Buffer region to 50%
	- Press Run

- Figure 6

11. Now that you have created the Voronoi polygon layer, we can see how many deaths lay within these poly-gons – i.e. the count of deaths within the vicinity of each pump. There are various ways to do this. We could use a spatial join to “allocate” each of the deaths to one of the Voronoi polygons, much like we used spatial joins previously, and then sum the number of deaths. So now, though, let’s look at the map visually. Which polygon do you think has the most deaths? Use the information tool to click on the polygon and find out the name of the pump, and make a note of it.

12. Another possible way to identify the location of the outbreak could be to find the spatial mean of the deaths – or the average x- and y-coordinate of all the features in the study area. It’s useful for tracking changes in the distribution or for comparing the distributions of different types of features. Here, we will use the Mean Center to highlight the distribution of deaths (Figure 7).
	
	- Go to Vector > Analysis Tools > Mean coordinate(s) 
	- Select deaths_locations as the Input vector layer.
	- Set the Weight field as Num_Cases. By setting the weight to be the number of cases, we are accounting for the fact that some addresses had multiple deaths when we calculated the average coor-dinates. 
	- Click Browse to save the Output Shapefile as: Deaths_Spatial_Mean to the your project folder.
	- Click OK to calculate the Mean Center and Close. What water pump is the spatial mean closest to?

- Figure 7 

13. Another way to show the distribution of cholera deaths is to create a heatmap. A heatmap is a data visuali-zation technique that shows magnitude of a phenomenon as color. In QGIS, the Kernel Density Tool cal-culates a magnitude per unit area from the point features using a kernel function to fit a smoothly tapered surface to each point. The result is a raster dataset which can reveal “hotspots” in the array of point data.
	- Go to the Processing Toolbox Window and type to search Kernel Density and open the tool Heatmap (Kernel Density Estimation) 
	- Select the deaths_locations layer as the Point Layer.
	- Set the Radius option to 50 (this is in meters).
	- Select Num_Cases as the Weight Field. This will take into account the number of deaths at each address.
	- Press Run

14. Edit the Symbology of the heatmap layer in it’s properties. This can include:
	- Changing the symbology to singleband pseudocolour
	- Changing the legend settings to reduce the number of significant figures. In the symbology tab, go to Legend Settings -> Number Format (Customise). Round the Decimal places to 0.

- Figure 8

15. All done! Make a final map in the layout manager, showing the locations of deaths, the water pumps, and the heatmap like in Figure 9 below. Remember to include a legend, with information that readers can un-derstand.

- Figure 9 
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJ4MTV3V05CSzZKRHc3Vml2Ijp7In
N0YXJ0IjoxOTk1LCJlbmQiOjIwMTQsInRleHQiOiIjIyBEQVRB
IFVTRUQvTkVFREVEIn0sIjZ1RXQxNkV3VXNNSTFGc0QiOnsic3
RhcnQiOjIwMTYsImVuZCI6MjAyOSwidGV4dCI6IiMjIENPTVBM
RVRJT04ifSwid1BiRHU5QUlWN2kyemt1dyI6eyJzdGFydCI6Mj
QxNywiZW5kIjoyNDMwLCJ0ZXh0IjoiZ2VvcmVmZXJlbmNlZCJ9
LCJvbnVZNmdaUHVLWnFPMnk2Ijp7InN0YXJ0IjozMTkwLCJlbm
QiOjMyMDAsInRleHQiOiItIEZpZ3VyZSAxIn0sInpURFRhd21H
N2ZhdnZZS3oiOnsic3RhcnQiOjQ3NTIsImVuZCI6NDc2MiwidG
V4dCI6Ii0gRmlndXJlIDIifSwiQXhISWQ3dXRERktIaGtyMCI6
eyJzdGFydCI6NTM5NSwiZW5kIjo1NDA1LCJ0ZXh0IjoiLSBGaW
d1cmUgMyJ9LCJLTlplRHVqbEZZdnR3MDNLIjp7InN0YXJ0Ijo2
MDc5LCJlbmQiOjYwODksInRleHQiOiItIEZpZ3VyZSA0In0sIn
pBTk5vdExwRnpQUTlGOTIiOnsic3RhcnQiOjY3MzQsImVuZCI6
Njc0NCwidGV4dCI6Ii0gRmlndXJlIDUifSwibXhEUG9hajJISn
I5S0FUMiI6eyJzdGFydCI6NzgwNiwiZW5kIjo3ODE2LCJ0ZXh0
IjoiLSBGaWd1cmUgNiJ9LCJiTVRCWG93UFR0QlExWUpRIjp7In
N0YXJ0Ijo5MzEwLCJlbmQiOjkzMjAsInRleHQiOiItIEZpZ3Vy
ZSA3In0sImxTOXZtam5MUlRKb3k0V1EiOnsic3RhcnQiOjEwND
I5LCJlbmQiOjEwNDM5LCJ0ZXh0IjoiLSBGaWd1cmUgOCJ9LCJY
U1Y4dXA3OThXSFpMdXRtIjp7InN0YXJ0IjoxMDY2MywiZW5kIj
oxMDY3MywidGV4dCI6Ii0gRmlndXJlIDkifX0sImNvbW1lbnRz
Ijp7IkduZFIzaHhoZHF2OW5IcjEiOnsiZGlzY3Vzc2lvbklkIj
oieDE1d1dOQks2SkR3N1ZpdiIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IkFkZCBzZWN0aW9uIiwiY3JlYXRlZCI6MTY4Nj
cyNzM3MzM4MH0sInRZd0d4YnRHWnY4R0RTZWkiOnsiZGlzY3Vz
c2lvbklkIjoiNnVFdDE2RXdVc01JMUZzRCIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBzZWN0aW9uIiwiY3JlYXRl
ZCI6MTY4NjcyNzM3ODc5Nn0sImZCamszbFdmTzF6T1FscHUiOn
siZGlzY3Vzc2lvbklkIjoid1BiRHU5QUlWN2kyemt1dyIsInN1
YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkxldCBzdHVkZW50cy
BkbyB0aGlzPyIsImNyZWF0ZWQiOjE2ODY3Mjc1NjcxMDh9LCJV
elp1bHBKb3lUdWV6cEtCIjp7ImRpc2N1c3Npb25JZCI6Im9udV
k2Z1pQdUtacU8yeTYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY3Mjc3Mj
A5ODl9LCJnVWRjOWo4VXlNWkhJV1E5Ijp7ImRpc2N1c3Npb25J
ZCI6InpURFRhd21HN2ZhdnZZS3oiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODY3MjgxNTcxODl9LCJhaUdzemZEbU9Na09vRG4zIjp7ImRpc2
N1c3Npb25JZCI6IkF4SElkN3V0REZLSGhrcjAiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODY3MjgxNjk3NDh9LCJHcGxveHV0cEliZTFOeU5n
Ijp7ImRpc2N1c3Npb25JZCI6IktOWmVEdWpsRll2dHcwM0siLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVy
ZSIsImNyZWF0ZWQiOjE2ODY3MjgyMjg4Mjl9LCJhYWRjdVhlck
JvUEx5UHFGIjp7ImRpc2N1c3Npb25JZCI6InpBTk5vdExwRnpQ
UTlGOTIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZG
QgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY3MjgzMDM5MDB9LCJF
SmtYangyTlIyTDNWVm41Ijp7ImRpc2N1c3Npb25JZCI6Im14RF
BvYWoySEpyOUtBVDIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY3Mjg0OD
E5MjV9LCJlc1JOYldsQjU2aGRsVFRYIjp7ImRpc2N1c3Npb25J
ZCI6ImJNVEJYb3dQVHRCUTFZSlEiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODY3Mjg1NjUwNzB9LCJqZEZGRnhDZzhFQUVZaGJaIjp7ImRpc2
N1c3Npb25JZCI6ImxTOXZtam5MUlRKb3k0V1EiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODY3Mjg2NDUwNDR9LCJ6WW5Dak8zRHl1UzQ4T0VF
Ijp7ImRpc2N1c3Npb25JZCI6IlhTVjh1cDc5OFdIWkx1dG0iLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVy
ZSIsImNyZWF0ZWQiOjE2ODY3Mjg2Njg0MjB9fSwiaGlzdG9yeS
I6WzE2MTc0NjQwNTIsNTQ5MTkyMDY2LDEyNzkxMjU0OTldfQ==

-->