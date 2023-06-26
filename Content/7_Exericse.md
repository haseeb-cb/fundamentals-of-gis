
### Fundamentals of Geographic Information Systems (GIS)

# Exercise 7:

## OVERVIEW & PURPOSE

## OBJECTIVES

In this tutorial, we will learn about spatial interpolation using QGIS. We will work with point data from air pollution monitoring stations in Helsinki to estimate air pollution levels in locations where there are no stations available. We will be asking ourselves the following research questions:

- What are the concentrations of nitrogen dioxide (NO2) air pollution in the Helsinki region?
- Do any areas exceed the EU recommended limit?
- What is the concentration in the wealthiest postcode? And the least wealthy?

## DATA USED/NEEDED

## Completion

Work in pairs or individually. Complete the exercise and submit a short report containing at least the following:

1. Maps of the outcome of the exercise

	- Remember: all maps should have a legend, a scale bar and a north arrow

	- Use the tips from the Crash Course to improve your map

2. A short reflection (200-300 words) on this exercise and your map

## EXERCISE PHASES

### Part 1 - Loading data

1. Save and extract the downloaded GIS data in a folder for this project. We have data on the location of air pollution monitoring sites in the Helsinki region.

2. Load the file *Air_pollution_monitoring_points.shp* into your QGIS project.

3. Examine the attribute table o fthe layer you added, what do you see?
	-  We can see that each point has some data associated with it, including the nitrogen dioxide concentration (NO2), the year of the measurement (Vuosi), the type of measurement station (Tyyppi), the location, and more.

4. Consider if it would be helpful to have some context during this analysis, maybe add aerial imagery or some other basemap for now? 

5. Let’s also add some postcode boundaries. Add the layer *Postcodes_air_pollution.shp* to the QGIS project.

6. Let’s change the symbology of the postcode boundaries to make it so that you can see the aerial imagery beneath them.
	- Change the symbology in such a way that you can see your basemap under it (e.g. remove the fill or change the transparency)  

7. Let’s also change the symbology of the monitoring stations
	- Let’s make these a graduated symbol. Choose NO2 as the *Value*.  You will now see a map with the monitoring stations coloured according to the monitored NO2 levels. Does anywhere exceed the EU Air Quality Directive limit of an annual average of 40 micrograms per cubic metre? 

### Part 2 - Spatial Interpolation

8. Now that we have our air monitoring station data loaded, we can see their locations and have an idea of what the annual average NO2 levels recorded at these stations are. But what about where there are no monitoring stations? Can we estimate what the concentrations are in other areas, based on the closest stations? GIS has the ability to interpolate between these data points to estimate concentrations elsewhere.

9. Let’s interpolate NO2 concentration between the monitoring stations. 
	-   Open the *IDW Interpolation tool*, in the *IDW Interpolation tool*, set:
		- *Vector Layer*: Air_pollution_monitoring_points, this means tells QGIS that you want to interpolate from this vector dataset.
		- *Interpolation Attribute*: NO2, the value associated with the monitoring stations that we want to interpolate.
		- Click the + symbol to add it to the list of items to interpolate
		- *Extent*: click the down arrow to the right of the extent box and choose *Calculate from Layer* > Air_pollution_monitoring_points. This will limit the interpolation to the areas covered by the monitoring stations – where we have data. Otherwise, the tool may try to interpolate over a wider area, and could lead to errors.
		- *Output Raster Size* will define the spatial resolution of the interpolation – meaning the size of the grid (or pixels). Too small a grid size, and you create a very large file and the results could be mis-leading (i.e. it could make people think we know the pollution in a 1m2 area, which we don’t). Too large, and we won’t get a good idea of the variation because the grid will be so large. We don’t have many monitoring stations, and it is computationally more difficult to produce a large raster, so let’s make it quite coarse. Set the X and Y pixel size as 50 for both.
	- Run the tool

10. The interpolation has produced a raster from point data. We can see how the IDW algorithm has estimated the concentration of air pollution between the different points as a continuous grid, where each pixel has a value. In reality, the spatial concentration of air pollution is more varying, with differences due to the pres-ence of pollution emission sources, urban canyons, wind, and other factors, and will vary over time as well. But, this gives us an initial estimate of how concentrations change across Helsinki.

### Part 3 - Social factors and exposures

11. Let’s now examine the concentrations in different postcodes in Helsinki. To do this, we can calculate raster statistics like we did in in a previous tutorial. To do this again, search in the Processing Toolbox for Zonal statistics.
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI5RU9OYjRkcFQ2MVpxcDk0Ijp7In
N0YXJ0Ijo2MzQsImVuZCI6NjUzLCJ0ZXh0IjoiIyMgREFUQSBV
U0VEL05FRURFRCJ9LCJPUHVWWkd5ZHcyY1R0ODBMIjp7InN0YX
J0Ijo3NCwiZW5kIjo5NSwidGV4dCI6IiMjIE9WRVJWSUVXICYg
UFVSUE9TRSJ9LCJ2SFhrZHNpV2tuaUdkbTc0Ijp7InN0YXJ0Ij
o0MTIsImVuZCI6NjMyLCJ0ZXh0IjoiLSBXaGF0IGFyZSB0aGUg
Y29uY2VudHJhdGlvbnMgb2Ygbml0cm9nZW4gZGlveGlkZSAoTk
8yKSBhaXIgcG9sbHV0aW9uIGluIHRoZSBIZeKApiJ9LCI4SGdn
bURhVlAyTExsdjFCIjp7InN0YXJ0IjoyMzM3LCJlbmQiOjI0ND
csInRleHQiOiJEb2VzIGFueXdoZXJlIGV4Y2VlZCB0aGUgRVUg
QWlyIFF1YWxpdHkgRGlyZWN0aXZlIGxpbWl0IG9mIGFuIGFubn
VhbCBhdmVyYWdlIG9m4oCmIn19LCJjb21tZW50cyI6eyJzdUJn
OVNEVW8xN2tha2JKIjp7ImRpc2N1c3Npb25JZCI6IjlFT05iNG
RwVDYxWnFwOTQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgc2VjdGlvbiIsImNyZWF0ZWQiOjE2ODc3Njg0NjEyMz
h9LCJsY1VsYXdOUkdpZ1ZwYzhHIjp7ImRpc2N1c3Npb25JZCI6
Ik9QdVZaR3lkdzJjVHQ4MEwiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgc2VjdGlvbiIsImNyZWF0ZWQiOjE2ODc3
Njg0Nzg2NDZ9LCJLb1EyYmVYWmRnN2RCaENGIjp7ImRpc2N1c3
Npb25JZCI6InZIWGtkc2lXa25pR2RtNzQiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgc2VjdGlvbiBpbiBtb29kbG
UgdG8gZmlsbCB0aGVzZSBvdXQiLCJjcmVhdGVkIjoxNjg3NzY5
MDA1MTQyfSwiVlNhY2hCWUN1MlZid2ZJaCI6eyJkaXNjdXNzaW
9uSWQiOiI4SGdnbURhVlAyTExsdjFCIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQWRkIHNlY3Rpb24gaW4gbW9vZGxlIH
RvIGZpbGwgdGhlc2Ugb3V0IiwiY3JlYXRlZCI6MTY4Nzc2OTAx
MTE1MH19LCJoaXN0b3J5IjpbLTIwNTgxMzQzNzMsMzY5MjU1ND
QsLTE4MzI1NDcxMDUsMTc2NzcwNDExXX0=
-->