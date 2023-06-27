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

### Calculating regional efficiency

3. **Being familiar with the attribute data, now you’ll have to calculate the building efficiency ratios for each district in Helsinki using SeutuRAMAVA data.**
	1. Remember: **E = total floor area/total land area**
	2. However, you might’ve noticed that the data covers the entire capital region – but only Helsinki is wanted. You can either:
		- First calculate the efficiency ratio for all small areas in SeutuRAMAVA, and after the calculations are complete, extract Helsinki’s districts, or
		- Select/clip Helsinki’s districts before any calculations are done.
	3. *TIP: To help you in including the Helsinki small areas only – the municipalities have unique identifying codes. Helsinki’s municipality code is 091 (KUNTA-field).*
	4. *TIP 2: You might also want to discard the empty outer sea region (called ALUEMERI in the NIMI field) to make mapping simpler (Hint: )*
	5. 

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJySUlNQ2tUNkZLbkt2V1RKIjp7In
N0YXJ0IjoxMDk4LCJlbmQiOjExMzgsInRleHQiOiIqKkUgPSB0
b3RhbCBmbG9vciBhcmVhL3RvdGFsIGxhbmQgYXJlYSoqIn0sIl
VzR3N3d05pWVVDdnRLR0giOnsic3RhcnQiOjQzODUsImVuZCI6
NDM5MywidGV4dCI6Ii0gRmlndXJlIn0sIjFNdzdXY1p0dG16dm
ZPb3EiOnsic3RhcnQiOjQ2NzEsImVuZCI6NDY3OSwidGV4dCI6
Ii0gRmlndXJlIn0sImk1cldmZjgwSFJ5WGJydFAiOnsic3Rhcn
QiOjM1MTksImVuZCI6MzUyNSwidGV4dCI6Ik1vb2RsZSJ9LCJ5
ZnRIZXhDTURheG5vWVM5Ijp7InN0YXJ0Ijo1NzI1LCJlbmQiOj
U3MjksInRleHQiOiJIaW50In19LCJjb21tZW50cyI6eyJOTHQ0
Z05aV01nSjBPemxuIjp7ImRpc2N1c3Npb25JZCI6InJJSU1Da1
Q2RktuS3ZXVEoiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgZGlhZ3JhbSIsImNyZWF0ZWQiOjE2ODc4NDY0MzQyNj
B9LCJnYW52SzNORUtGM25DSVk1Ijp7ImRpc2N1c3Npb25JZCI6
IlVzR3N3d05pWVVDdnRLR0giLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODc4
NDY5MzI2ODN9LCI3R0ZTeFNWdWpFWXFuUVlWIjp7ImRpc2N1c3
Npb25JZCI6IjFNdzdXY1p0dG16dmZPb3EiLCJzdWIiOiJnaDo0
MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZW
QiOjE2ODc4NDY5Mzc1NDZ9LCI4a05vb1ZZcWtvbzlUMnNZIjp7
ImRpc2N1c3Npb25JZCI6Imk1cldmZjgwSFJ5WGJydFAiLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJGaXggcmVmZXJlbmNl
IiwiY3JlYXRlZCI6MTY4Nzg0Njk5MTM1NX0sIkQ3Wm16SXBPcX
JRYXI5eVYiOnsiZGlzY3Vzc2lvbklkIjoieWZ0SGV4Q01EYXhu
b1lTOSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZC
ByZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg3ODQ3MjAwMzE0fX0s
Imhpc3RvcnkiOls0MzAzOTU5NDhdfQ==
-->