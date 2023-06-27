### Fundamentals of Geographic Information Systems (GIS)

# Exercise 8:

## OVERVIEW & PURPOSE

In this exercise your task is to **calculate building efficiency ratio on different spatial scales**. Efficiency ratios (e) describe the level of land use intensity on zoned city areas. The building efficiency ratio is calculated by **dividing the total floor area** of each story of a building (or buildings) **by the size of the piece of land the building is in**. The piece of land can be the real estate, a neighborhood, a city district or any specified area. This ratio can be used to identify areas which are urban (more efficient) from non-built (less efficient) areas. Conversely, “sparsity ratio” is the total area of all non-built features to the size of the piece of land. When calculating the building efficiency on a city district (or similar) scale, it depicts regional efficiency. When building efficiency is calculated on a property/plot scale it’s known as plot efficiency (see Table 1). During this exercise, you will discover the different forms and levels of urbanity in Helsinki.

**E = total floor area/total land area**

**The purpose of this exercise** is to get familiar with efficiency ratios and to understand how different spatial scales affect the apparent intensity of different phenomena (in our case building efficiency ratio). Simultaneously, we’re trying to analyze whether the building efficiency ratio is a sufficient indicator of urbanity.


## OBJECTIVES

1. Calculation of building efficiency ratio on a few different spatial scales
	
	a. City district level (Helsinki ‘small areas’)
	b. 250 m grid level
	c. Optional: Real estate registry (or property) level

2. Composing at least two maps depicting building efficiency ratios on different spatial scales

3. Thinking about how altering the spatial scale affects a phenomenon depicted on a map
	
	a. Be mindful of which efficiency ratio scoring (table 1) you use at different spatial scales when visualizing/interpreting the results.

## DATA USED/NEEDED

1. SeutuRAMAVA 2016 (zoning data of the Helsinki region)

	1. Spatial scale is at city district (‘small area’) level

2. HSY’s SeutuCD building registry data 2013

	1. Attribute data has been modified to protect the privacy of the inhabitants
2.  KERALA2-field has the total floor area (m2), use this field in the analysis!
i. (The original KERALA field also includes NoData -values, which will give you incorrect results – do not use that field. To save you some time, we have already created for you the KERALA2 field, where the original KERALA field’s values with 99999999 (or NoData) have been reassigned to be 0. So, use KERALA2, not KERALA.)
3. A 250-meter grid, which you will create (Plugin: MMQGIS)
a. Can be a grid of squares, diamonds or hexagons
4. Optional: HSY’s SeutuCD Real estate registry 2013
a. This data has been modified for privacy reasons
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJySUlNQ2tUNkZLbkt2V1RKIjp7In
N0YXJ0IjoxMDk4LCJlbmQiOjExMzgsInRleHQiOiIqKkUgPSB0
b3RhbCBmbG9vciBhcmVhL3RvdGFsIGxhbmQgYXJlYSoqIn19LC
Jjb21tZW50cyI6eyJOTHQ0Z05aV01nSjBPemxuIjp7ImRpc2N1
c3Npb25JZCI6InJJSU1Da1Q2RktuS3ZXVEoiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgZGlhZ3JhbSIsImNyZWF0
ZWQiOjE2ODc4NDY0MzQyNjB9fSwiaGlzdG9yeSI6WzEzMDA0Mj
c0MDVdfQ==
-->