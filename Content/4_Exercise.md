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
		- Create a field which describes whether the track is over- or underground so we can use symbology to differentiate these
	- Don't forget to save your edits and toggle off editing

5. Now look at the ring_rail_line_stations and railway_stations layers, for the visualization we would only like to have the stations that are part of the ring rail line, and have them seperated by pre-existing, new, and planned stations. 
	- Let's start by removing the stations that are not part of the ring rail line, toggle on editing for the railway_stations layer, select the stations we want to remove, and use *Delete Selected* in the editing toolbar (save edits and toggle off editing).
	- Now take a look at the attribute table of the ring_rail_line_stations layer, as you can see there is already a field for which stations are new and planned, so we can use symbology to differentiate these. 

7. Make a visualization to show the ring rail line. Show on your map: where the railway is underground, which stations are new and whatever else you find convenient. You can use data you have from previous exercises (e.g. sea -layer).

---

### Part 2: The ring rail line analysis
#### 2.1: Analyzing the effects on the people in the study area
As already mentioned, the Ring Rail line improves the commuter traffic network and accessibility of the suburbs along the track, but how does this show on real numbers?

5. Find out how many are notably affected by this by calculating how many people live within a radius of 500 meters and 1 kilometer from
	- ...the stations opened in 2015?
	- ...the new and planned stations combined?

The Ring Rail Line is likely to increase the attraction for the real estate in the nearby area. This, however, will also raise the question of the noise levels caused by the Aircraft traffic around the Helsinki-Vantaa Airport. Thanks to new improved technology the aircraft noise levels have slightly dropped in recent years.

6. Find out how many people approximately live inside the dB zones: 65 or more and 50 or more in Helsinki region based on:
	- ...the noise levels in 2006?
	- ...the noise levels in 2010?

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
V4dCI6Ii0gUGljdHVyZSJ9LCJHMTlOS0JJTGloREF2ME5FIjp7
InN0YXJ0Ijo0MDE5LCJlbmQiOjQ5MDIsInRleHQiOiI0LiBGb3
IgdmlzdWFsaXphdGlvbiBwdXJwb3NlcyB3ZSB3YW50IHRvIGhh
dmUgdW5kZXJncm91bmQgcGFydCBvZiB0aGUgcmFpbCBhcyBh4o
CmIn0sIkw0MmtOUERvR0NjcEZTdGsiOnsic3RhcnQiOjU2MTAs
ImVuZCI6NTg0MywidGV4dCI6IjUuIE1ha2UgYSB2aXN1YWxpem
F0aW9uIHRvIHNob3cgdGhlIHJpbmcgcmFpbCBsaW5lLiBTaG93
IG9uIHlvdXIgbWFwOiB3aGVyZSB0aGXigKYifSwiVlZoRndjYT
RQcVlPRXREQiI6eyJzdGFydCI6NTg5NSwiZW5kIjo1OTUzLCJ0
ZXh0IjoiMi4xOiBBbmFseXppbmcgdGhlIGVmZmVjdHMgb24gdG
hlIHBlb3BsZSBpbiB0aGUgc3R1ZHkgYXJlYSJ9LCJYQTNndVBG
R2FJb245b0dKIjp7InN0YXJ0Ijo2MTI0LCJlbmQiOjYyNjAsIn
RleHQiOiI1LiBGaW5kIG91dCBob3cgbWFueSBhcmUgbm90YWJs
eSBhZmZlY3RlZCBieSB0aGlzIGJ5IGNhbGN1bGF0aW5nIGhvdy
BtYW55IHBlb3Bs4oCmIn0sIm14SXl2d29SUExmRFlZVTMiOnsi
c3RhcnQiOjY2NjksImVuZCI6Njc5MSwidGV4dCI6IjYuIEZpbm
Qgb3V0IGhvdyBtYW55IHBlb3BsZSBhcHByb3hpbWF0ZWx5IGxp
dmUgaW5zaWRlIHRoZSBkQiB6b25lczogNjUgb3IgbW9yZeKApi
J9LCJueVhqS0t5czBwRlBDVW5uIjp7InN0YXJ0Ijo4OTIyLCJl
bmQiOjg5MzUsInRleHQiOiItIEFkZCBwaWN0dXJlIn0sInJqbU
1Xa0xJYTBGWTVqQVQiOnsic3RhcnQiOjc0MDcsImVuZCI6ODEw
MCwidGV4dCI6IioqVGhlIHJlcXVpcmVtZW50cyBhcmUgYXMgZm
9sbG93cyoqOlxuLSBUaGUgSG90ZWwgJiBDb25ncmVzcyBDZW50
ZXIgaGFzIHRvIGJlIGxv4oCmIn0sIk4xSDBkRXhnU0FtQ3ZaMl
giOnsic3RhcnQiOjM4OTcsImVuZCI6MzkwMywidGV4dCI6ImV4
cG9ydCJ9LCJUeFZLTHA3OThka2o1cE9xIjp7InN0YXJ0Ijo1Mz
Q2LCJlbmQiOjUzNjEsInRleHQiOiJlZGl0aW5nIHRvb2xiYXIi
fX0sImNvbW1lbnRzIjp7Ikh1MW9sN0dpRjZoQnQzY0kiOnsiZG
lzY3Vzc2lvbklkIjoiRXRQcmJOc1lHTVloT1l0UiIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkNvcnJlY3QiLCJjcmVhdG
VkIjoxNjg2ODk4NDA2ODEyfSwiSXVHN2hOYU9pNFJJYWZLZSI6
eyJkaXNjdXNzaW9uSWQiOiJyMW5pbXgxbUJ1bHphWGRWIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUi
LCJjcmVhdGVkIjoxNjg2ODk4NzU1OTQwfSwiV0hPYWxHeDVoeX
ZFSjhDRSI6eyJkaXNjdXNzaW9uSWQiOiJDVUx4NEJlVkRWczJu
RklBIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIH
BpY3R1cmUiLCJjcmVhdGVkIjoxNjg2ODk4Nzg3ODA1fSwidGV6
MG0yYXQzelhMZlhyYyI6eyJkaXNjdXNzaW9uSWQiOiJHMTlOS0
JJTGloREF2ME5FIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiV3JpdGUgdGhpcyBvdXQgd2l0aCBtb3JlIGluc3RydWN0aW
9ucywgZS5nLiByZW1pbmQgaG93IHRvIGRpZ2l0aXplLCBob3cg
dG8gZWRpdCBleGlzdGluZyBmZWF0dXJlcywgZXRjIiwiY3JlYX
RlZCI6MTY4Njg5ODkyNTMxN30sIkVOWmNKcDR0RnZYcXp5YkYi
OnsiZGlzY3Vzc2lvbklkIjoiRzE5TktCSUxpaERBdjBORSIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlRlc3QgdGhpcyBz
ZWN0aW9uIHdoZW4gd3JpdGluZyBzaW5jZSBpdCB3YXMgdHJpY2
t5IHdoZW4gSSBkaWQgaXQiLCJjcmVhdGVkIjoxNjg2ODk4OTQw
MDkzfSwiaXM4NGdPY0Z6a0R3dE15ViI6eyJkaXNjdXNzaW9uSW
QiOiJMNDJrTlBEb0dDY3BGU3RrIiwic3ViIjoiZ2g6NDAzMDQ3
ODgiLCJ0ZXh0IjoiR2l2ZSBzb21lIG1vcmUgaGludHMgb24gaG
93IHRvIGRvIHRoaXMiLCJjcmVhdGVkIjoxNjg2ODk5MDA5MDEz
fSwiR1VNbUNUSmhLeGs0UFNpTiI6eyJkaXNjdXNzaW9uSWQiOi
JWVmhGd2NhNFBxWU9FdERCIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQWRkIHNlY3Rpb24gaW4gbW9vZGxlIHdoZXJlIH
RvIGZpbGwgaW4gYW5zd2VycyBmb3IgdGhlc2UiLCJjcmVhdGVk
IjoxNjg2ODk5MjQ0OTk3fSwiWm02WTZWQUQ3NUZ1Y012WCI6ey
JkaXNjdXNzaW9uSWQiOiJYQTNndVBGR2FJb245b0dKIiwic3Vi
IjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiV3JpdGUgb3V0IGhvdy
B0byBkbyB0aGlzOiB0aGVpciBmaXJzdCB0aW1lIGRvaW5nIGJ1
ZmZlciBhbmFseXNpcyIsImNyZWF0ZWQiOjE2ODY4OTkyNzg2Mj
l9LCI2aWw3aVNlQkkzTlRNQm9xIjp7ImRpc2N1c3Npb25JZCI6
Im14SXl2d29SUExmRFlZVTMiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJXcml0ZSBvdXQgaG93IHRvIGRvIHRoaXM6IHRo
ZWlyIGZpcnMgdHRpbWUgZG9pbmcgYnVmZmVyIGFuYWx5c2lzIi
wiY3JlYXRlZCI6MTY4Njg5OTI5NzczM30sIlVCWmlrSkxhMVpq
eWVqaG0iOnsiZGlzY3Vzc2lvbklkIjoibnlYaktLeXMwcEZQQ1
VubiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBw
aWN0dXJlIiwiY3JlYXRlZCI6MTY4Njg5OTU5MzAwNX0sImZydD
FGd2FQR0J1dU1IZ0kiOnsiZGlzY3Vzc2lvbklkIjoicmptTVdr
TElhMEZZNWpBVCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IkZ1bGx5IGV4cGxhaW4gaG93IHRoZXkgZG8gdGhpcyIsImNy
ZWF0ZWQiOjE2ODY4OTk2MDUwMDV9LCIyRWNPSVJGRkxhNVhpOV
JtIjp7ImRpc2N1c3Npb25JZCI6Ik4xSDBkRXhnU0FtQ3ZaMlgi
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgaGludC
IsImNyZWF0ZWQiOjE2ODY5ODMwMTkyOTB9LCJTeVd5Qk1KVVhj
UHF1Z2xrIjp7ImRpc2N1c3Npb25JZCI6IlR4VktMcDc5OGRraj
VwT3EiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
cGljdHVyZSIsImNyZWF0ZWQiOjE2ODY5ODM3OTk1NjN9fSwiaG
lzdG9yeSI6Wy0xMzIyOTIyMzQxLDIwMTE5OTY3MTAsMTcwMDIz
MzgxOSw1MTE5OTk5MjIsMTg3MjEwNjYxNiwtNTQ4NjYyNDAsMj
AzODI0NjAxOCwtMjkzNjk0NzkxLC0xMzgwMTUxMjg4LDczMDk5
ODExNl19
-->