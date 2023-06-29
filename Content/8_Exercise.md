### Fundamentals of Geographic Information Systems (GIS)

# Exercise 8: Building efficiency & grids

## OVERVIEW & PURPOSE

In this exercise your task is to **calculate building efficiency ratio on different spatial scales**. Efficiency ratios (e) describe the level of land use intensity on zoned city areas. The building efficiency ratio is calculated by **dividing the total floor area** of each story of a building (or buildings) **by the size of the piece of land the building is in**. The piece of land can be the real estate, a neighborhood, a city district or any specified area. This ratio can be used to identify areas which are urban (more efficient) from non-built (less efficient) areas. Conversely, “sparsity ratio” is the total area of all non-built features to the size of the piece of land. When calculating the building efficiency on a city district (or similar) scale, it depicts regional efficiency. When building efficiency is calculated on a property/plot scale it’s known as plot efficiency (see Table 1). During this exercise, you will discover the different forms and levels of urbanity in Helsinki.

**E = total floor area/total land area**

**The purpose of this exercise** is to get familiar with efficiency ratios and to understand how different spatial scales affect the apparent intensity of different phenomena (in our case building efficiency ratio). Simultaneously, we’re trying to analyze whether the building efficiency ratio is a sufficient indicator of urbanity.


## OBJECTIVES

1. Calculation of building efficiency ratio on a few different spatial scales
	
	- City district level (Helsinki ‘small areas’)
	- 250 m grid level
	- Optional: Real estate registry (or property) level

2. Composing at least two maps depicting building efficiency ratios on different spatial scales

3. Thinking about how altering the spatial scale affects a phenomenon depicted on a map
	
	- Be mindful of which efficiency ratio scoring (table 1) you use at different spatial scales when visualizing/interpreting the results.

## DATA USED/NEEDED

1. SeutuRAMAVA 2016 (zoning data of the Helsinki region)

	- Spatial scale is at city district (‘small area’) level

2. HSY’s SeutuCD building registry data 2013

	- Attribute data has been modified to protect the privacy of the inhabitants
	-  KERALA2-field has the total floor area (m2), use this field in the analysis!
		- (The original KERALA field also includes NoData -values, which will give you incorrect results – do not use that field. To save you some time, we have already created for you the KERALA2 field, where the original KERALA field’s values with 99999999 (or NoData) have been reassigned to be 0. So, use KERALA2, not KERALA.)

3. A 250-meter grid, which you will create (Plugin: MMQGIS)
	- Can be a grid of squares, diamonds or hexagons

4. Optional: HSY’s SeutuCD Real estate registry 2013
	- This data has been modified for privacy reasons

## COMPLETION

Work individually or in pairs. Complete the exercise and write a short reflection. Include the following:
1. At least two maps of building efficiency ratio on different spatial scales.
	- Remember: all maps should have a legend, a scale bar and a north arrow

2. Analysis of the maps, considering:
	-  What the maps tell of the urbanity within Helsinki
	-  What is omitted/revealed when switching spatial scales
	-  How well building efficiency ratio describes urbanity

## EXERCISE PHASES

### Getting familiar with the data

1. **Download, unzip and open the exercise 8 data in QGIS from the course Moodle page** (see tips for effective adding of layers below!). 
Then explore the attribute tables to familiarize yourself with what sorts of data you actually have (this is always a good practice).
	1. The fields you want to focus on (total floor area, m2) are: 
		- kara_yht in the SeutuRAMAVA layer
		- KERALA2 in the Building registry layer
	2.  Have a look at the lowest and highest values and the different field names (you can ask your Finnish-speaking peers for help). We have for example ones that seem to refer to municipality (kunta), small area codes (kauposanro), and  small area names (nimi).

*TIP 1: Select all your vector layers at once by arranging the files by file type when you are adding your layers. Click on the file type header > click on the first SHP file in the list > press and hold SHIFT key > click on the last SHP file on the list.*

- Figure

*TIP 2: When working with data that will probably contain values with umlauts (Å, Ä, Ö), change the encoding to e.g. UTF-8 already when adding your layers, so you won’t run into problems later. Choose UTF-8 in the Encoding dropdown menu and write UTF-8 into Encoding field.*

- Figure

2. **You might want to have a background map to help you get your bearings.**
	1. Use QuickMapServices or XYZ tiles as we have done earlier

---

### Calculating regional efficiency

3. **Being familiar with the attribute data, now you’ll have to calculate the building efficiency ratios for each district in Helsinki using SeutuRAMAVA data.**
	1. Remember: **E = total floor area/total land area**
	2. However, you might’ve noticed that the data covers the entire capital region – but only Helsinki is wanted. You can either:
		- First calculate the efficiency ratio for all small areas in SeutuRAMAVA, and after the calculations are complete, extract Helsinki’s districts, or
		- Select/clip Helsinki’s districts before any calculations are done.

*TIP 1: To help you in including the Helsinki small areas only – the municipalities have unique identifying codes. Helsinki’s municipality code is 091 (KUNTA-field).*

*TIP 2: You might also want to discard the empty outer sea region (called ALUEMERI in the NIMI field) to make mapping simpler (Hint: )*

4. **After calculating the efficiency ratios, compose a map.**
	1. Which districts have the highest efficiency? What about the lowest?
	2. Why do these districts have high/low efficiency scores?

*TIP 1: Visualize the map using a similar logic as is found in Table 1 and use the same visualization style for all maps you compose.*

*TIP 2: To remove unnecessary information from the legend of your map, make sure that the Auto Update box is unchecked in the Legend Items section of Item Properties in the print layout composer. Then remove (using the buttons with + and – symbols) and rename (by double-clicking on the title) items as you wish.*

---

### Calculating efficiency in a 250m grid

5. Remember: Make sure your project and layers are all in the same coordinate system.

6. **There are many ways to create a grid in QGIS. We’re going to utilize a plugin called MMQGIS. Download and install it using the Plugin manager.**

7. **After installing MMQGIS, there should be a drop-down menu at the top of the QGIS window with the name MMQGIS:**
	1. *Create* > *Create Grid Layer*
		1.  Define whether you want your grid to consist of rectangles, diamonds or hexagons (Geometry Type)
		2. Define the size of a grid element (X Spacing, Y Spacing, Units). Remember that we want to have a 250-meter grid. *TIP:* 
		3. Use Helsinki municipality borders as Extent.
		4. Save the resulting grid layer on your computer with an informative name (e.g. Helsinki_grid_250m)

8. **To join the building registry data into the grid layer:**
	1. First export the building registry data to Geopackage file format. (The spatial join operation takes an eternity if the layer is in Shapefile format.)
	2. As usual, save your project and any temporary layers now (in case of crash).
	3. **Join Attributes by Location (summary).**
		1. Because you want to **join building data into the grid**, the grid will be your Base layer (or Input layer, depending on QGIS version), and the Geopackaged building data will be your Join layer.
		2. You want information based on where floor area spatially coincides with your grid elements – what is a good Geometric predicate for this?
		3. Remember which field in the buildings layer contains the floor area?
		4. You need the sum of floor area in each cell.
		5. Make sure the parameters are set correctly before running the algorithm.
		6. Hit Run. This might take a while if your computer is tired. Have a coffee.

9. **Calculate the building efficiency ratio for the grid using field calculator. You need the *area of each cell* for this calculation.**
	1. Remember to choose an appropriate output field type.

--- 

### Map visualization  

10. **Compose a map of the outcome**
	
	1. Categorize the results using Table 1 like in the previous map
		- Be critical when interpreting the efficiency values

--- 

### Optional challenge 1

11. Calculate the building efficiency ratio using SeutuCD Real estate registry and building registry datasets.

12. Compose a map of the outcome.

---

### Optional challenge 2

13. Create a heatmap visualization of either the building efficiency ratio grid data or/and real estate data.
	
	1. Create centroids out of efficiency grid or/and real estate registry data
		1. Tip: Vector > Geometry Tools > Centroids
	2. Create a heatmap (Tip: Heatmap (Kernel Density Estimation)) using the centroids
		1. Set Weight from field to your efficiency ratio field (found under Advanced Parameters)
		2. Try different radiuses (e.g. 500 m, 1000 m and 2000 m) and kernel shapes
			- How does altering these affect the outcome?
		3. If you happen to encounter an error, try to reduce the rows and columns values

14. Compose a map of the heatmap analysis



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJySUlNQ2tUNkZLbkt2V1RKIjp7In
N0YXJ0IjoxMTI2LCJlbmQiOjExNjYsInRleHQiOiIqKkUgPSB0
b3RhbCBmbG9vciBhcmVhL3RvdGFsIGxhbmQgYXJlYSoqIn0sIl
VzR3N3d05pWVVDdnRLR0giOnsic3RhcnQiOjQ0MTMsImVuZCI6
NDQyMSwidGV4dCI6Ii0gRmlndXJlIn0sIjFNdzdXY1p0dG16dm
ZPb3EiOnsic3RhcnQiOjQ2OTksImVuZCI6NDcwNywidGV4dCI6
Ii0gRmlndXJlIn0sImk1cldmZjgwSFJ5WGJydFAiOnsic3Rhcn
QiOjM1NDcsImVuZCI6MzU1MywidGV4dCI6Ik1vb2RsZSJ9LCJ5
ZnRIZXhDTURheG5vWVM5Ijp7InN0YXJ0Ijo1NzU0LCJlbmQiOj
U3NTgsInRleHQiOiJIaW50In0sIno3Y25CUFlad0NqWFdIY3ci
Onsic3RhcnQiOjQxNTUsImVuZCI6NDQxMSwidGV4dCI6IipUSV
AgMTogU2VsZWN0IGFsbCB5b3VyIHZlY3RvciBsYXllcnMgYXQg
b25jZSBieSBhcnJhbmdpbmcgdGhlIGZpbGVzIGJ5IGZpbGUgdH
nigKYifSwiSHJHZ01qMjQ1ZEN1OWt5TiI6eyJzdGFydCI6NDQy
MywiZW5kIjo0Njk3LCJ0ZXh0IjoiKlRJUCAyOiBXaGVuIHdvcm
tpbmcgd2l0aCBkYXRhIHRoYXQgd2lsbCBwcm9iYWJseSBjb250
YWluIHZhbHVlcyB3aXRoIHVtbGF1dHMgKOKApiJ9LCJ2ZW9VRH
dTc1FQVG43dWl5Ijp7InN0YXJ0Ijo2MDk2LCJlbmQiOjY0MDks
InRleHQiOiIqVElQIDI6IFRvIHJlbW92ZSB1bm5lY2Vzc2FyeS
BpbmZvcm1hdGlvbiBmcm9tIHRoZSBsZWdlbmQgb2YgeW91ciBt
YXAsIG1ha2Ugc3Vy4oCmIn0sIjhsdXZpNFgxSURLOEFmWTMiOn
sic3RhcnQiOjY2NDQsImVuZCI6NjY5MywidGV4dCI6IkRvd25s
b2FkIGFuZCBpbnN0YWxsIGl0IHVzaW5nIHRoZSBQbHVnaW4gbW
FuYWdlci4ifSwieVp4SUdzUnh1akhRUllWZyI6eyJzdGFydCI6
NzA3MSwiZW5kIjo3MDc0LCJ0ZXh0IjoiVElQIn0sIkIzdFFpWW
9La2RzTHl6NlYiOnsic3RhcnQiOjE5MDIsImVuZCI6MTkwNSwi
dGV4dCI6Im1hcCJ9fSwiY29tbWVudHMiOnsiTkx0NGdOWldNZ0
owT3psbiI6eyJkaXNjdXNzaW9uSWQiOiJySUlNQ2tUNkZLbkt2
V1RKIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIG
RpYWdyYW0iLCJjcmVhdGVkIjoxNjg3ODQ2NDM0MjYwfSwiZ2Fu
dkszTkVLRjNuQ0lZNSI6eyJkaXNjdXNzaW9uSWQiOiJVc0dzd3
dOaVlVQ3Z0S0dIIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3ODQ2OTMyNj
gzfSwiN0dGU3hTVnVqRVlxblFZViI6eyJkaXNjdXNzaW9uSWQi
OiIxTXc3V2NadHRtenZmT29xIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3
ODQ2OTM3NTQ2fSwiOGtOb29WWXFrb285VDJzWSI6eyJkaXNjdX
NzaW9uSWQiOiJpNXJXZmY4MEhSeVhicnRQIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiRml4IHJlZmVyZW5jZSIsImNyZW
F0ZWQiOjE2ODc4NDY5OTEzNTV9LCJEN1pteklwT3FyUWFyOXlW
Ijp7ImRpc2N1c3Npb25JZCI6InlmdEhleENNRGF4bm9ZUzkiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcmVmZXJl
bmNlIiwiY3JlYXRlZCI6MTY4Nzg0NzIwMDMxNH0sImtiU25YNH
N6cWdhSmJzUGwiOnsiZGlzY3Vzc2lvbklkIjoiejdjbkJQWVp3
Q2pYV0hjdyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
1vdmUgdG8gZWFybGllciBpbiBjb3Vyc2UiLCJjcmVhdGVkIjox
Njg3ODQ3MjkzODQzfSwieW1EbmdNakVDSWVRUnliTSI6eyJkaX
NjdXNzaW9uSWQiOiJIckdnTWoyNDVkQ3U5a3lOIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiTW92ZSB0byBlYXJsaWVyIG
luIGNvdXJzZSIsImNyZWF0ZWQiOjE2ODc4NDcyOTc2NTF9LCJs
a250RDN2TFpoemp2WFV2Ijp7ImRpc2N1c3Npb25JZCI6InZlb1
VEd1NzUVBUbjd1aXkiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJNb3ZlIHRvIGVhcmxpZXIgaW4gY291cnNlIiwiY3JlYX
RlZCI6MTY4Nzg0NzMzNjg4Mn0sIm5DZXZDck5ndkVGVUc5ZzEi
OnsiZGlzY3Vzc2lvbklkIjoiOGx1dmk0WDFJREs4QWZZMyIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBoaW50Iiwi
Y3JlYXRlZCI6MTY4Nzg0NzQwOTg1MX0sIkUzMnF2a21DMGpQU0
JJbnIiOnsiZGlzY3Vzc2lvbklkIjoieVp4SUdzUnh1akhRUllW
ZyIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaW
N0dXJlIiwiY3JlYXRlZCI6MTY4Nzg0NzUwMDAxMn0sInpnMkhF
bjlGUDIzakVwTmUiOnsiZGlzY3Vzc2lvbklkIjoiQjN0UWlZb0
trZHNMeXo2ViIsInN1YiI6ImdoOjIyMTY4MTU3IiwidGV4dCI6
IkFzc3Vtb25nIHRoZSB0aGVvcnkgaXMgYWJvdXQgTUFVUCBhbm
QgZWNvbG9pY2FsIGZhbGxhY3ksIGl0IG1pZ2h0IGJlIGdvb2Qg
dG8gcmVmZXIgYmFjayB0aGF0IGhlcmUuIiwiY3JlYXRlZCI6MT
Y4ODAzNjc5ODcxN319LCJoaXN0b3J5IjpbLTE4NzkzMzg5NjAs
LTEyMDcwNTY5NjksLTEwNzEyMzE4MzFdfQ==
-->