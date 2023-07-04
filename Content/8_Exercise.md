### Fundamentals of Geographic Information Systems (GIS)

# Exercise 8: Building efficiency & grids

By Sara Todorovic & Tatu Leppämäki for USP-303 at the Helsinki University. 

*Updated by Rowan van der Kaaden* 

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

1. Download 8_Exercise_data.zip from the [Github repository](https://github.com/rowan8k/fundamentals-of-gis/tree/master/Data), save it in a folder for this exercise, and extract the contents from the zip.  (see tips for effective adding of layers below!). 
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
RleHQiOiIqKkUgPSB0b3RhbCBmbG9vciBhcmVhL3RvdGFsIGxh
bmQgYXJlYSoqIiwic3RhcnQiOjEyMzksImVuZCI6MTI3OX0sIl
VzR3N3d05pWVVDdnRLR0giOnsidGV4dCI6Ii0gRmlndXJlIiwi
c3RhcnQiOjQ2NDQsImVuZCI6NDY1Mn0sIjFNdzdXY1p0dG16dm
ZPb3EiOnsidGV4dCI6Ii0gRmlndXJlIiwic3RhcnQiOjQ5MzAs
ImVuZCI6NDkzOH0sImk1cldmZjgwSFJ5WGJydFAiOnsidGV4dC
I6Ik1vb2RsZSIsInN0YXJ0IjozNzY5LCJlbmQiOjM3ODV9LCJ5
ZnRIZXhDTURheG5vWVM5Ijp7InRleHQiOiJIaW50Iiwic3Rhcn
QiOjU5ODUsImVuZCI6NTk4OX0sIno3Y25CUFlad0NqWFdIY3ci
OnsidGV4dCI6IipUSVAgMTogU2VsZWN0IGFsbCB5b3VyIHZlY3
RvciBsYXllcnMgYXQgb25jZSBieSBhcnJhbmdpbmcgdGhlIGZp
bGVzIGJ5IGZpbGUgdHnigKYiLCJzdGFydCI6NDM4NiwiZW5kIj
o0NjQyfSwiSHJHZ01qMjQ1ZEN1OWt5TiI6eyJ0ZXh0IjoiKlRJ
UCAyOiBXaGVuIHdvcmtpbmcgd2l0aCBkYXRhIHRoYXQgd2lsbC
Bwcm9iYWJseSBjb250YWluIHZhbHVlcyB3aXRoIHVtbGF1dHMg
KOKApiIsInN0YXJ0Ijo0NjU0LCJlbmQiOjQ5Mjh9LCJ2ZW9VRH
dTc1FQVG43dWl5Ijp7InRleHQiOiIqVElQIDI6IFRvIHJlbW92
ZSB1bm5lY2Vzc2FyeSBpbmZvcm1hdGlvbiBmcm9tIHRoZSBsZW
dlbmQgb2YgeW91ciBtYXAsIG1ha2Ugc3Vy4oCmIiwic3RhcnQi
OjYzMjcsImVuZCI6NjY0MH0sIjhsdXZpNFgxSURLOEFmWTMiOn
sidGV4dCI6IkRvd25sb2FkIGFuZCBpbnN0YWxsIGl0IHVzaW5n
IHRoZSBQbHVnaW4gbWFuYWdlci4iLCJzdGFydCI6Njg3NSwiZW
5kIjo2OTI0fSwieVp4SUdzUnh1akhRUllWZyI6eyJ0ZXh0Ijoi
VElQIiwic3RhcnQiOjczMDIsImVuZCI6NzMwNX0sIkIzdFFpWW
9La2RzTHl6NlYiOnsidGV4dCI6Im1hcCIsInN0YXJ0IjoyMDE1
LCJlbmQiOjIwMTh9LCJzZjkxV0ZaWDdDZHZISmkyIjp7InRleH
QiOiJQbHVnaW4iLCJzdGFydCI6NjkwOSwiZW5kIjo2OTE1fSwi
aFlFUFFyWlJ5MG5PSHJBZiI6eyJ0ZXh0IjoidmFsdWVzIiwic3
RhcnQiOjg4MTcsImVuZCI6ODgyM319LCJjb21tZW50cyI6eyJO
THQ0Z05aV01nSjBPemxuIjp7ImRpc2N1c3Npb25JZCI6InJJSU
1Da1Q2RktuS3ZXVEoiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJBZGQgZGlhZ3JhbSIsImNyZWF0ZWQiOjE2ODc4NDY0Mz
QyNjB9LCJnYW52SzNORUtGM25DSVk1Ijp7ImRpc2N1c3Npb25J
ZCI6IlVzR3N3d05pWVVDdnRLR0giLCJzdWIiOiJnaDo0MDMwND
c4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2
ODc4NDY5MzI2ODN9LCI3R0ZTeFNWdWpFWXFuUVlWIjp7ImRpc2
N1c3Npb25JZCI6IjFNdzdXY1p0dG16dmZPb3EiLCJzdWIiOiJn
aDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZW
F0ZWQiOjE2ODc4NDY5Mzc1NDZ9LCI4a05vb1ZZcWtvbzlUMnNZ
Ijp7ImRpc2N1c3Npb25JZCI6Imk1cldmZjgwSFJ5WGJydFAiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVmZXJl
bmNlIiwiY3JlYXRlZCI6MTY4Nzg0Njk5MTM1NX0sIkQ3Wm16SX
BPcXJRYXI5eVYiOnsiZGlzY3Vzc2lvbklkIjoieWZ0SGV4Q01E
YXhub1lTOSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCByZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3ODQ3MjAwMzE0
fSwia2JTblg0c3pxZ2FKYnNQbCI6eyJkaXNjdXNzaW9uSWQiOi
J6N2NuQlBZWndDalhXSGN3Iiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiTW92ZSB0byBlYXJsaWVyIGluIGNvdXJzZSIsIm
NyZWF0ZWQiOjE2ODc4NDcyOTM4NDN9LCJ5bURuZ01qRUNJZVFS
eWJNIjp7ImRpc2N1c3Npb25JZCI6IkhyR2dNajI0NWRDdTlreU
4iLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJNb3ZlIHRv
IGVhcmxpZXIgaW4gY291cnNlIiwiY3JlYXRlZCI6MTY4Nzg0Nz
I5NzY1MX0sImxrbnREM3ZMWmh6anZYVXYiOnsiZGlzY3Vzc2lv
bklkIjoidmVvVUR3U3NRUFRuN3VpeSIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6Ik1vdmUgdG8gZWFybGllciBpbiBjb3Vy
c2UiLCJjcmVhdGVkIjoxNjg3ODQ3MzM2ODgyfSwibkNldkNyTm
d2RUZVRzlnMSI6eyJkaXNjdXNzaW9uSWQiOiI4bHV2aTRYMUlE
SzhBZlkzIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQW
RkIGhpbnQiLCJjcmVhdGVkIjoxNjg3ODQ3NDA5ODUxfSwiRTMy
cXZrbUMwalBTQkluciI6eyJkaXNjdXNzaW9uSWQiOiJ5WnhJR3
NSeHVqSFFSWVZnIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg3ODQ3NTAwMD
EyfSwiemcySEVuOUZQMjNqRXBOZSI6eyJkaXNjdXNzaW9uSWQi
OiJCM3RRaVlvS2tkc0x5ejZWIiwic3ViIjoiZ2g6MjIxNjgxNT
ciLCJ0ZXh0IjoiQXNzdW1vbmcgdGhlIHRoZW9yeSBpcyBhYm91
dCBNQVVQIGFuZCBlY29sb2ljYWwgZmFsbGFjeSwgaXQgbWlnaH
QgYmUgZ29vZCB0byByZWZlciBiYWNrIHRoYXQgaGVyZS4iLCJj
cmVhdGVkIjoxNjg4MDM2Nzk4NzE3fSwid3JEcEVMcjNkaExUZ1
BiViI6eyJkaXNjdXNzaW9uSWQiOiJzZjkxV0ZaWDdDZHZISmky
Iiwic3ViIjoiZ2g6MjIxNjgxNTciLCJ0ZXh0IjoiSSB0aGluay
B5b3UgaGF2ZSBtZW50aW9uZWQgUGx1Z2luIE1hbmFnZXIgYWxy
ZWFkeSwgYnV0IGlmIG5vdCAtIHdvcnRoIGJyaWVmbHkgc2F5aW
5nIHdoeSBpdCBpcyB1c2VmdWwgaGVyZS4iLCJjcmVhdGVkIjox
Njg4MDM2OTQ3MzI1fSwiSHpkUmhKZFJyc2dseHg2aCI6eyJkaX
NjdXNzaW9uSWQiOiJoWUVQUXJaUnkwbk9IckFmIiwic3ViIjoi
Z2g6MjIxNjgxNTciLCJ0ZXh0IjoiY291bGQgcmVmZXIgYmFjay
B0byB0aGVvcnkgJ2ludGVycHJldCB0aGUgcmVzdWx0cywgY3Jp
dGljYWxseSByZWZsZWN0aW5nIG9uIE1BVVAvZXRjXCIiLCJjcm
VhdGVkIjoxNjg4MDM3MDIwOTczfX0sImhpc3RvcnkiOls4NjQz
NjAzNTQsLTc1MDM5OTM4NiwtMTIwNzA1Njk2OSwtMTA3MTIzMT
gzMV19
-->