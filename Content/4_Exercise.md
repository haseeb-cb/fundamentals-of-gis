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
1. Go to Moodle and download the data necessary for the task.

2. We need to have the Ring Rail Line in geospatial format. One option is to digitize it based on a basic map. Other is to find the data online – let’s do that for practice!
	- HRI offers easy access to open data sources between the cities of Helsinki, Espoo, Vantaa and Kauniainen. Follow the link to Helsinki-Region Transport’s public transport lines from 2021-2022 and open the preview in HSL’s website. https://hri.fi/data/en_GB/dataset/hsl-n-linjat

- Picture 

	- As you can see, the dataset is big and we don’t need everything it contains. You could download the whole data and edit it on your computer, but you can also filter the data before downloading it. You’d have to figure out what different attributes mean – unfortunately in this case the information is in Finnish, so needed code explanations are provided here. You can check them also through the link below and “Aineiston kuvaus (pdf)”.
		- https://public-transport-hslhrt.opendata.arcgis.com/datasets/HSLHRT::hsln-linjat-4/about
	- You can select features by clicking “Filter data” on right.
		- Filter by column jl_laji (has information on public transport type (bus, tram, …)
		- Select column value 12 from jl_laji, 12 = VR local trains
	- When the selection is done, you can download it. Click the “toggle filters” to choose only the selected features.

- Picture 

3. If you’d rather digitize, use the Topographic map raster 1: 100 000 available from PaITuli and the plan overview images from the project area as your support. The precise route can be found on page 5 in the Ring Rail Line Brochure PDF (see Moodle). Remember to draw the underground and overground parts (the dash line in the brochure map shows the underground part) as separate segments - this is essential for the visualization stage!).

#### 1.2: Making a map visualization of the new ring rail line
4. For visualization purposes we want to have underground part of the rail as a separate segment. You can do this either by digitizing or editing one of the ring rail line features (there’s multiple features with same information). The dataset still contains some extra features, you can keep them for visualization or delete them, as you wish. You can see the route in the Ring Rail Line Brochure PDF (see Moodle).

5. Make a visualization to show the ring rail line. Show on your map: where the railway is underground, which stations are new and whatever else you find convenient. You can use data you have from previous exercises (e.g. sea -layer).

---

### Part 2: The ring rail line analysis
#### 2.1: Analyzing the effects on the people in the study area
As already mentioned, the Ring Rail line improves the commuter traffic network and accessibility of the suburbs along the track, but how does this show on real numbers?

5. Find out how many are notably affected by this by calculating how many people live within a radius of 500 meters and 1 kilometer from
	- ...the stations opened in 2015?
	- ...the new and planned stations combined

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJFdFByYk5zWUdNWWhPWXRSIjp7In
N0YXJ0IjoxNDUyLCJlbmQiOjE0NTgsInRleHQiOiJNb29kbGUi
fSwicjFuaW14MW1CdWx6YVhkViI6eyJzdGFydCI6MTk2MSwiZW
5kIjoxOTcwLCJ0ZXh0IjoiLSBQaWN0dXJlIn0sIkNVTHg0QmVW
RFZzMm5GSUEiOnsic3RhcnQiOjI4MzUsImVuZCI6Mjg0NCwidG
V4dCI6Ii0gUGljdHVyZSJ9LCJHMTlOS0JJTGloREF2ME5FIjp7
InN0YXJ0IjozMzUyLCJlbmQiOjM3NjcsInRleHQiOiI0LiBGb3
IgdmlzdWFsaXphdGlvbiBwdXJwb3NlcyB3ZSB3YW50IHRvIGhh
dmUgdW5kZXJncm91bmQgcGFydCBvZiB0aGUgcmFpbCBhcyBh4o
CmIn0sIkw0MmtOUERvR0NjcEZTdGsiOnsic3RhcnQiOjM3Njks
ImVuZCI6NDAwMywidGV4dCI6IjUuIE1ha2UgYSB2aXN1YWxpem
F0aW9uIHRvIHNob3cgdGhlIHJpbmcgcmFpbCBsaW5lLiBTaG93
IG9uIHlvdXIgbWFwOiB3aGVyZSB0aGXigKYifX0sImNvbW1lbn
RzIjp7Ikh1MW9sN0dpRjZoQnQzY0kiOnsiZGlzY3Vzc2lvbklk
IjoiRXRQcmJOc1lHTVloT1l0UiIsInN1YiI6ImdoOjQwMzA0Nz
g4IiwidGV4dCI6IkNvcnJlY3QiLCJjcmVhdGVkIjoxNjg2ODk4
NDA2ODEyfSwiSXVHN2hOYU9pNFJJYWZLZSI6eyJkaXNjdXNzaW
9uSWQiOiJyMW5pbXgxbUJ1bHphWGRWIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIj
oxNjg2ODk4NzU1OTQwfSwiV0hPYWxHeDVoeXZFSjhDRSI6eyJk
aXNjdXNzaW9uSWQiOiJDVUx4NEJlVkRWczJuRklBIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJj
cmVhdGVkIjoxNjg2ODk4Nzg3ODA1fSwidGV6MG0yYXQzelhMZl
hyYyI6eyJkaXNjdXNzaW9uSWQiOiJHMTlOS0JJTGloREF2ME5F
Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiV3JpdGUgdG
hpcyBvdXQgd2l0aCBtb3JlIGluc3RydWN0aW9ucywgZS5nLiBy
ZW1pbmQgaG93IHRvIGRpZ2l0aXplLCBob3cgdG8gZWRpdCBleG
lzdGluZyBmZWF0dXJlcywgZXRjIiwiY3JlYXRlZCI6MTY4Njg5
ODkyNTMxN30sIkVOWmNKcDR0RnZYcXp5YkYiOnsiZGlzY3Vzc2
lvbklkIjoiRzE5TktCSUxpaERBdjBORSIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IlRlc3QgdGhpcyBzZWN0aW9uIHdoZW
4gd3JpdGluZyBzaW5jZSBpdCB3YXMgdHJpY2t5IHdoZW4gSSBk
aWQgaXQiLCJjcmVhdGVkIjoxNjg2ODk4OTQwMDkzfSwiaXM4NG
dPY0Z6a0R3dE15ViI6eyJkaXNjdXNzaW9uSWQiOiJMNDJrTlBE
b0dDY3BGU3RrIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiR2l2ZSBzb21lIG1vcmUgaGludHMgb24gaG93IHRvIGRvIHRo
aXMiLCJjcmVhdGVkIjoxNjg2ODk5MDA5MDEzfX0sImhpc3Rvcn
kiOlstMTU1MDczNzIwNSwtMTM4MDE1MTI4OCw3MzA5OTgxMTZd
fQ==
-->