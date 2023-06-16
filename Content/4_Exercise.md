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
	- ...the new and planned stations combined?

The Ring Rail Line is likely to increase the attraction for the real estate in the nearby area. This, however, will also raise the question of the noise levels caused by the Aircraft traffic around the Helsinki-Vantaa Airport. Thanks to new improved technology the aircraft noise levels have slightly dropped in recent years.

6. Find out how many people approximately live inside the dB zones: 65 or more and 50 or more in Helsinki region based on:
	- ...the noise levels in 2006?
	- ...the noise levels in 2010?

*Tip : For the Capital_region_people layer field name metadata, see Appendix in Exercise 4 instructions*

#### 2.2: Planning a new airport hotel & congress center near the ring rail line
You work in a team that is supposed to find an optimal location for a new Airport Hotel & Congress Center to the Helsinki-Vantaa Airport area based on accessibility. Your task is to follow the given requirements and make a map visualization of the area(s) to be shown at the company meeting of where the new Hotel & Congress center could possibly be located.



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
IG9uIHlvdXIgbWFwOiB3aGVyZSB0aGXigKYifSwiVlZoRndjYT
RQcVlPRXREQiI6eyJzdGFydCI6NDA1NSwiZW5kIjo0MTEzLCJ0
ZXh0IjoiMi4xOiBBbmFseXppbmcgdGhlIGVmZmVjdHMgb24gdG
hlIHBlb3BsZSBpbiB0aGUgc3R1ZHkgYXJlYSJ9LCJYQTNndVBG
R2FJb245b0dKIjp7InN0YXJ0Ijo0Mjg0LCJlbmQiOjQ0MjAsIn
RleHQiOiI1LiBGaW5kIG91dCBob3cgbWFueSBhcmUgbm90YWJs
eSBhZmZlY3RlZCBieSB0aGlzIGJ5IGNhbGN1bGF0aW5nIGhvdy
BtYW55IHBlb3Bs4oCmIn0sIm14SXl2d29SUExmRFlZVTMiOnsi
c3RhcnQiOjQ4MjksImVuZCI6NDk1MSwidGV4dCI6IjYuIEZpbm
Qgb3V0IGhvdyBtYW55IHBlb3BsZSBhcHByb3hpbWF0ZWx5IGxp
dmUgaW5zaWRlIHRoZSBkQiB6b25lczogNjUgb3IgbW9yZeKApi
J9fSwiY29tbWVudHMiOnsiSHUxb2w3R2lGNmhCdDNjSSI6eyJk
aXNjdXNzaW9uSWQiOiJFdFByYk5zWUdNWWhPWXRSIiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQ29ycmVjdCIsImNyZWF0
ZWQiOjE2ODY4OTg0MDY4MTJ9LCJJdUc3aE5hT2k0UklhZktlIj
p7ImRpc2N1c3Npb25JZCI6InIxbmlteDFtQnVsemFYZFYiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZS
IsImNyZWF0ZWQiOjE2ODY4OTg3NTU5NDB9LCJXSE9hbEd4NWh5
dkVKOENFIjp7ImRpc2N1c3Npb25JZCI6IkNVTHg0QmVWRFZzMm
5GSUEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
cGljdHVyZSIsImNyZWF0ZWQiOjE2ODY4OTg3ODc4MDV9LCJ0ZX
owbTJhdDN6WExmWHJjIjp7ImRpc2N1c3Npb25JZCI6IkcxOU5L
QklMaWhEQXYwTkUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJXcml0ZSB0aGlzIG91dCB3aXRoIG1vcmUgaW5zdHJ1Y3Rp
b25zLCBlLmcuIHJlbWluZCBob3cgdG8gZGlnaXRpemUsIGhvdy
B0byBlZGl0IGV4aXN0aW5nIGZlYXR1cmVzLCBldGMiLCJjcmVh
dGVkIjoxNjg2ODk4OTI1MzE3fSwiRU5aY0pwNHRGdlhxenliRi
I6eyJkaXNjdXNzaW9uSWQiOiJHMTlOS0JJTGloREF2ME5FIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVGVzdCB0aGlzIH
NlY3Rpb24gd2hlbiB3cml0aW5nIHNpbmNlIGl0IHdhcyB0cmlj
a3kgd2hlbiBJIGRpZCBpdCIsImNyZWF0ZWQiOjE2ODY4OTg5ND
AwOTN9LCJpczg0Z09jRnprRHd0TXlWIjp7ImRpc2N1c3Npb25J
ZCI6Ikw0MmtOUERvR0NjcEZTdGsiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJHaXZlIHNvbWUgbW9yZSBoaW50cyBvbiBo
b3cgdG8gZG8gdGhpcyIsImNyZWF0ZWQiOjE2ODY4OTkwMDkwMT
N9LCJHVU1tQ1RKaEt4azRQU2lOIjp7ImRpc2N1c3Npb25JZCI6
IlZWaEZ3Y2E0UHFZT0V0REIiLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgc2VjdGlvbiBpbiBtb29kbGUgd2hlcmUg
dG8gZmlsbCBpbiBhbnN3ZXJzIGZvciB0aGVzZSIsImNyZWF0ZW
QiOjE2ODY4OTkyNDQ5OTd9LCJabTZZNlZBRDc1RnVjTXZYIjp7
ImRpc2N1c3Npb25JZCI6IlhBM2d1UEZHYUlvbjlvR0oiLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJXcml0ZSBvdXQgaG93
IHRvIGRvIHRoaXM6IHRoZWlyIGZpcnN0IHRpbWUgZG9pbmcgYn
VmZmVyIGFuYWx5c2lzIiwiY3JlYXRlZCI6MTY4Njg5OTI3ODYy
OX0sIjZpbDdpU2VCSTNOVE1Cb3EiOnsiZGlzY3Vzc2lvbklkIj
oibXhJeXZ3b1JQTGZEWVlVMyIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IldyaXRlIG91dCBob3cgdG8gZG8gdGhpczogdG
hlaXIgZmlycyB0dGltZSBkb2luZyBidWZmZXIgYW5hbHlzaXMi
LCJjcmVhdGVkIjoxNjg2ODk5Mjk3NzMzfX0sImhpc3RvcnkiOl
s5NTY2MjM3MzUsLTEzODAxNTEyODgsNzMwOTk4MTE2XX0=
-->