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

| **The requirements are as follows** |
|--|
| The Hotel & Congress Center has to be located within the maximum **distance of 2 kilometers from the Airport area** (but not inside it) |
| The Hotel & Congress Center has to be easily accessible, thus located **within the radius of 1 kilometer from the new Ring Rail Line stations** (including the reserved ones) |
| It has to be **within the radius of 500 meters from the road network**. |
| The Hotel & Congress Center has to be **outside the ≥ 55 dB noise zones** caused by the airport traffic. |
| The Hotel & Congress Center **cannot be built on already built up areas**. |
| The Hotel & Congress Center requires **at least 5000 m2 of free building space**. |

- Start by creating buffers around the airport area, ring rail line staitons, and road network, setting the distance based on the requirements
	- You can disolve the result of the buffer to make future steps easier, 
- Use the *Intersection*  tool to combine intersect these buffers to get the areas which are only within 2km of the airport area, within a 1km radius from the stations, and within 500m from the road network. 
	- You have to run this intersect with two buffers first, then run the output of that with the final buffer to get the desired result, don't forget to make your outputs permanent in between processing
- No we need to remove the areas that are not suitable from this layer, namely the airport area itself, the stations themselves, the roads themselves, the 55 dB noise zone, and the build up areas. 
	- We can do this using the *Difference* tool, read its description, what does it do?
	- In short, it ouputs the parts of the input layer that fall outside the overlay layer. 
	- So we need to run this for all our areas that we do not want, similar to last time we run *Difference* and then run it again with its output and the next criteria
		- Use *Selected features only* again where necessary
- Once we have the final suitable areas we need to determine which have at least 5000m2 of free building space
	- Look at your current layer and its features, could we select the areas which have at least 5000m2 free space right now? Why not? 
	- Some features that are not phyiscally connected are still 1 feature, so we need to seperate them. 
		- Do this by running the *Promote to Multipart* tool on your current layer, this will seperate the features into seperate parts
	- Let's extract areas of at least 5000m2 using the *Extract by Expression* tool
- Done! You should now have the areas that meet all the criteria

8. Make your final map of the suitable areas for the new airport hotel & congress center

## Appendix: Overview map of the ring rail line

- Add picture

Legend in English: Pintarata = Overground, Tunneli = tunnel, Asema = station, Asemavaraus = station reservation, Nykyiset asemat = Current stations, Hämeenlinnanväylän parannus = improvement of Hämeenlinnanväylä



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJFdFByYk5zWUdNWWhPWXRSIjp7In
N0YXJ0IjoxNDUyLCJlbmQiOjE0NTgsInRleHQiOiJNb29kbGUi
fSwicjFuaW14MW1CdWx6YVhkViI6eyJzdGFydCI6MjE1NiwiZW
5kIjoyMTY1LCJ0ZXh0IjoiLSBQaWN0dXJlIn0sIkNVTHg0QmVW
RFZzMm5GSUEiOnsic3RhcnQiOjM1MjYsImVuZCI6MzUzNSwidG
V4dCI6Ii0gUGljdHVyZSJ9LCJWVmhGd2NhNFBxWU9FdERCIjp7
InN0YXJ0Ijo2MzMzLCJlbmQiOjYzOTEsInRleHQiOiIyLjE6IE
FuYWx5emluZyB0aGUgZWZmZWN0cyBvbiB0aGUgcGVvcGxlIGlu
IHRoZSBzdHVkeSBhcmVhIn0sIm55WGpLS3lzMHBGUENVbm4iOn
sic3RhcnQiOjExNzgwLCJlbmQiOjExNzkzLCJ0ZXh0IjoiLSBB
ZGQgcGljdHVyZSJ9LCJOMUgwZEV4Z1NBbUN2WjJYIjp7InN0YX
J0IjozODk3LCJlbmQiOjM5MDMsInRleHQiOiJleHBvcnQifSwi
VHhWS0xwNzk4ZGtqNXBPcSI6eyJzdGFydCI6NTM3NiwiZW5kIj
o1MzkxLCJ0ZXh0IjoiZWRpdGluZyB0b29sYmFyIn0sIm5KYkRR
ekNlbkp2aEtydUEiOnsic3RhcnQiOjQyMTIsImVuZCI6NDM1My
widGV4dCI6Ii0gV2UgY2FuIHVzZSBHb29nbGUgU2F0ZWxsaXRl
IGltYWdlcnkgYW5kIHRoZSBvdmVydmlldyBtYXAgb2YgdGhlIH
JpbmcgcmFpbCBsaW7igKYifSwieXlLWHJZUHpxTDFrTDhtQyI6
eyJzdGFydCI6NzU1MywiZW5kIjo3NTU0LCJ0ZXh0IjoiWCJ9LC
JEeFk5dXNQNUsxYWdsWTU5Ijp7InN0YXJ0Ijo4NDk3LCJlbmQi
Ojg1MzAsInRleHQiOiJGaWxsIGluIHRoZSBhbnN3ZXJzIHRvIH
RoZSBNb29kbGUifSwiME92TTdRN1dQRkRaZGtGYyI6eyJzdGFy
dCI6ODYzOCwiZW5kIjo4NzE4LCJ0ZXh0IjoiIyMjIyAyLjI6IF
BsYW5uaW5nIGEgbmV3IGFpcnBvcnQgaG90ZWwgJiBjb25ncmVz
cyBjZW50ZXIgbmVhciB0aGUgcmluZyByYWlsIGxpbmUifSwiNV
kwT3E5VHRTZVhYVmhyZSI6eyJzdGFydCI6MTEyNjMsImVuZCI6
MTE1NzQsInRleHQiOiItIExldCdzIGV4dHJhY3QgYXJlYXMgb2
YgYXQgbGVhc3QgNTAwMG0yIHVzaW5nIHRoZSAqRXh0cmFjdCBi
eSBFeHByZXNzaW9uKiB0b29sIn19LCJjb21tZW50cyI6eyJIdT
FvbDdHaUY2aEJ0M2NJIjp7ImRpc2N1c3Npb25JZCI6IkV0UHJi
TnNZR01ZaE9ZdFIiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDb3JyZWN0IiwiY3JlYXRlZCI6MTY4Njg5ODQwNjgxMn0s
Ikl1RzdoTmFPaTRSSWFmS2UiOnsiZGlzY3Vzc2lvbklkIjoicj
FuaW14MW1CdWx6YVhkViIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Njg5OD
c1NTk0MH0sIldIT2FsR3g1aHl2RUo4Q0UiOnsiZGlzY3Vzc2lv
bklkIjoiQ1VMeDRCZVZEVnMybkZJQSIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6
MTY4Njg5ODc4NzgwNX0sIkdVTW1DVEpoS3hrNFBTaU4iOnsiZG
lzY3Vzc2lvbklkIjoiVlZoRndjYTRQcVlPRXREQiIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBzZWN0aW9uIGluIG
1vb2RsZSB3aGVyZSB0byBmaWxsIGluIGFuc3dlcnMgZm9yIHRo
ZXNlIiwiY3JlYXRlZCI6MTY4Njg5OTI0NDk5N30sIlVCWmlrSk
xhMVpqeWVqaG0iOnsiZGlzY3Vzc2lvbklkIjoibnlYaktLeXMw
cEZQQ1VubiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4Njg5OTU5MzAwNX0s
IjJFY09JUkZGTGE1WGk5Um0iOnsiZGlzY3Vzc2lvbklkIjoiTj
FIMGRFeGdTQW1DdloyWCIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkFkZCBoaW50IiwiY3JlYXRlZCI6MTY4Njk4MzAxOT
I5MH0sIlN5V3lCTUpVWGNQcXVnbGsiOnsiZGlzY3Vzc2lvbklk
IjoiVHhWS0xwNzk4ZGtqNXBPcSIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4
Njk4Mzc5OTU2M30sIkp1Tk5FYm03SG9CSjU2MkUiOnsiZGlzY3
Vzc2lvbklkIjoibkpiRFF6Q2VuSnZoS3J1QSIsInN1YiI6Imdo
OjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBoaW50IiwiY3JlYXRlZC
I6MTY4Njk4NDU4OTU4MH0sIjBZMGNKUVM3ZExDM0ZzUFgiOnsi
ZGlzY3Vzc2lvbklkIjoieXlLWHJZUHpxTDFrTDhtQyIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBtZWFuaW5nIiwi
Y3JlYXRlZCI6MTY4Njk4NjM1ODMzMH0sImRLQmNIMWdHZ3IybE
F3N3MiOnsiZGlzY3Vzc2lvbklkIjoiRHhZOXVzUDVLMWFnbFk1
OSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkZpeCByZW
ZlcmVuY2UiLCJjcmVhdGVkIjoxNjg2OTg2NDI5MTA1fSwiNjZT
cHRKd0pHOE90VnBrYiI6eyJkaXNjdXNzaW9uSWQiOiIwT3ZNN1
E3V1BGRFpka0ZjIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiT3B0aW9uYWxseSAocmUpbW92ZSB0aGlzIGlmIHRvbyBoYX
JkIiwiY3JlYXRlZCI6MTY4Njk4ODc0NzM2OX0sIjloNjM1Szk1
OWlEZE1IQmwiOnsiZGlzY3Vzc2lvbklkIjoiNVkwT3E5VHRTZV
hYVmhyZSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFk
ZCBoaW50IG9uIHdoZXJlIHRvIGZpbmQgZXhwcmVzc2lvbiBmb3
IgdGhpcyIsImNyZWF0ZWQiOjE2ODY5ODg5MjgxMDR9fSwiaGlz
dG9yeSI6Wy0zMDI0NjUyMTIsLTE5Mjk1MjYwNjEsMjEwMTk0Mz
g1Miw3MjQ2MTc5MCwtMjA3MzM5MzEwMywyMDMzODQ1MDc0LC01
MDk4MDY2OTEsLTQ0OTExNTYwMywtMjc5OTM3MDg5LDIwMTE5OT
Y3MTAsMTcwMDIzMzgxOSw1MTE5OTk5MjIsMTg3MjEwNjYxNiwt
NTQ4NjYyNDAsMjAzODI0NjAxOCwtMjkzNjk0NzkxLC0xMzgwMT
UxMjg4LDczMDk5ODExNl19
-->