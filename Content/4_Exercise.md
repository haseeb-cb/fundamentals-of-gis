### Fundamentals of Geographic Information Systems (GIS)

# Exercise 4: 

## OVERVIEW & PURPOSE

## OBJECTIVES

## DATA USED

## COMPLETION

## EXERCISE PHASES

### Part 1: The ring rail line visualization
The Ring Rail Line, also known as “Kehärata”, is a railway line that was opened in 2015 in the Helsinki capital region. The new rail route created a connection between Helsinki-Vantaa Airport and the Helsinki region commuter traffic network by joining the existing Vantaankoski and Main line branches. The approximately 18-kilometer-long Ring Rail line connects to the current rail network at the Vantaankoski and Hiekkaharju stations and the track between Viinikkala and Ruskeasanta goes in an underground tunnel.

For the 2015 opening, altogether five new stations were constructed at Leinelä, Helsinki-Vantaa Airport, Aviapolis, Kivistö and Vehkala. Reservations have also been made for four additional stations at Petas, Viinikkala, Ruskeasanta and Lapinkylä to be built later in the second phase. Out of these, the Aviapolis and Airport stations are located underground. Similarly, the reserved stations of Ruskeasanta and Viinikkala will be located underground.

The Ring Rail line improves the accessibility of the airport area and the suburbs along the route, cut down the journey times for over 12 million airport passengers per annum and it is also estimated to create employment for over 60 000 people.

![enter image description here](https://vayla.fi/documents/25230764/35593193/Keh%C3%A4rata_kartta.jpg/a9017019-18d8-4a4d-a601-88b08a32fe87?t=1451313857883)
*Legend in English: Pintarata = Overground, Tunneli = tunnel, Asema = station, Asemavaraus = station reservation, Nykyiset asemat = Current stations, Hämeenlinnanväylän parannus = improvement of Hämeenlinnanväylä*

## OBJECTIVES
This exercise consists of three main objectives:
- Gather and prepare data of the ring rail line for processing
- Use the gathered ring rail line data and provided data to answer questions about the impact of the ring rail line and the airport on the surrounding residents
- Find an optimal location for a new Airport Hotel & Congress Center to the Helsinki-Vantaa Airport area based on accessibility

To complete these you will put the following main skills to use:
- Data gathering and processing
- Buffer analysis
- Overlay analysis

## DATA USED
- Capital region people explanation 

## Completion

Work in pairs or individually. Complete the exercise and submit a short report containing at least the following:

1. Maps of the outcome of the exercise

	- Remember: all maps should have a legend, a scale bar and a north arrow

	- Use the tips from the Crash Course to improve your map

2. A short reflection (200-300 words) on this exercise and your map

## EXERCISE PHASES

### Part 1: The ring rail line visualization
#### 1.1: Getting the data
1. Download 4_Exercise_data from the [Github repository](https://github.com/rowan8k/fundamentals-of-gis/tree/master/Data), save it in a folder for this exercise, and add it to your QGIS project. 
	- Go through the data, what does it describe? What order of layers would be good to work with?#### 1.1: Getting the data
1. Go to Moodle and download the data necessary for the task.

32. We need to have the Ring Rail Line in geospatial format. One option is to digitize it based on a basic map. Other is to find the data online – let’s do that for practice!
	- HRI offers easy access to open data sources between the cities of Helsinki, Espoo, Vantaa and Kauniainen. Follow the link to Helsinki-Region Transport’s public transport lines from 2021-2022 and open the preview in HSL’s website. https://public-transport-hslhrt.opendata.arcgis.comhri.fi/data/en_GB/datasets/hsl-n-linjat-4/

- Picture 

	- As you can see, the dataset is big and we don’t need everything it contains. You could download the whole data and edit it on your computer, but you can also filter the data before downloading it. You’d have to figure out what different attributes mean – in this case the information is in Finnish, so needed code explanations are provided here. You can also check them also through the link below and clicking “Aineiston kuvaus (pdf)”.
		- https://public-transport-hslhrt.opendata.arcgis.com/datasets/HSLHRT::hsln-linjat-4/about
	- You can select features by clicking “Filter data” on the left of the page.
		- JL_LAJI: 12, fright.
		- Filters by local VR traffic
		- VERKKO: 4, filters on train traffic
		- AIK_VOIM: 1, filters on in-use tracks
		- SUUNTA: 1, filter on 1 direction
		- You will notice when you filter on these that the visual output barely changes, we are filtering to get as little duplicate lines as possible so we have to do as little manual adjustments ourselves. For this purpose we are only looking to extract the rough location of the line, and thus for example a single direction is sufficient. 
	- When the selection is done, you can download it by going to the Download tab under the Filter data tabcolumn jl_laji (has information on public transport type (bus, tram, …)
		- Select column value 12 from jl_laji, 12 = VR local trains
	- When the selection is done, you can download it. Click the “toggle filters” to choose only the selected features, and download .

- Picture 

3. If you’d rather data as a Shapefile. 

 ![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/4_Exercise/4_Exercise_data_selection.png)

3. Add the data you downloaded to your QGIS project and inspect the features, what do you notice? 
	- There are still duplicate entries for the Ring Rail Line and there are other entries we do not need and are in the way
	- We want to end up with only the Ring Rail Line, go through the attribute table and find which entry describes the full ring Rail Line, export (Exercise 3, step 4) this to a new layer, you can remove the original. igitize, use the Topographic map raster 1: 100 000 available from PaITuli and the plan overview images from the project area as your support. The precise route can be found on page 5 in the Ring Rail Line Brochure PDF (see Moodle). Remember to draw the underground and overground parts (the dash line in the brochure map shows the underground part) as separate segments - this is essential for the visualization stage!).

#### 1.2: Making a map visualization of the new ring rail line
4. For visualization purposes we want to have underground part of the rail as a separate segment. You can do this by splitting the ring rail line feature you exported into multiple features. 
	- We can use Google Satellite imagery (Hint: Crash Course) and the overview map of the ring rail line to find the places where we need to split the ring rail line
		- You might want to change the symbology of your ring rail line to make it more visible for editing
	- Select your Ring Rail Line layer, toggle on editing, and navigate to Edit > Edit Geometry > Split features
		- How to Split and Merge Line in QGIS: https://www.youtube.com/watch?v=vLL4hdDO1zU
	- Split the line into sections for overground and underground track
		- Create a field which describes whether the track is over- or underground so we can use symbology to differentiate these (Attribute table > New Field)
	- Don't forget to save your edits and toggle off editing

5. Now look at the ring_rail_line_stations and railway_stations layers, for the visualization we would only like to have the stations that are part of the ring rail line, and have them seperated by pre-existing, new, and planned stations. 
	- Let's start by removing the stations that are not part of the ring rail line, toggle on editing for the railway_stations layer, select the stations we want to remove, and use *Delete Selected* in the editing toolbar (Hint: Exercise 2, step 10) (Don't forget to save edits and toggle off editing).
	- Now take a look at the attribute table of the ring_rail_line_stations layer, as you can see there is already a field for which stations are new and planned, so we can use symbology to differentiate these. 
	- Optionally: Convert the train stations from polygons to points: https://docs.qgis.org/3.16/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html#centroids
		- In thi scase, points scale better, are easier to edit, and easier to add labels to

6. Make a visualization to show the ring rail line. Show on your map: where the railway is underground, which stations are new and whatever else you find convenient. 
	- Use categorized symobology to show the different types of railway and stations
	- Don't forget to add a basemap for reference (hint: Use one that contrasts with the data)
	- Optionally you can add labels to the stations either by digitizing or editing one of the ring rail line features (there’s multiple features with same information). The dataset still contains some extra features, you can keep them for visualization or delete them, as you wish. You can see the route in the Ring Rail Line Brochure PDF (see Moodle).

5. Make a visualization to show the ring rail line. Show on your map: where the railway is underground, which stations are new and whatever else you find convenient. You can use data you have from previous exercises (e.g. sea -layer).

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
	- Run *Basic Statistics for Fields* to get the total amount of residents living within the buffer (Input layer: Capital_region_people, selected feature only, Field to calculate: ASYHT(Persons in total in the building))
		- Look the output log for the SUM output, this shows the total amount
	- Repeat the same steps for the other buffer500 meters and 1 kilometer from
	- ...the stations opened in 2015?
	- ...the new and planned stations combined?

The Ring Rail Line is likely to increase the attraction for the real estate in the nearby area. This, however, will also raise the question of the noise levels caused by the Aircraft traffic around the Helsinki-Vantaa Airport. Thanks to new improved technology the aircraft noise levels have slightly dropped in recent years.

6. Find out how many people approximately live inside the dB zones: 65 or more and 50 or more in Helsinki region based on :
	- ...the noise levels in 2006? And 
	- ...the noise levels in 2010?
	- This time you don't need to create a buffer, as the dB zones already exist
	- Repeat the same steps as in step 5 to get the number of residents living within the 65 and 50 dB zones in 2006 and 2010
		- Hint: Look at the attribute tables of the noise layers (use *Selected features only* in *Select by location*)

Fill in the answers to the Moodle

*Tip : For the Capital_region_people layer field name metadata, see Appendix in Exercise 4 instructions*

#### 2.2: Planning a new airport hotel & congress center near the ring rail line
7. You work in a team that is supposed to find an optimal location for a new Airport Hotel & Congress Center to the Helsinki-Vantaa Airport area based on accessibility. Your task is to follow the given requirements and make a map visualization of the area(s) to be shown at the company meeting of where the new Hotel & Congress center could possibly be located.

| **The requirements are as follows** |
|--|
|:
- The Hotel & Congress Center has to be located within the maximum **distance of 2 kilometers from the Airport area** (but not inside it) |
|.
- The Hotel & Congress Center has to be easily accessible, thus located **within the radius of 1 kilometer from the new Ring Rail Line stations** (including the reserved ones) |
|
- It has to be **within the radius of 500 meters from the road network**. |
|
- The Hotel & Congress Center has to be **outside the ≥ 55 dB noise zones** caused by the airport traffic. |
|
- The Hotel & Congress Center **cannot be built on already built up areas**. |
|
- The Hotel & Congress Center requires **at least 5000 m2 of free building space**. |

- Start by creating buffers around the airport area, ring rail line staitons, and road network, setting the distance based on the requirements
	- You can disolve the result of the buffer to make future steps easier, 
- Use the *Intersection*  tool to combine intersect these buffers to get the areas which are only within 2km of the airport area, within a 1km radius from the stations, and within 500m from the road network. 
	- You have to run this intersect with two buffers first, then run the output of that with the final buffer to get the desired result

*Hint 1: The Multipart to Singlepart- geoprocessing tool can be used to detach the polygons individual features to be able to calculate their areas. This is useful when the overlay operations combine the features, but because their topology information is still stored, they can be separated using this tool.*

*Hint 2: When creating a buffer for the roads, don't forget to make your outputs permanent in between processing
- No we need to remove the areas that are not suitable from this layer, namely the airport area itself, the stations themselves, the roads themselves, the 55 dB noise zone, and the build up areas. 
	- We can do this using the *Difference* tool, read its description, what does it do?
	- In short, it ouputs the parts of the input layer that fall outside the overlay layer. 
	- So we need to run this for all our areas that we do not want, similar to last time we run *Difference* and then run it again with its output and the next criteria
		- Use *Selected features only* again where necessary
- Once we have the final suitable areas we need to determine which have at least 5000m2 of free building space
	- Look atly include ones near the airport area. A buffer or “Select by location” -tool’s buffering parameter can be helpful. Creating a buffer for all of the roads is unnecessary and takes a lot of time to process.*

8. Try to make the map as clear and informative as possible and insert the finished map with all the necessary map elements to your courrent layer and its features, could we select the areas which have at least 5000m2 free space right now? Why not? 
	- Some features that are not phyiscally connected are still 1 feature, so we need to seperate them. 
		- Do this by running the *Promote to Multipart* tool on your current layer, this will seperate the features into seperate parts
	- Let's extract areas of at least 5000m2 using the *Extract by Expression* tool (Hint: Crash Course, step 7)
- Done! You should now have the areas that meet all the criteria

8. Make your final map of the suitable areas for the new airport hotel & congress center

se report. Write also a short reflection on what was done and why.

## Appendix: Overview map of the ring rail line

- Add picture

Legend in English: Pintarata = Overground, Tunneli = tunnel, Asema = station, Asemavaraus = station reservation, Nykyiset asemat = Current stations, Hämeenlinnanväylän parannus = improvement of Hämeenlinnanväylä



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJFdFByYk5zWUdNWWhPWXRSIjp7In
RleHQiOiJNb29kbGUiLCJzdGFydCI6MzE4NiwiZW5kIjozMTky
fSwicjFuaW14MW1CdWx6YVhkViI6eyJ0ZXh0IjoiLSBQaWN0dX
JlIiwic3RhcnQiOjM3NDMsImVuZCI6Mzc1Mn0sIkNVTHg0QmVW
RFZzMm5GSUEiOnsidGV4dCI6Ii0gUGljdHVyZSIsInN0YXJ0Ij
o1MjUzLCJlbmQiOjUyNjJ9LCJHMTlOS0JJTGloREF2ME5FIjp7
InRleHQiOiI0LiBGb3IgdmlzdWFsaXphdGlvbiBwdXJwb3Nlcy
B3ZSB3YW50IHRvIGhhdmUgdW5kZXJncm91bmQgcGFydCBvZiB0
aGUgcmFpbCBhcyBh4oCmIiwic3RhcnQiOjYzNTMsImVuZCI6OD
k4MX0sIkw0MmtOUERvR0NjcEZTdGsiOnsidGV4dCI6IjUuIE1h
a2UgYSB2aXN1YWxpemF0aW9uIHRvIHNob3cgdGhlIHJpbmcgcm
FpbCBsaW5lLiBTaG93IG9uIHlvdXIgbWFwOiB3aGVyZSB0aGXi
gKYiLCJzdGFydCI6ODk4MywiZW5kIjo5MjE3fSwiVlZoRndjYT
RQcVlPRXREQiI6eyJ0ZXh0IjoiMi4xOiBBbmFseXppbmcgdGhl
IGVmZmVjdHMgb24gdGhlIHBlb3BsZSBpbiB0aGUgc3R1ZHkgYX
JlYSIsInN0YXJ0Ijo5MjY5LCJlbmQiOjkzMjd9LCJYQTNndVBG
R2FJb245b0dKIjp7InRleHQiOiI1LiBGaW5kIG91dCBob3cgbW
FueSBhcmUgbm90YWJseSBhZmZlY3RlZCBieSB0aGlzIGJ5IGNh
bGN1bGF0aW5nIGhvdyBtYW55IHBlb3Bs4oCmIiwic3RhcnQiOj
k0OTgsImVuZCI6MTA2NzJ9LCJteEl5dndvUlBMZkRZWVUzIjp7
InRleHQiOiI2LiBGaW5kIG91dCBob3cgbWFueSBwZW9wbGUgYX
Bwcm94aW1hdGVseSBsaXZlIGluc2lkZSB0aGUgZEIgem9uZXM6
IDY1IG9yIG1vcmXigKYiLCJzdGFydCI6MTEwODEsImVuZCI6MT
EyMDR9LCJueVhqS0t5czBwRlBDVW5uIjp7InRleHQiOiItIEFk
ZCBwaWN0dXJlIiwic3RhcnQiOjE1Njc3LCJlbmQiOjE1NjkwfS
wicmptTVdrTElhMEZZNWpBVCI6eyJ0ZXh0IjoiKipUaGUgcmVx
dWlyZW1lbnRzIGFyZSBhcyBmb2xsb3dzKio6XG4tIFRoZSBIb3
RlbCAmIENvbmdyZXNzIENlbnRlciBoYXMgdG8gYmUgbG/igKYi
LCJzdGFydCI6MTIxNzcsImVuZCI6MTM0NjJ9LCJEeFk5dXNQNU
sxYWdsWTU5Ijp7InRleHQiOiJGaWxsIGluIHRoZSBhbnN3ZXJz
IHRvIHRoZSBNb29kbGUiLCJzdGFydCI6MTE1OTAsImVuZCI6MT
E2MjN9LCIwT3ZNN1E3V1BGRFpka0ZjIjp7InRleHQiOiIjIyMj
IDIuMjogUGxhbm5pbmcgYSBuZXcgYWlycG9ydCBob3RlbCAmIG
NvbmdyZXNzIGNlbnRlciBuZWFyIHRoZSByaW5nIHJhaWwgbGlu
ZSIsInN0YXJ0IjoxMTczMSwiZW5kIjoxMTgxMX0sIlliQ3ZSNG
RMTjBmb0ZZTW0iOnsidGV4dCI6IiMjIERBVEEgVVNFRCIsInN0
YXJ0IjoyMzQzLCJlbmQiOjIzNTV9LCIyeE9YWWt4WFpIYTZkM0
1UIjp7InRleHQiOiIjIEV4ZXJjaXNlIDQ6Iiwic3RhcnQiOjU4
LCJlbmQiOjcxfSwiNXdRUUk3ZDlEU2tZOWpnRyI6eyJzdGFydC
I6MzE1MiwiZW5kIjozMTUzLCJ0ZXh0IjoiIyJ9fSwiY29tbWVu
dHMiOnsiSHUxb2w3R2lGNmhCdDNjSSI6eyJkaXNjdXNzaW9uSW
QiOiJFdFByYk5zWUdNWWhPWXRSIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiQ29ycmVjdCIsImNyZWF0ZWQiOjE2ODY4OT
g0MDY4MTJ9LCJJdUc3aE5hT2k0UklhZktlIjp7ImRpc2N1c3Np
b25JZCI6InIxbmlteDFtQnVsemFYZFYiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQi
OjE2ODY4OTg3NTU5NDB9LCJXSE9hbEd4NWh5dkVKOENFIjp7Im
Rpc2N1c3Npb25JZCI6IkNVTHg0QmVWRFZzMm5GSUEiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsIm
NyZWF0ZWQiOjE2ODY4OTg3ODc4MDV9LCJ0ZXowbTJhdDN6WExm
WHJjIjp7ImRpc2N1c3Npb25JZCI6IkcxOU5LQklMaWhEQXYwTk
UiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXcml0ZSB0
aGlzIG91dCB3aXRoIG1vcmUgaW5zdHJ1Y3Rpb25zLCBlLmcuIH
JlbWluZCBob3cgdG8gZGlnaXRpemUsIGhvdyB0byBlZGl0IGV4
aXN0aW5nIGZlYXR1cmVzLCBldGMiLCJjcmVhdGVkIjoxNjg2OD
k4OTI1MzE3fSwiRU5aY0pwNHRGdlhxenliRiI6eyJkaXNjdXNz
aW9uSWQiOiJHMTlOS0JJTGloREF2ME5FIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiVGVzdCB0aGlzIHNlY3Rpb24gd2hl
biB3cml0aW5nIHNpbmNlIGl0IHdhcyB0cmlja3kgd2hlbiBJIG
RpZCBpdCIsImNyZWF0ZWQiOjE2ODY4OTg5NDAwOTN9LCJpczg0
Z09jRnprRHd0TXlWIjp7ImRpc2N1c3Npb25JZCI6Ikw0MmtOUE
RvR0NjcEZTdGsiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJHaXZlIHNvbWUgbW9yZSBoaW50cyBvbiBob3cgdG8gZG8gdG
hpcyIsImNyZWF0ZWQiOjE2ODY4OTkwMDkwMTN9LCJHVU1tQ1RK
aEt4azRQU2lOIjp7ImRpc2N1c3Npb25JZCI6IlZWaEZ3Y2E0UH
FZT0V0REIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQgc2VjdGlvbiBpbiBtb29kbGUgd2hlcmUgdG8gZmlsbCBpbi
BhbnN3ZXJzIGZvciB0aGVzZSIsImNyZWF0ZWQiOjE2ODY4OTky
NDQ5OTd9LCJabTZZNlZBRDc1RnVjTXZYIjp7ImRpc2N1c3Npb2
5JZCI6IlhBM2d1UEZHYUlvbjlvR0oiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJXcml0ZSBvdXQgaG93IHRvIGRvIHRoaX
M6IHRoZWlyIGZpcnN0IHRpbWUgZG9pbmcgYnVmZmVyIGFuYWx5
c2lzIiwiY3JlYXRlZCI6MTY4Njg5OTI3ODYyOX0sIjZpbDdpU2
VCSTNOVE1Cb3EiOnsiZGlzY3Vzc2lvbklkIjoibXhJeXZ3b1JQ
TGZEWVlVMyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Il
dyaXRlIG91dCBob3cgdG8gZG8gdGhpczogdGhlaXIgZmlycyB0
dGltZSBkb2luZyBidWZmZXIgYW5hbHlzaXMiLCJjcmVhdGVkIj
oxNjg2ODk5Mjk3NzMzfSwiVUJaaWtKTGExWmp5ZWpobSI6eyJk
aXNjdXNzaW9uSWQiOiJueVhqS0t5czBwRlBDVW5uIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJj
cmVhdGVkIjoxNjg2ODk5NTkzMDA1fSwiZnJ0MUZ3YVBHQnV1TU
hnSSI6eyJkaXNjdXNzaW9uSWQiOiJyam1NV2tMSWEwRlk1akFU
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiRnVsbHkgZX
hwbGFpbiBob3cgdGhleSBkbyB0aGlzIiwiY3JlYXRlZCI6MTY4
Njg5OTYwNTAwNX0sImRLQmNIMWdHZ3IybEF3N3MiOnsiZGlzY3
Vzc2lvbklkIjoiRHhZOXVzUDVLMWFnbFk1OSIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkZpeCByZWZlcmVuY2UiLCJjcm
VhdGVkIjoxNjg2OTg2NDI5MTA1fSwiNjZTcHRKd0pHOE90VnBr
YiI6eyJkaXNjdXNzaW9uSWQiOiIwT3ZNN1E3V1BGRFpka0ZjIi
wic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiT3B0aW9uYWxs
eSAocmUpbW92ZSB0aGlzIGlmIHRvbyBoYXJkIiwiY3JlYXRlZC
I6MTY4Njk4ODc0NzM2OX0sIjViRm9DWlpKUkRPRGh6RFkiOnsi
ZGlzY3Vzc2lvbklkIjoiWWJDdlI0ZExOMGZvRllNbSIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IldoYXQgYXJlIHRoZSBk
YXRhIHNvdXJjZXM/IiwiY3JlYXRlZCI6MTY4NzE1ODA1ODcxM3
0sIlRoVmxKb09HZGVmVW40TkQiOnsiZGlzY3Vzc2lvbklkIjoi
MnhPWFlreFhaSGE2ZDNNVCIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCB0aXRsZSIsImNyZWF0ZWQiOjE2ODcxNzA0
Mjg0MDZ9LCJxOTlvdnhzcWZaeXpHVXJDIjp7ImRpc2N1c3Npb2
5JZCI6IjV3UVFJN2Q5RFNrWTlqZ0ciLCJzdWIiOiJnaDoyMjE2
ODE1NyIsInRleHQiOiI/IiwiY3JlYXRlZCI6MTY4NzI1NDM0ND
MxM319LCJoaXN0b3J5IjpbLTE1MTI3MDY4MiwxMDQ4MzgwNDAx
LC0xODEzNjEyODQxLDMyMDc1NzI4OSwxMzE5NTA0MjM1LDEyMz
gxODQ5ODYsMTQyOTQ1MTQzOCwxMjEyNTk1ODM2LC0xMzI3NzM1
MTUyLC0yNzYwNzIxMTUsLTMwMjQ2NTIxMiwtMTkyOTUyNjA2MS
wyMTAxOTQzODUyLDcyNDYxNzkwLC0yMDczMzkzMTAzLDIwMzM4
NDUwNzQsLTUwOTgwNjY5MSwtNDQ5MTE1NjAzLC0yNzk5MzcwOD
ksMjAxMTk5NjcxMF19
-->