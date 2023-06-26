
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
-
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI5RU9OYjRkcFQ2MVpxcDk0Ijp7In
N0YXJ0Ijo2MzQsImVuZCI6NjUzLCJ0ZXh0IjoiIyMgREFUQSBV
U0VEL05FRURFRCJ9LCJPUHVWWkd5ZHcyY1R0ODBMIjp7InN0YX
J0Ijo3NCwiZW5kIjo5NSwidGV4dCI6IiMjIE9WRVJWSUVXICYg
UFVSUE9TRSJ9fSwiY29tbWVudHMiOnsic3VCZzlTRFVvMTdrYW
tiSiI6eyJkaXNjdXNzaW9uSWQiOiI5RU9OYjRkcFQ2MVpxcDk0
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHNlY3
Rpb24iLCJjcmVhdGVkIjoxNjg3NzY4NDYxMjM4fSwibGNVbGF3
TlJHaWdWcGM4RyI6eyJkaXNjdXNzaW9uSWQiOiJPUHVWWkd5ZH
cyY1R0ODBMIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIHNlY3Rpb24iLCJjcmVhdGVkIjoxNjg3NzY4NDc4NjQ2fX
0sImhpc3RvcnkiOlstNDQ1NzI1NzcxLC0xODMyNTQ3MTA1LDE3
Njc3MDQxMV19
-->