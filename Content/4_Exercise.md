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
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJFdFByYk5zWUdNWWhPWXRSIjp7In
N0YXJ0IjoxNDUyLCJlbmQiOjE0NTgsInRleHQiOiJNb29kbGUi
fSwicjFuaW14MW1CdWx6YVhkViI6eyJzdGFydCI6MTk2MSwiZW
5kIjoxOTcwLCJ0ZXh0IjoiLSBQaWN0dXJlIn0sIkNVTHg0QmVW
RFZzMm5GSUEiOnsic3RhcnQiOjI4MzUsImVuZCI6Mjg0NCwidG
V4dCI6Ii0gUGljdHVyZSJ9fSwiY29tbWVudHMiOnsiSHUxb2w3
R2lGNmhCdDNjSSI6eyJkaXNjdXNzaW9uSWQiOiJFdFByYk5zWU
dNWWhPWXRSIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
Q29ycmVjdCIsImNyZWF0ZWQiOjE2ODY4OTg0MDY4MTJ9LCJJdU
c3aE5hT2k0UklhZktlIjp7ImRpc2N1c3Npb25JZCI6InIxbmlt
eDFtQnVsemFYZFYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY4OTg3NTU5
NDB9LCJXSE9hbEd4NWh5dkVKOENFIjp7ImRpc2N1c3Npb25JZC
I6IkNVTHg0QmVWRFZzMm5GSUEiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2OD
Y4OTg3ODc4MDV9fSwiaGlzdG9yeSI6WzMzMjIwNDQ5NiwtMTM4
MDE1MTI4OCw3MzA5OTgxMTZdfQ==
-->