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
	- 
You can see the route in the Ring Rail Line Brochure PDF (see Moodle).

5. Make a visualization to show the ring rail line. Show on your map: where the railway is underground, which stations are new and whatever else you find convenient. You can use data you have from previous exercises (e.g. sea -layer).

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
InN0YXJ0Ijo0MDE5LCJlbmQiOjQyODUsInRleHQiOiI0LiBGb3
IgdmlzdWFsaXphdGlvbiBwdXJwb3NlcyB3ZSB3YW50IHRvIGhh
dmUgdW5kZXJncm91bmQgcGFydCBvZiB0aGUgcmFpbCBhcyBh4o
CmIn0sIkw0MmtOUERvR0NjcEZTdGsiOnsic3RhcnQiOjQyODgs
ImVuZCI6NDUyMSwidGV4dCI6IjUuIE1ha2UgYSB2aXN1YWxpem
F0aW9uIHRvIHNob3cgdGhlIHJpbmcgcmFpbCBsaW5lLiBTaG93
IG9uIHlvdXIgbWFwOiB3aGVyZSB0aGXigKYifSwiVlZoRndjYT
RQcVlPRXREQiI6eyJzdGFydCI6NDU3MywiZW5kIjo0NjMxLCJ0
ZXh0IjoiMi4xOiBBbmFseXppbmcgdGhlIGVmZmVjdHMgb24gdG
hlIHBlb3BsZSBpbiB0aGUgc3R1ZHkgYXJlYSJ9LCJYQTNndVBG
R2FJb245b0dKIjp7InN0YXJ0Ijo0ODAyLCJlbmQiOjQ5MzgsIn
RleHQiOiI1LiBGaW5kIG91dCBob3cgbWFueSBhcmUgbm90YWJs
eSBhZmZlY3RlZCBieSB0aGlzIGJ5IGNhbGN1bGF0aW5nIGhvdy
BtYW55IHBlb3Bs4oCmIn0sIm14SXl2d29SUExmRFlZVTMiOnsi
c3RhcnQiOjUzNDcsImVuZCI6NTQ2OSwidGV4dCI6IjYuIEZpbm
Qgb3V0IGhvdyBtYW55IHBlb3BsZSBhcHByb3hpbWF0ZWx5IGxp
dmUgaW5zaWRlIHRoZSBkQiB6b25lczogNjUgb3IgbW9yZeKApi
J9LCJueVhqS0t5czBwRlBDVW5uIjp7InN0YXJ0Ijo3NjAwLCJl
bmQiOjc2MTMsInRleHQiOiItIEFkZCBwaWN0dXJlIn0sInJqbU
1Xa0xJYTBGWTVqQVQiOnsic3RhcnQiOjYwODUsImVuZCI6Njc3
OCwidGV4dCI6IioqVGhlIHJlcXVpcmVtZW50cyBhcmUgYXMgZm
9sbG93cyoqOlxuLSBUaGUgSG90ZWwgJiBDb25ncmVzcyBDZW50
ZXIgaGFzIHRvIGJlIGxv4oCmIn0sIk4xSDBkRXhnU0FtQ3ZaMl
giOnsic3RhcnQiOjM4OTcsImVuZCI6MzkwMywidGV4dCI6ImV4
cG9ydCJ9fSwiY29tbWVudHMiOnsiSHUxb2w3R2lGNmhCdDNjSS
I6eyJkaXNjdXNzaW9uSWQiOiJFdFByYk5zWUdNWWhPWXRSIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCIsIm
NyZWF0ZWQiOjE2ODY4OTg0MDY4MTJ9LCJJdUc3aE5hT2k0Uklh
ZktlIjp7ImRpc2N1c3Npb25JZCI6InIxbmlteDFtQnVsemFYZF
YiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGlj
dHVyZSIsImNyZWF0ZWQiOjE2ODY4OTg3NTU5NDB9LCJXSE9hbE
d4NWh5dkVKOENFIjp7ImRpc2N1c3Npb25JZCI6IkNVTHg0QmVW
RFZzMm5GSUEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY4OTg3ODc4MDV9
LCJ0ZXowbTJhdDN6WExmWHJjIjp7ImRpc2N1c3Npb25JZCI6Ik
cxOU5LQklMaWhEQXYwTkUiLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJXcml0ZSB0aGlzIG91dCB3aXRoIG1vcmUgaW5zdH
J1Y3Rpb25zLCBlLmcuIHJlbWluZCBob3cgdG8gZGlnaXRpemUs
IGhvdyB0byBlZGl0IGV4aXN0aW5nIGZlYXR1cmVzLCBldGMiLC
JjcmVhdGVkIjoxNjg2ODk4OTI1MzE3fSwiRU5aY0pwNHRGdlhx
enliRiI6eyJkaXNjdXNzaW9uSWQiOiJHMTlOS0JJTGloREF2ME
5FIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVGVzdCB0
aGlzIHNlY3Rpb24gd2hlbiB3cml0aW5nIHNpbmNlIGl0IHdhcy
B0cmlja3kgd2hlbiBJIGRpZCBpdCIsImNyZWF0ZWQiOjE2ODY4
OTg5NDAwOTN9LCJpczg0Z09jRnprRHd0TXlWIjp7ImRpc2N1c3
Npb25JZCI6Ikw0MmtOUERvR0NjcEZTdGsiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJHaXZlIHNvbWUgbW9yZSBoaW50cy
BvbiBob3cgdG8gZG8gdGhpcyIsImNyZWF0ZWQiOjE2ODY4OTkw
MDkwMTN9LCJHVU1tQ1RKaEt4azRQU2lOIjp7ImRpc2N1c3Npb2
5JZCI6IlZWaEZ3Y2E0UHFZT0V0REIiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJBZGQgc2VjdGlvbiBpbiBtb29kbGUgd2
hlcmUgdG8gZmlsbCBpbiBhbnN3ZXJzIGZvciB0aGVzZSIsImNy
ZWF0ZWQiOjE2ODY4OTkyNDQ5OTd9LCJabTZZNlZBRDc1RnVjTX
ZYIjp7ImRpc2N1c3Npb25JZCI6IlhBM2d1UEZHYUlvbjlvR0oi
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXcml0ZSBvdX
QgaG93IHRvIGRvIHRoaXM6IHRoZWlyIGZpcnN0IHRpbWUgZG9p
bmcgYnVmZmVyIGFuYWx5c2lzIiwiY3JlYXRlZCI6MTY4Njg5OT
I3ODYyOX0sIjZpbDdpU2VCSTNOVE1Cb3EiOnsiZGlzY3Vzc2lv
bklkIjoibXhJeXZ3b1JQTGZEWVlVMyIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IldyaXRlIG91dCBob3cgdG8gZG8gdGhp
czogdGhlaXIgZmlycyB0dGltZSBkb2luZyBidWZmZXIgYW5hbH
lzaXMiLCJjcmVhdGVkIjoxNjg2ODk5Mjk3NzMzfSwiVUJaaWtK
TGExWmp5ZWpobSI6eyJkaXNjdXNzaW9uSWQiOiJueVhqS0t5cz
BwRlBDVW5uIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2ODk5NTkzMDA1fS
wiZnJ0MUZ3YVBHQnV1TUhnSSI6eyJkaXNjdXNzaW9uSWQiOiJy
am1NV2tMSWEwRlk1akFUIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLC
J0ZXh0IjoiRnVsbHkgZXhwbGFpbiBob3cgdGhleSBkbyB0aGlz
IiwiY3JlYXRlZCI6MTY4Njg5OTYwNTAwNX0sIjJFY09JUkZGTG
E1WGk5Um0iOnsiZGlzY3Vzc2lvbklkIjoiTjFIMGRFeGdTQW1D
dloyWCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
BoaW50IiwiY3JlYXRlZCI6MTY4Njk4MzAxOTI5MH19LCJoaXN0
b3J5IjpbMTI2OTk4Nzk5LDIwMTE5OTY3MTAsMTcwMDIzMzgxOS
w1MTE5OTk5MjIsMTg3MjEwNjYxNiwtNTQ4NjYyNDAsMjAzODI0
NjAxOCwtMjkzNjk0NzkxLC0xMzgwMTUxMjg4LDczMDk5ODExNl
19
-->