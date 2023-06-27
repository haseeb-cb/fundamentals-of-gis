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

6. 


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
YXAsIG1ha2Ugc3Vy4oCmIn19LCJjb21tZW50cyI6eyJOTHQ0Z0
5aV01nSjBPemxuIjp7ImRpc2N1c3Npb25JZCI6InJJSU1Da1Q2
RktuS3ZXVEoiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOi
JBZGQgZGlhZ3JhbSIsImNyZWF0ZWQiOjE2ODc4NDY0MzQyNjB9
LCJnYW52SzNORUtGM25DSVk1Ijp7ImRpc2N1c3Npb25JZCI6Il
VzR3N3d05pWVVDdnRLR0giLCJzdWIiOiJnaDo0MDMwNDc4OCIs
InRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODc4ND
Y5MzI2ODN9LCI3R0ZTeFNWdWpFWXFuUVlWIjp7ImRpc2N1c3Np
b25JZCI6IjFNdzdXY1p0dG16dmZPb3EiLCJzdWIiOiJnaDo0MD
MwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQi
OjE2ODc4NDY5Mzc1NDZ9LCI4a05vb1ZZcWtvbzlUMnNZIjp7Im
Rpc2N1c3Npb25JZCI6Imk1cldmZjgwSFJ5WGJydFAiLCJzdWIi
OiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVmZXJlbmNlIi
wiY3JlYXRlZCI6MTY4Nzg0Njk5MTM1NX0sIkQ3Wm16SXBPcXJR
YXI5eVYiOnsiZGlzY3Vzc2lvbklkIjoieWZ0SGV4Q01EYXhub1
lTOSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBy
ZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3ODQ3MjAwMzE0fSwia2
JTblg0c3pxZ2FKYnNQbCI6eyJkaXNjdXNzaW9uSWQiOiJ6N2Nu
QlBZWndDalhXSGN3Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiTW92ZSB0byBlYXJsaWVyIGluIGNvdXJzZSIsImNyZWF0
ZWQiOjE2ODc4NDcyOTM4NDN9LCJ5bURuZ01qRUNJZVFSeWJNIj
p7ImRpc2N1c3Npb25JZCI6IkhyR2dNajI0NWRDdTlreU4iLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJNb3ZlIHRvIGVhcm
xpZXIgaW4gY291cnNlIiwiY3JlYXRlZCI6MTY4Nzg0NzI5NzY1
MX0sImxrbnREM3ZMWmh6anZYVXYiOnsiZGlzY3Vzc2lvbklkIj
oidmVvVUR3U3NRUFRuN3VpeSIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6Ik1vdmUgdG8gZWFybGllciBpbiBjb3Vyc2UiLC
JjcmVhdGVkIjoxNjg3ODQ3MzM2ODgyfX0sImhpc3RvcnkiOlsx
ODE0MDc2MzQzXX0=
-->