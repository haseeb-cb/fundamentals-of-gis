
### Fundamentals of Geographic Information Systems (GIS)

# Exercise 7: Air pollution analysis

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

---

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

---

### Part 3 - Social factors and exposures

11. Let’s now examine the concentrations in different postcodes in Helsinki. To do this, we can calculate raster statistics like we did in in a previous tutorial. 
	- Open the *Zonal Statistics* tool
	- Under *Input Layer*, select Postcodes_air_pollution. This tells QGIS that you want to calculate sta-tistics within these postcode boundaries (the ‘zones’)
	- Under *Raster Layer*, select your Interpolated air pollution data. This tells QGIS that you want to calculate statistics from this layer.
	- Press *OK*. This will create a new vector layer that at first glance looks the same as the postcode layer. However, it now has the summary statistics for the raster joined to each postcode.

12. Open the *Attribute Table* of the new layer. You will see a column on the right that shows the average concentration. There is also a column called tr_mtu, which is the median income of households. By clicking on the column heading, you can sort the data ascending or descending. 
	- What is the postcode with the highest NO2 concentrations? 
	- What is the postcode with the lowest? 
	- What are the concentrations in the postcode with the highest median income? 
	- What is the pollution in the postcodes with the lowest median income (ignoring those with 0)? 

13. We can also join the air pollution monitoring stations point data to the postcodes. This can help us identify the number of monitoring stations in postcodes, and estimate the average concentrations based on only the monitoring stations. To do so, we will perform a spatial join.
	- Open the *Join Attributes by Location (Summary)* tool
	- Under *Input*, choose the layer you produced when you calculated the Zonal Statistics 
	- Under *Join Layer*, choose Air_pollution_monitoring_points
	- Select which *Geometric predicate* you think is best (Hint: Theory 4)
	- Under *Fields to summarize*, press the box on the right and choose NO2
	- Under *Summaries to calculate*, press the box on the right and choose *Count* and *Mean*

14. This will have created a new layer, with the default name Joined Layer. Open the attribute table. What post-code had the most NO2 monitors? How many were there?

---

### Map visualization  

15. You’ve now answered your research questions. Make a nice informative map, showing the interpolated air pollution raster, and the air pollution monitoring points. Insert a legend for concentrations, so we know how the air pollution is varying across the city.
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI5RU9OYjRkcFQ2MVpxcDk0Ijp7In
N0YXJ0Ijo2NTcsImVuZCI6Njc2LCJ0ZXh0IjoiIyMgREFUQSBV
U0VEL05FRURFRCJ9LCJPUHVWWkd5ZHcyY1R0ODBMIjp7InN0YX
J0Ijo5NywiZW5kIjoxMTgsInRleHQiOiIjIyBPVkVSVklFVyAm
IFBVUlBPU0UifSwidkhYa2RzaVdrbmlHZG03NCI6eyJzdGFydC
I6NDM1LCJlbmQiOjY1NSwidGV4dCI6Ii0gV2hhdCBhcmUgdGhl
IGNvbmNlbnRyYXRpb25zIG9mIG5pdHJvZ2VuIGRpb3hpZGUgKE
5PMikgYWlyIHBvbGx1dGlvbiBpbiB0aGUgSGXigKYifSwiOEhn
Z21EYVZQMkxMbHYxQiI6eyJzdGFydCI6MjM2MCwiZW5kIjoyND
cwLCJ0ZXh0IjoiRG9lcyBhbnl3aGVyZSBleGNlZWQgdGhlIEVV
IEFpciBRdWFsaXR5IERpcmVjdGl2ZSBsaW1pdCBvZiBhbiBhbm
51YWwgYXZlcmFnZSBvZuKApiJ9LCJZUzl4R3lWaG5WRkd1b3l0
Ijp7InN0YXJ0Ijo1ODczLCJlbmQiOjYxNTIsInRleHQiOiItIF
doYXQgaXMgdGhlIHBvc3Rjb2RlIHdpdGggdGhlIGhpZ2hlc3Qg
Tk8yIGNvbmNlbnRyYXRpb25zPyBcblx0LSBXaGF0IGlzIHRoZS
Bwb3PigKYifSwickhsdmZReTdIcHAwOEtVdiI6eyJzdGFydCI6
Njk4OSwiZW5kIjo3MDUxLCJ0ZXh0IjoiV2hhdCBwb3N0LWNvZG
UgaGFkIHRoZSBtb3N0IE5PMiBtb25pdG9ycz8gSG93IG1hbnkg
d2VyZSB0aGVyZT8ifX0sImNvbW1lbnRzIjp7InN1Qmc5U0RVbz
E3a2FrYkoiOnsiZGlzY3Vzc2lvbklkIjoiOUVPTmI0ZHBUNjFa
cXA5NCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BzZWN0aW9uIiwiY3JlYXRlZCI6MTY4Nzc2ODQ2MTIzOH0sImxj
VWxhd05SR2lnVnBjOEciOnsiZGlzY3Vzc2lvbklkIjoiT1B1Vl
pHeWR3MmNUdDgwTCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4
dCI6IkFkZCBzZWN0aW9uIiwiY3JlYXRlZCI6MTY4Nzc2ODQ3OD
Y0Nn0sIktvUTJiZVhaZGc3ZEJoQ0YiOnsiZGlzY3Vzc2lvbklk
IjoidkhYa2RzaVdrbmlHZG03NCIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBzZWN0aW9uIGluIG1vb2RsZSB0byBm
aWxsIHRoZXNlIG91dCIsImNyZWF0ZWQiOjE2ODc3NjkwMDUxND
J9LCJWU2FjaEJZQ3UyVmJ3ZkloIjp7ImRpc2N1c3Npb25JZCI6
IjhIZ2dtRGFWUDJMTGx2MUIiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgc2VjdGlvbiBpbiBtb29kbGUgdG8gZmls
bCB0aGVzZSBvdXQiLCJjcmVhdGVkIjoxNjg3NzY5MDExMTUwfS
wiYjJTbkp5Q1l0bHptZUtvayI6eyJkaXNjdXNzaW9uSWQiOiJZ
Uzl4R3lWaG5WRkd1b3l0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQWRkIHNlY3Rpb24gaW4gbW9vZGxlIHRvIGZpbGwg
dGhlc2Ugb3V0IiwiY3JlYXRlZCI6MTY4Nzc2OTg5MjE1N30sIl
kxcGFyT1dSaXljS0RpaUIiOnsiZGlzY3Vzc2lvbklkIjoickhs
dmZReTdIcHAwOEtVdiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidG
V4dCI6IkFkZCBzZWN0aW9uIGluIE1vb2RsZSB0byBmaWxsIHRo
aXMgb3V0IiwiY3JlYXRlZCI6MTY4Nzc3MDExODc1N319LCJoaX
N0b3J5IjpbLTE4ODczNDI2MTIsMjg5NzAzNjI1LDM2OTI1NTQ0
LC0xODMyNTQ3MTA1LDE3Njc3MDQxMV19
-->