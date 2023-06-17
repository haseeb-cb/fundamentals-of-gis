### Fundamentals of Geographic Information Systems (GIS)

# Exercise 4: 

## OVERVIEW & PURPOSE

## OBJECTIVES

## DATA USED

## COMPLETION

## EXERCISE PHASES

### Part 1: The ring rail line visualization
The Ring Rail Line, also known as “Kehärata”, is a railway line that was opened in 2015 in the Helsinki capital region. The new rail route created a connection between Helsinki-Vantaa Airport and the Helsinki region commuter traffic network by joining the existing Vantaankoski and Main line branches. The approximately 18-kilometer-long Ring Rail line connects to the current rail network at the Vantaankoski and Hiekkaharju stations and the track between Viinikkala and Ruskeasanta goes in an underground tunnel.

To 2015 opening, altogether five new stations were constructed at Leinelä, Helsinki-Vantaa Airport, Aviapolis, Kivistö and Vehkala. Reservations have also been made for four additional stations at Petas, Viinikkala, Ruskeasanta and Lapinkylä to be built later in the second phase. Out of these, the Aviapolis and Airport stations are located underground. Similarly, the reserved stations of Ruskeasanta and Viinikkala will be located underground.

The Ring Rail line improves the accessibility of the airport area and the suburbs along the route, cut down the journey times for over 12 million airport passengers per annum and it is also estimated to create employment for over 60 000 people.

#### 1.1: Getting the data
1. Go to Moodle, download the data necessary for the task, save it in a folder for this exercise, and add it to your QGIS project. 
	- Go through the data, what does it describe? What order of layers would be good to work with?

3. We need to have the Ring Rail Line in geospatial format. One option is to digitize it based on a basic map. Other is to find the data online – let’s do that for practice!
	- HRI offers easy access to open data sources between the cities of Helsinki, Espoo, Vantaa and Kauniainen. Follow the link to Helsinki-Region Transport’s public transport lines from 2021-2022 and open the preview in HSL’s website. https://public-transport-hslhrt.opendata.arcgis.com/datasets/hsln-linjat-4/

- Picture 

	- As you can see, the dataset is big and we don’t need everything it contains. You could download the whole data and edit it on your computer, but you can also filter the data before downloading it. You’d have to figure out what different attributes mean – unfortunately in this case the information is in Finnish, so needed code explanations are provided here. You can also check them through the link below and clicking “Aineiston kuvaus (pdf)”.
		- https://public-transport-hslhrt.opendata.arcgis.com/datasets/HSLHRT::hsln-linjat-4/about
	- You can select features by clicking “Filter data” on the left of the page.
		- JL_LAJI: 12, filters by local VR traffic
		- VERKKO: 4, filters on train traffic
		- AIK_VOIM: 1, filters on in-use tracks
		- SUUNTA: 1, filter on 1 direction
		- You will notice when you filter on these that the visual output barely changes, we are filtering on as much as possible to get as little duplicate lines as possible so we have to do as little manual adjustments ourselves. For this purpose we are only looking to extract the rough location of the line, and thus for example a single direction is sufficient. 
	- When the selection is done, you can download it by going to the Download tab under the Filter data tab. Click the “toggle filters” to choose only the selected features, and download the data as a Shapefile. 

- Picture 

3. Add the data you downloaded to your QGIS project and inspect the features, what do you notice? 
	- There are still duplicate entries for the Ring Rail Line and there are other entries we do not need and are in the way
	- We want to end up with only the Ring Rail Line, go through the attribute table and find which entry describes the full ring Rail Line, export this to a new layer, you can remove the original. 

#### 1.2: Making a map visualization of the new ring rail line
4. For visualization purposes we want to have underground part of the rail as a separate segment. You can do this by splitting the ring rail line feature you exported into multiple features. 
	- We can use Google Satellite imagery and the overview map of the ring rail line to find the places where we need to split the ring rail line
		- You might want to change the symbology of your ring rail line to make it more visible for editing
	- Select your Ring Rail Line layer, toggle on editing, and navigate to Edit > Edit Geometry > Split features
		- How to Split and Merge Line in QGIS: https://www.youtube.com/watch?v=vLL4hdDO1zU
	- Split the line into sections for overground and underground track
		- Create a field which describes whether the track is over- or underground so we can use symbology to differentiate these (Attribute table > New Field)
	- Don't forget to save your edits and toggle off editing

5. Now look at the ring_rail_line_stations and railway_stations layers, for the visualization we would only like to have the stations that are part of the ring rail line, and have them seperated by pre-existing, new, and planned stations. 
	- Let's start by removing the stations that are not part of the ring rail line, toggle on editing for the railway_stations layer, select the stations we want to remove, and use *Delete Selected* in the editing toolbar (save edits and toggle off editing).
	- Now take a look at the attribute table of the ring_rail_line_stations layer, as you can see there is already a field for which stations are new and planned, so we can use symbology to differentiate these. 
	- Optionally: Convert the train stations from polygons to points: https://docs.qgis.org/3.16/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html#centroids
		- In thi scase, points scale better, are easier to edit, and easier to add labels to

6. Make a visualization to show the ring rail line. Show on your map: where the railway is underground, which stations are new and whatever else you find convenient. 
	- Use categorized symobology to show the different types of railway and stations
	- Don't forget to add a basemap for reference (hint: Use one that contrasts with the data)
	- Optionally you can add labels to the stations 

---

### Part 2: The ring rail line analysis
#### 2.1: Analyzing the effects on the people in the study area
As already mentioned, the Ring Rail line improves the commuter traffic network and accessibility of the suburbs along the track, but how does this show on real numbers?

5. Find out how many are notably affected by this by calculating how many people live within a radius of 1 kilometer from the stations opened in 2015? And the new and planned stations combined?
	- You can do this by doing a buffer analysis using the ring_rail_line_stations and capital_region_people data
	- Open the *Buffer* tool from the *Processing Toolbox*
	- Make a 1km buffer around the ring_rail_line_stations (input: ring_rail_line_stations, distance: 1000)
		- To only make a buffer around the stations opened in 2015, select those stations and use the *Selected features only* function in the *Buffer* tool
	- Don't forget to make the temporary layers from the buffer permanent
	- Use *Select by Location* to select the entries from the capital_region_people data that intersect with the buffers
	- Run *Basic Statistics for Fields* to get the total amount of residents living within the buffer (Input layer: Capital_region_people, selected feature only, Field to calculate: ASYHT(X))
		- Look the output log for the SUM output, this shows the total amount
	- Repeat the same steps for the other buffer

The Ring Rail Line is likely to increase the attraction for the real estate in the nearby area. This, however, will also raise the question of the noise levels caused by the Aircraft traffic around the Helsinki-Vantaa Airport. Thanks to new improved technology the aircraft noise levels have slightly dropped in recent years.

6. Find out how many people approximately live inside the dB zones: 65 or more and 50 or more in Helsinki region based on the noise levels in 2006? And the noise levels in 2010?
	- This time you don't need to create a buffer, as the dB zones already exist
	- Repeat the same steps as in step 5 to get the number of residents living within the 65 and 50 dB zones in 2006 and 2010
		- Hint: Look at the attribute tables of the noise layers (use *Selected features only* in *Select by location*)

Fill in the answers to the Moodle

*Tip : For the Capital_region_people layer field name metadata, see Appendix in Exercise 4 instructions*

#### 2.2: Planning a new airport hotel & congress center near the ring rail line
7. You work in a team that is supposed to find an optimal location for a new Airport Hotel & Congress Center to the Helsinki-Vantaa Airport area based on accessibility. Your task is to follow the given requirements and make a map visualization of the area(s) to be shown at the company meeting of where the new Hotel & Congress center could possibly be located.

**The requirements are as follows**:
- The Hotel & Congress Center has to be located within the maximum **distance of 2 kilometers from the Airport area** (but not inside it).
- The Hotel & Congress Center has to be easily accessible, thus located **within the radius of 1 kilometer from the new Ring Rail Line stations** (including the reserved ones)
- It has to be **within the radius of 500 meters from the road network**.
- The Hotel & Congress Center has to be **outside the ≥ 55 dB noise zones** caused by the airport traffic.
- The Hotel & Congress Center **cannot be built on already built up areas**.
- The Hotel & Congress Center requires **at least 5000 m2 of free building space**.

*Hint 1: The Multipart to Singlepart- geoprocessing tool can be used to detach the polygons individual features to be able to calculate their areas. This is useful when the overlay operations combine the features, but because their topology information is still stored, they can be separated using this tool.*

*Hint 2: When creating a buffer for the roads, only include ones near the airport area. A buffer or “Select by location” -tool’s buffering parameter can be helpful. Creating a buffer for all of the roads is unnecessary and takes a lot of time to process.*

8. Try to make the map as clear and informative as possible and insert the finished map with all the necessary map elements to you course report. Write also a short reflection on what was done and why.

## Appendix: Overview map of the ring rail line

- Add picture

Legend in English: Pintarata = Overground, Tunneli = tunnel, Asema = station, Asemavaraus = station reservation, Nykyiset asemat = Current stations, Hämeenlinnanväylän parannus = improvement of Hämeenlinnanväylä



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJFdFByYk5zWUdNWWhPWXRSIjp7In
N0YXJ0IjoxNDUyLCJlbmQiOjE0NTgsInRleHQiOiJNb29kbGUi
fSwicjFuaW14MW1CdWx6YVhkViI6eyJzdGFydCI6MjE1NiwiZW
5kIjoyMTY1LCJ0ZXh0IjoiLSBQaWN0dXJlIn0sIkNVTHg0QmVW
RFZzMm5GSUEiOnsic3RhcnQiOjM1MjYsImVuZCI6MzUzNSwidG
V4dCI6Ii0gUGljdHVyZSJ9LCJMNDJrTlBEb0dDY3BGU3RrIjp7
InN0YXJ0Ijo1ODkyLCJlbmQiOjYwNTcsInRleHQiOiI1LiBNYW
tlIGEgdmlzdWFsaXphdGlvbiB0byBzaG93IHRoZSByaW5nIHJh
aWwgbGluZS4gU2hvdyBvbiB5b3VyIG1hcDogd2hlcmUgdGhl4o
CmIn0sIlZWaEZ3Y2E0UHFZT0V0REIiOnsic3RhcnQiOjYzMzMs
ImVuZCI6NjM5MSwidGV4dCI6IjIuMTogQW5hbHl6aW5nIHRoZS
BlZmZlY3RzIG9uIHRoZSBwZW9wbGUgaW4gdGhlIHN0dWR5IGFy
ZWEifSwibnlYaktLeXMwcEZQQ1VubiI6eyJzdGFydCI6MTA1OT
csImVuZCI6MTA2MTAsInRleHQiOiItIEFkZCBwaWN0dXJlIn0s
InJqbU1Xa0xJYTBGWTVqQVQiOnsic3RhcnQiOjkwODIsImVuZC
I6OTc3NSwidGV4dCI6IioqVGhlIHJlcXVpcmVtZW50cyBhcmUg
YXMgZm9sbG93cyoqOlxuLSBUaGUgSG90ZWwgJiBDb25ncmVzcy
BDZW50ZXIgaGFzIHRvIGJlIGxv4oCmIn0sIk4xSDBkRXhnU0Ft
Q3ZaMlgiOnsic3RhcnQiOjM4OTcsImVuZCI6MzkwMywidGV4dC
I6ImV4cG9ydCJ9LCJUeFZLTHA3OThka2o1cE9xIjp7InN0YXJ0
Ijo1Mzc2LCJlbmQiOjUzOTEsInRleHQiOiJlZGl0aW5nIHRvb2
xiYXIifSwibkpiRFF6Q2VuSnZoS3J1QSI6eyJzdGFydCI6NDIx
MiwiZW5kIjo0MzUzLCJ0ZXh0IjoiLSBXZSBjYW4gdXNlIEdvb2
dsZSBTYXRlbGxpdGUgaW1hZ2VyeSBhbmQgdGhlIG92ZXJ2aWV3
IG1hcCBvZiB0aGUgcmluZyByYWlsIGxpbuKApiJ9LCJ5eUtYcl
lQenFMMWtMOG1DIjp7InN0YXJ0Ijo3NTUzLCJlbmQiOjc1NTQs
InRleHQiOiJYIn0sIkR4WTl1c1A1SzFhZ2xZNTkiOnsic3Rhcn
QiOjg0OTcsImVuZCI6ODUzMCwidGV4dCI6IkZpbGwgaW4gdGhl
IGFuc3dlcnMgdG8gdGhlIE1vb2RsZSJ9fSwiY29tbWVudHMiOn
siSHUxb2w3R2lGNmhCdDNjSSI6eyJkaXNjdXNzaW9uSWQiOiJF
dFByYk5zWUdNWWhPWXRSIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiQ29ycmVjdCIsImNyZWF0ZWQiOjE2ODY4OTg0MDY4
MTJ9LCJJdUc3aE5hT2k0UklhZktlIjp7ImRpc2N1c3Npb25JZC
I6InIxbmlteDFtQnVsemFYZFYiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2OD
Y4OTg3NTU5NDB9LCJXSE9hbEd4NWh5dkVKOENFIjp7ImRpc2N1
c3Npb25JZCI6IkNVTHg0QmVWRFZzMm5GSUEiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0
ZWQiOjE2ODY4OTg3ODc4MDV9LCJpczg0Z09jRnprRHd0TXlWIj
p7ImRpc2N1c3Npb25JZCI6Ikw0MmtOUERvR0NjcEZTdGsiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJHaXZlIHNvbWUgbW
9yZSBoaW50cyBvbiBob3cgdG8gZG8gdGhpcyIsImNyZWF0ZWQi
OjE2ODY4OTkwMDkwMTN9LCJHVU1tQ1RKaEt4azRQU2lOIjp7Im
Rpc2N1c3Npb25JZCI6IlZWaEZ3Y2E0UHFZT0V0REIiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgc2VjdGlvbiBpbi
Btb29kbGUgd2hlcmUgdG8gZmlsbCBpbiBhbnN3ZXJzIGZvciB0
aGVzZSIsImNyZWF0ZWQiOjE2ODY4OTkyNDQ5OTd9LCJVQlppa0
pMYTFaanllamhtIjp7ImRpc2N1c3Npb25JZCI6Im55WGpLS3lz
MHBGUENVbm4iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY4OTk1OTMwMDV9
LCJmcnQxRndhUEdCdXVNSGdJIjp7ImRpc2N1c3Npb25JZCI6In
JqbU1Xa0xJYTBGWTVqQVQiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJGdWxseSBleHBsYWluIGhvdyB0aGV5IGRvIHRoaX
MiLCJjcmVhdGVkIjoxNjg2ODk5NjA1MDA1fSwiMkVjT0lSRkZM
YTVYaTlSbSI6eyJkaXNjdXNzaW9uSWQiOiJOMUgwZEV4Z1NBbU
N2WjJYIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRk
IGhpbnQiLCJjcmVhdGVkIjoxNjg2OTgzMDE5MjkwfSwiU3lXeU
JNSlVYY1BxdWdsayI6eyJkaXNjdXNzaW9uSWQiOiJUeFZLTHA3
OThka2o1cE9xIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2OTgzNzk5NTYz
fSwiSnVOTkVibTdIb0JKNTYyRSI6eyJkaXNjdXNzaW9uSWQiOi
JuSmJEUXpDZW5KdmhLcnVBIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQWRkIGhpbnQiLCJjcmVhdGVkIjoxNjg2OTg0NT
g5NTgwfSwiMFkwY0pRUzdkTEMzRnNQWCI6eyJkaXNjdXNzaW9u
SWQiOiJ5eUtYcllQenFMMWtMOG1DIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQWRkIG1lYW5pbmciLCJjcmVhdGVkIjox
Njg2OTg2MzU4MzMwfSwiZEtCY0gxZ0dncjJsQXc3cyI6eyJkaX
NjdXNzaW9uSWQiOiJEeFk5dXNQNUsxYWdsWTU5Iiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IHJlZmVyZW5jZSIsIm
NyZWF0ZWQiOjE2ODY5ODY0MjkxMDV9fSwiaGlzdG9yeSI6Wy0x
Nzg1ODg1NzM0LC01MDk4MDY2OTEsLTQ0OTExNTYwMywtMjc5OT
M3MDg5LDIwMTE5OTY3MTAsMTcwMDIzMzgxOSw1MTE5OTk5MjIs
MTg3MjEwNjYxNiwtNTQ4NjYyNDAsMjAzODI0NjAxOCwtMjkzNj
k0NzkxLC0xMzgwMTUxMjg4LDczMDk5ODExNl19
-->