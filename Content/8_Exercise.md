### Fundamentals of Geographic Information Systems (GIS)

# Exercise 8:

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


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJySUlNQ2tUNkZLbkt2V1RKIjp7In
N0YXJ0IjoxMDk4LCJlbmQiOjExMzgsInRleHQiOiIqKkUgPSB0
b3RhbCBmbG9vciBhcmVhL3RvdGFsIGxhbmQgYXJlYSoqIn0sIl
VzR3N3d05pWVVDdnRLR0giOnsic3RhcnQiOjQzODUsImVuZCI6
NDM5MywidGV4dCI6Ii0gRmlndXJlIn0sIjFNdzdXY1p0dG16dm
ZPb3EiOnsic3RhcnQiOjQ2NzEsImVuZCI6NDY3OSwidGV4dCI6
Ii0gRmlndXJlIn0sImk1cldmZjgwSFJ5WGJydFAiOnsic3Rhcn
QiOjM1MTksImVuZCI6MzUyNSwidGV4dCI6Ik1vb2RsZSJ9LCJ5
ZnRIZXhDTURheG5vWVM5Ijp7InN0YXJ0Ijo1NzI2LCJlbmQiOj
U3MzAsInRleHQiOiJIaW50In0sIno3Y25CUFlad0NqWFdIY3ci
Onsic3RhcnQiOjQxMjcsImVuZCI6NDM4MywidGV4dCI6IipUSV
AgMTogU2VsZWN0IGFsbCB5b3VyIHZlY3RvciBsYXllcnMgYXQg
b25jZSBieSBhcnJhbmdpbmcgdGhlIGZpbGVzIGJ5IGZpbGUgdH
nigKYifSwiSHJHZ01qMjQ1ZEN1OWt5TiI6eyJzdGFydCI6NDM5
NSwiZW5kIjo0NjY5LCJ0ZXh0IjoiKlRJUCAyOiBXaGVuIHdvcm
tpbmcgd2l0aCBkYXRhIHRoYXQgd2lsbCBwcm9iYWJseSBjb250
YWluIHZhbHVlcyB3aXRoIHVtbGF1dHMgKOKApiJ9LCJ2ZW9VRH
dTc1FQVG43dWl5Ijp7InN0YXJ0Ijo2MDY4LCJlbmQiOjYzODEs
InRleHQiOiIqVElQIDI6IFRvIHJlbW92ZSB1bm5lY2Vzc2FyeS
BpbmZvcm1hdGlvbiBmcm9tIHRoZSBsZWdlbmQgb2YgeW91ciBt
YXAsIG1ha2Ugc3Vy4oCmIn0sIjhsdXZpNFgxSURLOEFmWTMiOn
sic3RhcnQiOjY2MTYsImVuZCI6NjY2NSwidGV4dCI6IkRvd25s
b2FkIGFuZCBpbnN0YWxsIGl0IHVzaW5nIHRoZSBQbHVnaW4gbW
FuYWdlci4ifSwieVp4SUdzUnh1akhRUllWZyI6eyJzdGFydCI6
NzA0MywiZW5kIjo3MDQ2LCJ0ZXh0IjoiVElQIn19LCJjb21tZW
50cyI6eyJOTHQ0Z05aV01nSjBPemxuIjp7ImRpc2N1c3Npb25J
ZCI6InJJSU1Da1Q2RktuS3ZXVEoiLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgZGlhZ3JhbSIsImNyZWF0ZWQiOjE2
ODc4NDY0MzQyNjB9LCJnYW52SzNORUtGM25DSVk1Ijp7ImRpc2
N1c3Npb25JZCI6IlVzR3N3d05pWVVDdnRLR0giLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODc4NDY5MzI2ODN9LCI3R0ZTeFNWdWpFWXFuUVlW
Ijp7ImRpc2N1c3Npb25JZCI6IjFNdzdXY1p0dG16dmZPb3EiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVy
ZSIsImNyZWF0ZWQiOjE2ODc4NDY5Mzc1NDZ9LCI4a05vb1ZZcW
tvbzlUMnNZIjp7ImRpc2N1c3Npb25JZCI6Imk1cldmZjgwSFJ5
WGJydFAiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaX
ggcmVmZXJlbmNlIiwiY3JlYXRlZCI6MTY4Nzg0Njk5MTM1NX0s
IkQ3Wm16SXBPcXJRYXI5eVYiOnsiZGlzY3Vzc2lvbklkIjoieW
Z0SGV4Q01EYXhub1lTOSIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkFkZCByZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3OD
Q3MjAwMzE0fSwia2JTblg0c3pxZ2FKYnNQbCI6eyJkaXNjdXNz
aW9uSWQiOiJ6N2NuQlBZWndDalhXSGN3Iiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiTW92ZSB0byBlYXJsaWVyIGluIGNv
dXJzZSIsImNyZWF0ZWQiOjE2ODc4NDcyOTM4NDN9LCJ5bURuZ0
1qRUNJZVFSeWJNIjp7ImRpc2N1c3Npb25JZCI6IkhyR2dNajI0
NWRDdTlreU4iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JNb3ZlIHRvIGVhcmxpZXIgaW4gY291cnNlIiwiY3JlYXRlZCI6
MTY4Nzg0NzI5NzY1MX0sImxrbnREM3ZMWmh6anZYVXYiOnsiZG
lzY3Vzc2lvbklkIjoidmVvVUR3U3NRUFRuN3VpeSIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik1vdmUgdG8gZWFybGllci
BpbiBjb3Vyc2UiLCJjcmVhdGVkIjoxNjg3ODQ3MzM2ODgyfSwi
bkNldkNyTmd2RUZVRzlnMSI6eyJkaXNjdXNzaW9uSWQiOiI4bH
V2aTRYMUlESzhBZlkzIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiQWRkIGhpbnQiLCJjcmVhdGVkIjoxNjg3ODQ3NDA5OD
UxfSwiRTMycXZrbUMwalBTQkluciI6eyJkaXNjdXNzaW9uSWQi
OiJ5WnhJR3NSeHVqSFFSWVZnIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3
ODQ3NTAwMDEyfX0sImhpc3RvcnkiOlstMTgzODM3NDgxMl19
-->